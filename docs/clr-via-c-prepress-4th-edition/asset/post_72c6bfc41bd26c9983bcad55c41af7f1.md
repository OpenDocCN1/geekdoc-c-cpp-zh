
```csharp
Type2 result2 = await Method2Async();
}
}
catch (Exception) {
    Console.WriteLine("Catch");
}
finally {
    Console.WriteLine("Finally");
}
return "Done";
}
```

While MyMethodAsync seems rather contrived, it demonstrates some key things. First it is an async function itself that returns a Task<String> but the code’s body ultimately returns a String. Second, it calls other functions that execute operations asynchronously, one standalone and the other from within a for loop. Finally, it also contains exception handling code. When compiling MyMethodAsync, the compiler transforms the code in this method to a state machine structure that is capable of being suspended and resumed.

I took the code above, compiled it, and then reverse engineered the IL code back into C# source code. I then simplified the code and added a lot of comments to it so you can understand what the compiler is doing to make async functions work. Below is the essence of the code created by the compiler’s transformation. I show the transformed MyMethodAsync method as well as the state machine structure it now depends on:

```csharp
// AsyncStateMachine attribute indicates an async method (good for tools using reflection);
// The type indicates which struct implements the state machine
[DebuggerStepThrough, AsyncStateMachine(typeof(StateMachine))]
private static Task<String> MyMethodAsync(Int32 argument) {
    // Create state machine instance & initialize it
    StateMachine stateMachine = new StateMachine() {
        // Create builder returning Task<String> from this stub method
        // State machine accesses builder to set Task completion/exception
        m_builder = AsyncTaskMethodBuilder<String>.Create(),

        m_state = -1,              // Initialize state
        m_argument = argument     // Copy arguments to state machine fields
    };

    // Start executing the state machine
    stateMachine.m_builder.Start(ref stateMachine);
    return stateMachine.m_builder.Task; // Return the state machine’s Task
}

// This is the state machine structure
[CompilerGenerated, StructLayout(LayoutKind.Auto)]
private struct StateMachine : IAsyncStateMachine {
    // Fields for the state machine’s builder (Task) & its location
    public AsyncTaskMethodBuilder<String> m_builder;
    public Int32 m_state;

    // Argument and local variables are fields now:
```

attaches the object being awaited to the state machine and I think it would be helpful if I explained how this piece of glue worked. Whenever you use the await operator in your code, the compiler takes the specified operand and attempts to call a GetAwaiter method on it. This method can be either an instance method or an extension method. The object returned from calling the GetAwaiter method is referred to as an awaiter. An awaiter is the glue I was referring to.

After the state machine obtains an awaiter, it queries its IsCompleted property. If the operation completed synchronously, true is returned and, as an optimization, the state machine simply continues executing. At this point, it calls the awaiter's GetResult method which either throws an exception if the operation failed or returns the result if the operation was successful. The state machine continues running from here to process the result.

If the operation completes asynchronously, IsCompleted returns false. In this case, the state machine calls the awaiter's OnCompleted method passing it a delegate to the state machine's MoveNext method. And now, the state machine allows its thread to return back to where it came from so that it can execute other code. In the future, the awaiter, which wraps the underlying Task, knows when it completes and invokes the delegate causing MoveNext to execute. The fields within the state machine are used to figure out how to get to the right point in the code giving the illusion that the method is continuing from where it left off. At this point, the code calls the awaiter's GetResult method and execution continues running from here to process the result.

That is how async functions work and the whole purpose is to simplify the coding effort normally involved when writing non-blocking code.

## Async Function Extensibility

