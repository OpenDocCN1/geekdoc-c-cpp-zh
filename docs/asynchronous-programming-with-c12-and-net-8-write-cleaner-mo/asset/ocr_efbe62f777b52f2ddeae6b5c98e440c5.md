```
await longRunningTask; // Wait for the task to complete
(optional)
}
}
...
```

In this example, we create a cancellation token source (`CancellationTokenSource`) and use it to cancel a long-running task when the user presses Enter.

# 4. Exception Handling with Tasks:

Tasks in the TPL support exception handling to handle errors that occur during asynchronous operations. You can use `try/catch` blocks or `await` with `Task.WhenAll` for handling multiple tasks and exceptions.

# Exception Handling Example:

```
```csharp
public class Program
{
    public static async Task Main()
    {
        Task<int> task1 = Task.Run(() =>
        {
            throw new Exception("Error in Task 1");
            return 0; // This line won't be reached
```