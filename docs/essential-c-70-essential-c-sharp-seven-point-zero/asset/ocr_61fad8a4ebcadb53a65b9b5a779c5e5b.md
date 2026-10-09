```
public class AsyncSynchronizationContext : SynchronizationContext
{
    public Exception Exception { get; set; }
    public ManualResetEventSlim ResetEvent { get; } = new ManualResetEventSlim();

    public override void Send(SendOrPostCallback callback, object state)
    {
        try
        {
            Console.WriteLine($"Send notification invoked...(Thread ID: {Thread.CurrentThread.ManagedThreadId}")";
            callback(state);
        }
        catch (Exception exception)
        {
            Exception = exception;
#if !WithOutUsingResetEvent
            ResetEvent.Set();
#endif
        }
    }

    public override void Post(SendOrPostCallback callback, object state)
    {
        try
        {
            Console.WriteLine($"Post notification invoked...(Thread ID: {Thread.CurrentThread.ManagedThreadId}")";
            callback(state);
        }
        catch (Exception exception)
        {
            Exception = exception;
#if !WithOutUsingResetEvent
            ResetEvent.Set();
#endif
        }
    }
}

public class Program
{
    static bool EventTriggered { get; set; }
    public const string ExpectedExceptionMessage = "Expected Exception";

    public static void Main()
    {
        AsyncSynchronizationContext synchronizationContext =
            new AsyncSynchronizationContext();
        SynchronizationContext.SetSynchronizationContext(synchronizationContext);
```