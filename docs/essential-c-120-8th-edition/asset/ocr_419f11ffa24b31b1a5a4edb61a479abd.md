```
try
{
    Task.WaitAny(task, cancelTask);
    // Cancel whichever task has not finished.
    cts.Cancel();
    await task;

    Console.ForegroundColor = ConsoleColor.Green;
    Console.WriteLine("ncompleted successfully");
}
catch (OperationCanceledException taskCanceledException)
{
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("Cancelled: {taskCanceledException.Message}");
}
finally
{
    Console.ForegroundColor = originalColor;
}
```

```
private static async Task<int> ConsoleReadAsync(CancellationToken cancellationToken = default)
{
    return await Task.Run(async () =>
    {
        int maxDelay = 1025;
        int delay = 0;
        while (!cancellationToken.IsCancellationRequested)
        {
            if (Console.KeyAvailable)
            {
                return Console.Read();
            }
            else
            {
                await Task.Delay(delay, cancellationToken);
                if (delay < maxDelay) delay *= 2 + 1;
            }
        }
        cancellationToken.ThrowIfCancellationRequested();
        throw new InvalidOperationException(
            "Previous line should throw preventing this from ever executing");
    }, cancellationToken);
```