As for extensibility, if you can wrap a Task object around an operation that completes in the future, you can use the await operator to await that operation. Having a single type (Task) to represent all kinds of asynchronous operations is phenomenally useful because it allows you to implement combinators (like Task's WhenAll and WhenAny methods) and other helpful operations. Later in this chapter, I demonstrate doing this by wrapping a CancellationToken with a Task so I can await an asynchronous operation while also exposing timeout and cancellation.

I'd also like to share with you another example. Below is my TaskLogger class which you can use to show you asynchronous operations which haven't yet completed. This is very useful in debugging scenarios especially when your application appears hung due to a bad request or a non-responding server.

```csharp
public static class TaskLogger {
    public enum TaskLogLevel { None, Pending }
    public static TaskLogLevel LogLevel { get; set; }

    public sealed class TaskLogEntry {
        public Task Task { get; internal set; }
        public String Tag { get; internal set; }
        public DateTime LogTime { get; internal set; }
        public String CallerMemberName { get; internal set; }
        public String CallerFilePath { get; internal set; }
        public Int32 CallerLineNumber { get; internal set; }
        public override string ToString() {
            return String.Format("LogTime={0}, Tag={1}, Member={2}, File={3}({4})",
                LogTime, Tag ?? "(none)", CallerMemberName, CallerFilePath, CallerLineNumber);
        }
    }

    private static readonly ConcurrentDictionary<Task, TaskLogEntry> s_log =
        new ConcurrentDictionary<Task, TaskLogEntry>();
    public static IEnumerable<TaskLogEntry> GetLogEntries() { return s_log.Values; }

    public static Task<TResult> Log<TResult>(this Task<TResult> task, String tag = null,
        [CallerMemberName] String callerMemberName = null,
        [CallerFilePath] String callerFilePath = null,
        [CallerLineNumber] Int32 callerLineNumber = -1) {
        return (Task<TResult>)Log((Task)task, tag, callerMemberName, callerFilePath, callerLineNumber);
    }
    public static Task Log(this Task task, String tag = null,
        [CallerMemberName] String callerMemberName = null,
        [CallerFilePath] String callerFilePath = null,
        [CallerLineNumber] Int32 callerLineNumber = -1) {
        if (LogLevel == TaskLogger.TaskLogLevel.None) return task;
        var logEntry = new TaskLogEntry {
            Task = task,
            LogTime = DateTime.Now,
            Tag = tag,
            CallerMemberName = callerMemberName,
            CallerFilePath = callerFilePath,
            CallerLineNumber = callerLineNumber
        };
        s_log[task] = logEntry;
        task.ContinueWith(t => { TaskLogEntry entry; s_log.TryRemove(t, out entry); },
            TaskContinuationOptions.ExecuteSynchronously);
        return task;
    }
}
```

And here is some code that demonstrates the use of the class:

```csharp
public static async Task Go() {
#if DEBUG
    // Using TaskLogger incurs a memory and performance hit; so turn it on in debug builds
    TaskLogger.LogLevel = TaskLogger.TaskLogLevel.Pending;
#endif

    // Initiate 3 task; for testing the TaskLogger, we control their duration explicitly
    var tasks = new List<Task> {
        Task.Delay(2000).Log("2s op"),
        Task.Delay(5000).Log("5s op"),
        Task.Delay(6000).Log("6s op")
    };

    try {
        // Wait for all tasks but cancel after 3 seconds; only 1 task above should complete in time
        // Note: WithCancellation is my extension method described later in this chapter
        await Task.WhenAll(tasks).
            WithCancellation(new CancellationTokenSource(3000).Token);
    }
    catch (OperationCanceledException) { }

    // Ask the logger which tasks have not yet completed and sort
    // them in order from the one that's been waiting the longest
    foreach (var op in TaskLogger.GetLogEntries().OrderBy(tie => tie.LogTime))
        Console.WriteLine(op);
}
```

When I build and run this code, I get the following output:

```text
LogTime=7/16/2012 6:44:31 AM, Tag=6s op, Member=Go, File=C:\LR via C#\Code\Ch28-1-100qs.cs(332)
LogTime=7/16/2012 6:44:31 AM, Tag=5s op, Member=Go, File=C:\LR via C#\Code\Ch28-1-100qs.cs(331)
```

In addition to all the flexibility you have with using Task, async functions have another extensibility point: the compiler calls GetAwaiter on whatever operand is used with await. So, the operand doesn't have to be a Task object at all; it can be of any type as long as it has a GetAwaiter method available to call. Here is an example of my own awaiter that is the glue between an async method's state machine and an event being raised:

```csharp
public sealed class EventAwaiter<TEventArgs> : INotifyCompletion {
    private ConcurrentQueue<TEventArgs> m_events = new ConcurrentQueue<TEventArgs>();
    private Action m_continuation;

    #region Members invoked by the state machine
    // The state machine will call this first to get our awaiter; we return ourself
    public EventAwaiter<TEventArgs> GetAwaiter() { return this; }

    // Tell state machine if any events have happened yet
    public Boolean IsCompleted { get { return m_events.Count > 0; } }

    // The state machine tells us what method to invoke later; we save it
    public void OnCompleted(Action continuation) {
        Volatile.Write(ref m_continuation, continuation);
    }

    // The state machine queries the result; this is the await operator's result
    public TEventArgs GetResult() {
        TEventArgs e;
        m_events.TryDequeue(out e);
        return e;
    }
    #endregion

    // Potentially invoked by multiple threads simultaneously when each raises the event
    public void EventRaised(Object sender, TEventArgs eventArgs) {
        m_events.Enqueue(eventArgs);   // Save EventArgs to return it from GetResult/await
```
