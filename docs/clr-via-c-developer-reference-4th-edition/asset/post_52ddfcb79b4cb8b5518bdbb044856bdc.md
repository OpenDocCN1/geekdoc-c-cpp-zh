
```cs
// Fields for state machine's builder (Task) & its location
public AsyncTaskMethodBuilder<String> m_builder;
public Int32 m_state;
```

```cs
// Argument and local variables are fields now:
public Int32 m_argument, m_local, m_x;
public Type1 m_resultType1;
public Type2 m_resultType2;
```

```cs
// There is 1 awaiter type.
// Only 1 of these fields is important at any time. That field refers
// to the most recently executed awaiter that is completing asynchronously:
private TaskAwaiter<Type1> m_awaiterType1;
private TaskAwaiter<Type2> m_awaiterType2;
```

```cs
// This is the state machine method itself
void IASyncStateMachine.MoveNext() {
String result = null; // Task's result value
```

```cs
// Compiler-inserted finally block ensures the state machine's tasks completes
try {
Boolean executeFinally = true; // Assume we're logically leaving the 'try' block
if (m_state == -1) { // 1st time in state machine method,
m_local = m_argument; // execute start of original method
}
```

```cs
// Try block that we had in our original code
try {
TaskAwaiter<Type1> m_awaiterType1;
TaskAwaiter<Type2> m_awaiterType2;
```

```cs
// Tell awaiter to call Next when operation completes
m_builder.AwaitUnsafeCompleted(ref awaiterType1, ref this);
// The line above invokes awaiterType1's OnCompleted which is approximately
// calls ContinueWith(() => Next()) on the Task being awaited.
// When the Task completes, the ContinueWith calls MoveNext
```

```cs
executeFinally = false; // We're not logically leaving the 'try'
return; // block
// Thread returns to caller
```

```cs
// Method1Async completed synchronously
break;
```

```cs
case 0: // Method1Async completed asynchronously
awaiterType1 = m_awaiterType1; // Restore most-recent awaiter
break;
```

```cs
case 1: // 'Method2Async' completed asynchronously
awaiterType2 = m_awaiterType2; // Restore most-recent awaiter
goto ForLoopEpilog;
```

// After the first await, we capture the result & start the 'for' loop
m_result = awaitType1.GetResult(); // Get await's result

```cs
ForLoopPrologue:
m_x = 0; // 'for' loop initialization
goto ForLoopBody; // Skip to 'for' loop body
```

```cs
ForLoopEpilog:
m_resultType2 = awaiterType2.GetResult();
m_x++; // Increment x after each loop iteration
// Fall into the 'for' loop's body
```

```cs
catch (Exception) {
Console.WriteLine("Catch");
finally {
// Whenever a thread physically leaves a 'try', the 'finally' executes
// We only want to execute this code when thread logically leaves the 'try'
if (executeFinally) {
Console.WriteLine("Finally");
}
result = "Done"; // What we ultimately want to return from the async
}
catch (Exception exception) {
// Unhandled exception: complete state machine's Task with exception
m_builder.SetException(exception);
return;
}
// No exception: complete state machine's Task with result
m_builder.SetResult(result);
}
```

If you spend the time to walk through the preceding code and read all the comments, I think you'll be able to fully digest what the compiler does for you. However, there is a piece of glue that attaches the object awaited to the state machine and I think it would be helpful if I explained how this piece of glue worked. Whenever you use the await operator in your code, the compiler takes the specified operand and attempts to call a GetAwaiter method on it. This method can be either an instance method or an extension method. The object returned from calling the GetAwaiter method is referred to as an awaiter. An awaiter is the glue I was referring to.

After the state machine obtains an awaiter, it queries its IsCompleted property. If the operation completed synchronously, true is returned, and as an optimization, the state machine continues executing. But at this point, it calls the awaiter's GetResult method, which either throws an exception if the operation failed or returns the result if the operation was successful. The state machine continues running here to process the result.

If the operation completes asynchronously, IsCompleted returns false. In this case, the state machine calls the awaiter's OnCompleted method passing a delegate to the state machine's MoveNext method. And now, the state machine uses its thread to return to where it can execute code. In the future, the awaiter, which wraps the underlying Task, knows when it completes and invokes the delegate calling MoveNext to execute. The fields within the state machine are used to figure out how to get the right point in the code, giving the illusion that method is continuing from where it left off. At this point, the code calls the awaiter's GetResult method and execution continues here to process the result.

That is how async functions work and the whole purpose is to simplify the coding effort when writing non-blocking code.

## Async Function Extensibility

