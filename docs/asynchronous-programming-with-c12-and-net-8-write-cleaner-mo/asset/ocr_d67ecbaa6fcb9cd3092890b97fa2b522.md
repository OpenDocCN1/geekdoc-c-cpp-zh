```
await Task.WhenAll(task1, task2, task3);
Console.WriteLine("All tasks completed:");
Console.WriteLine("Task 1 Result: " + task1.Result);
Console.WriteLine("Task 2 Result: " + task2.Result);
Console.WriteLine("Task 3 Result: " + task3.Result);
}
public static async Task<int> Task1()
{
    await Task.Delay(1000); // Simulate asynchronous
delay
    return 10;
}
public static async Task<int> Task2()
{
    await Task.Delay(1500); // Simulate asynchronous
delay
    return 20;
}
public static async Task<int> Task3()
{
    await Task.Delay(2000); // Simulate asynchronous
delay
    return 30;
}
}

```

In this example, `Task.WhenAll` is used to execute `Task1`, `Task2`, and `Task3` concurrently, and then await their completion. This approach maximizes CPU utilization by allowing tasks to run in parallel.

# 2. Limiting Concurrent Tasks with SemaphoreSlim: