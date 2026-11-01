```
{
    // Create a cancellation token source
    CancellationTokenSource cts = new
CancellationTokenSource();

    CancellationToken token = cts.Token;

    // Start a task that can be cancelled
    Task longRunningTask = Task.Run(() =>
    {
        while (!token.IsCancellationRequested)
        {
            Console.WriteLine("Task running...");
            Thread.Sleep(1000); // Simulate work
        }
        Console.WriteLine("Task cancelled.");
    }, token);

    // Wait for user input to cancel the task
    Console.WriteLine("Press Enter to cancel the task.");
    Console.ReadLine();

    // Cancel the task using the cancellation token
    cts.Cancel();
}
```