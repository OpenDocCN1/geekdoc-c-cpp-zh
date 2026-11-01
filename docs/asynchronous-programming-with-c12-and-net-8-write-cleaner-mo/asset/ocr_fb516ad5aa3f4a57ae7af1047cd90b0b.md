```
```csharp
public class TaskCancellationExample
{
    public async Task ProcessDataAsync(CancellationToken cancellationToken)
    {
        try
        {
            await Task.Delay(5000, cancellationToken); // Simulate long-running operation
            Console.WriteLine("Task completed.");
        }
        catch (TaskCanceledException)
        {
            Console.WriteLine("Task was canceled.");
        }
    }
}
```
```

In the above example, `ProcessDataAsync` method accepts a `CancellationToken` to allow cancellation of the asynchronous operation. Use `cancellationToken.ThrowIfCancellationRequested()` to check for cancellation within the method.

# **Best Practices:**

+   - **Pass CancellationToken:** Always pass a `CancellationToken` to async methods and propagate cancellation through the call chain.
+   - **Handle Cancellation:** Use try-catch blocks to catch `TaskCanceledException` or check `cancellationToken.IsCancellationRequested` within async methods.
+   - **Cancel Pending Tasks:** Cancel pending tasks promptly when cancellation is requested to release