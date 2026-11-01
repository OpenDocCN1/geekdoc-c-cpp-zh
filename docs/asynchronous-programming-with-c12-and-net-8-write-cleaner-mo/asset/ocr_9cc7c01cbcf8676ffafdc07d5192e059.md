While concurrent execution is beneficial, there are scenarios where limiting the number of concurrent tasks is necessary to avoid overwhelming system resources. `SemaphoreSlim` is a synchronization primitive that can be used to limit concurrent access to a resource.

# Example: Limiting Concurrent Tasks with SemaphoreSlim

```
```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    private static SemaphoreSlim semaphore = new SemaphoreSlim(2); // Limit to 2 concurrent tasks

    public static async Task Main()
    {
        Task task1 = Task.Run(() => PerformTask(1));
        Task task2 = Task.Run(() => PerformTask(2));
        Task task3 = Task.Run(() => PerformTask(3));
        Task task4 = Task.Run(() => PerformTask(4));

        await Task.WhenAll(task1, task2, task3, task4);
    }

    public static async Task PerformTask(int id)
    {
        await semaphore.WaitAsync(); // Wait until semaphore available
        try
        {
            Console.WriteLine($"Task {id} started");
            await Task.Delay(1000); // Simulate asynchronous delay
            Console.WriteLine($"Task {id} completed");
        }
    }
}
```
```