If you can wrap an object around an operation that completes in the future, you can use the await operator to await that operation. Having a single type (Task) to represent all kinds of asynchronous operations is phenomenally useful because it allows to implement combinators (like Task.WhenAll and WhenAny) and other helpful operations. In this chapter, I demonstrate this by wrapping CancellationToken with Task to show your asynchronous operations that haven't yet completed. This is very useful in debugging scenarios when your application hangs due to a bad request or non-responsive responder. I'd also like to share with you another example. The following is TaskLogger class, which you can use to show extensibility.

```cs
public static class TaskLogger {
    public enum TaskLogLevel { None, Pending }
    public static TaskLogLevel Level { get; set; }

    public sealed class TaskEntry {
        public Task Task { get; set; }
        public DateTime LogTime { get; set; }
        public String CallerName { get; set; }
        public String CallerPath { get; set; }
        public Int32 CallerNumber { get; set; }
        public override string ToString() {
            return String.Format("LogTime={0}, Tag={1}, Member={2}, File={3}",
                LogTime, Tag, CallerName, CallerPath);
        }
    }

    private static readonly ConcurrentDictionary<Task, TaskEntry> s_log = new ConcurrentDictionary<Task, TaskEntry>();
    public static IEnumerable<TaskEntry> GetEntries() { return s_log.Values; }

    public static TaskResult<T> Log<T>(Task task, String tag = null, String callerName = null, String callerPath = null, Int32 CallerNumber = -1) {
        return new TaskResult<T>();
    }

    public static Task Log(Task task, String tag = null, String callerName = null, String callerPath = null, Int32 CallerNumber = -1) {
        if (LogLevel == TaskLevel.None) return task;
        var logEntry = new TaskEntry {
            Task = task,
            LogTime = DateTime.Now,
            Tag = tag,
            CallerName = callerName,
            CallerPath = callerPath,
            CallerNumber = CallerNumber
        };
        s_log[task] = logEntry;
        task.ContinueWith(t => { TaskEntry entry; s_log.Remove(task, out entry); }, TaskContinuationOptions.ExecuteSynchronously);
        return task;
    }
}
```

Here is some code that demonstrates the use of the class.

```cs
public static async Task Go() {
    #if DEBUG
    // Using Logger incurs a memory and performance hit; turn it off in debug builds
    TaskLogger.LogLevel = TaskLogLevel.Pending;
    #endif

    // Initiate 3 tasks; for testing the Logger, we control their duration explicitly
    var tasks = new List<Task>();
    Task.Delay(2000).Log("2s op");
    Task.Delay(5000).Log("5s op");
    Task.Delay(6000).Log("6s op");

    try {
      // Wait for all tasks but cancel after 3 seconds; only 1 task should complete in time
      // Note: WithCancellation is my extension method described later in this chapter
      await Task.WhenAll(tasks);
      WithCancellation(new CancellationTokenSource(3000).Token);
    }
    catch (OperationCanceledException) { }

    // Ask the logger which tasks have not yet completed and sort
    // them in order from the one's been waiting the longest
    foreach (var op in TaskLogger.GetEntries().OrderBy(tle => tle.LogTime)) {
        Console.WriteLine(op);
    }
}
```

When I build and run this code, I get the following output:

```
LogTime=7/16/2012 6:44:31 AM, Tag=6s op, Member=Go, File=C:\CLR\Code\Ch28-1-I0ops.cs(332)
LogTime=7/16/2012 6:44:31 AM, Tag=5s op, Member=Go, File=C:\CLR\Code\Ch28-1-I0ops.cs(331)
```

In addition to all the flexibility you have using Task, async functions have another extensibility: the compiler calls GetAwait on whatever operand is used with await. So, the operand doesn't have to be a Task object at all; it can be of any type as long as it has a GetAwait method available to call. Here is an example of my awaiter that is the glue between async method's state machine and event being raised.

```cs
public sealed class EventAwaiter<TEventArgs> : NotifyCompletion {
  private ConcurrentQueue<TEventArgs> m_events = new ConcurrentQueue<TEventArgs>();
  private Action m_continuation;

  #region Members invoked will call this first to get our awaiter; we return ourselves
  public EventAwaiter<TEventArgs> GetAwait() { return this; }

  // Tell the state machine if any events have happened
  public bool IsCompleted() { return m_events.Count > 0; }

  // The state machine tells us method how to invoke later; we save it
  public void OnCompleted(Action continuation) {
    Volatile.Write(ref m_continuation, continuation);
  }

  // The state machine queries the result; this is the awaiter's result
  public TEventArgs GetResult() {
    TEventArgs e;
    m_events.TryDequeue(out e);
    return e;
  }
  #endregion

  // Potentially invoked by multiple threads simultaneously when each raises the event
}
```
