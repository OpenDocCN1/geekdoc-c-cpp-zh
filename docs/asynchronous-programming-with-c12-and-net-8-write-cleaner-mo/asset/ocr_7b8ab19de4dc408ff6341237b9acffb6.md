# 5. Task Parallelism and Performance:

The TPL allows developers to leverage the power of multi-core processors by running tasks in parallel. This can lead to improved performance in CPU-bound and parallelizable workloads.

# Parallelism Example:

```
```csharp
public class Program
{
    public static void Main()
    {
        Parallel.For(0, 10, i =>
        {
            Console.WriteLine($"Task {i} running on thread {Thread.CurrentThread.ManagedThreadId}");
            Thread.Sleep(1000); // Simulate work
        });
    }
}
```
```

In this example, `Parallel.For` is used to run multiple tasks in parallel, utilizing multiple threads for concurrent execution.