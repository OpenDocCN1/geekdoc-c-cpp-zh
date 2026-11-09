
```csharp
// Fields for state machine's builder (Task) & its location
public AsyncTaskMethodBuilder<String> m_builder;
public Int32 m_state;

// Argument and local variables are fields now:
public Int32 m_argument, m_local, m_x;
public Type1 m_resultType1;
public Type2 m_resultType2;

// There is 1 field per awaiter type.
// Only 1 of these fields is important at any time. That field refers
// to the most recently executed await that is completing asynchronously:
private TaskAwaiter<Type1> m_awaiterType1;
private TaskAwaiter<Type2> m_awaiterType2;

// This is the state machine method itself
void IAsyncStateMachine.MoveNext()
{
    String result = null;   // Task's result value

    // Compiler-inserted try block ensures the state machine's task completes
    try {
        Boolean executeFinally = true;  // Assume we're logically leaving the 'try' block
        if (m_state == -1) {             // If 1st time in state machine method,
            m_local = m_argument;       // Execute start of original method
        }

        // Try block that we had in our original code
        try {
            TaskAwaiter<Type1> awaiterType1;
            TaskAwaiter<Type2> awaiterType2;

            switch (m_state) {
                case -1: // Start execution of code in 'try'
                    // Call Method1Async and get its awaiter
                    awaiterType1 = Method1Async().GetAwaiter();
                    if (!awaiterType1.IsCompleted) {
                        m_state = 0;                 // 'Method1Async' is completing
                                                       // asynchronously
                        m_awaiterType1 = awaiterType1; // Save the awaiter for when we come back

                        // Tell awaiter to call MoveNext when operation completes
                        m_builder.AwaitUnsafeOnCompleted(ref awaiterType1, ref this);
                        // The line above invokes awaiterType1's OnCompleted which approximately
                        // calls Continuation(this => MoveNext()) on the Task being awaited.
                        // When the Task completes, the Continuation with task calls MoveNext

                        executeFinally = false;       // We're not logically leaving the 'try'
                                                       // block
                        return;                         // Thread returns to caller
                    }
                } // 'Method1Async' completed synchronously
                break;

                case 0: // 'Method1Async' completed asynchronously
                    awaiterType1 = m_awaiterType1; // Restore most-recent awaiter
                    break;
```

如果你花时间仔细阅读前面的代码和所有注释，我认为你就能完全理解编译器为你做了什么。然而，有一块“胶水”将被等待的对象连接到状态机，我认为解释这块胶水如何工作会很有帮助。每当你在代码中使用 await 运算符时，编译器会获取指定的操作数并尝试调用它的 GetAwaiter 方法。这个方法可以是实例方法或扩展方法。调用 GetAwaiter 方法返回的对象称为 awaiter。awaiter 就是我所说的胶水。

状态机获得 awaiter 后，会查询它的 IsCompleted 属性。如果操作同步完成，则返回 true，作为一种优化，状态机直接继续执行。此时，它调用 awaiter 的 GetResult 方法：如果操作失败，该方法抛出异常；如果操作成功，则返回结果。状态机从这里继续运行以处理结果。

如果操作异步完成，IsCompleted 返回 false。在这种情况下，状态机调用 awaiter 的 OnCompleted 方法，并向它传递一个指向状态机 MoveNext 方法的委托。现在，状态机允许其线程返回到原来的位置，以便执行其他代码。将来，包装底层 Task 的 awaiter 知道何时完成，并调用该委托使 MoveNext 执行。状态机中的字段用于确定如何到达代码中的正确位置，从而造成方法从上次离开的地方继续执行的假象。此时，代码调用 awaiter 的 GetResult 方法，执行从这里继续运行以处理结果。

这就是 async 函数的工作方式，其全部目的就是简化通常编写非阻塞代码时所涉及的编码工作。

## 异步函数的可扩展性

至于可扩展性，如果你能将一个 Task 对象包装在将来完成的操作上，就可以使用 await 运算符等待该操作。用单一类型（Task）表示所有类型的异步操作非常有用，因为它允许你实现组合器（如 Task 的 WhenAll 和 WhenAny 方法）以及其他有用的操作。在本章后面，我将演示通过用 Task 包装 CancellationToken 来做到这一点，这样我就可以等待异步操作，同时暴露超时和取消。

我还想与你分享另一个示例。下面是我的 TaskLogger 类，你可以用它来显示尚未完成的异步操作。这在调试场景中非常有用，尤其是当你的应用程序由于错误请求或无响应的服务器而看起来挂起时。

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
        public override String ToString() {
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
        return (Task<TResult>)
            Log(task, tag, callerMemberName, callerFilePath, callerLineNumber);
    }

    public static Task Log(this Task task, String tag = null,
        [CallerMemberName] String callerMemberName = null,
        [CallerFilePath] String callerFilePath = null,
        [CallerLineNumber] Int32 callerLineNumber = -1) {
        if (LogLevel == TaskLogLevel.None) return task;
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

下面是一些演示该类用法的代码。

```csharp
public static async Task Go() {
#if DEBUG
    // Using TaskLogger incurs a memory and performance hit, so turn it on in debug builds
    TaskLogger.LogLevel = TaskLogger.TaskLogLevel.Pending;
#endif

    // Initiate 3 tasks; for testing the TaskLogger, we control their duration explicitly
    var tasks = new List<Task> {
        Task.Delay(2000).Log("2s op"),
        Task.Delay(5000).Log("5s op"),
        Task.Delay(10000).Log("10s op")
```
