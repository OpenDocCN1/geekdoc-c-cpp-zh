```
Task<int> task3 = Task.Run(() =>
DelayedOperation(3, 1000));

// Await the completion of the first group of tasks
among task1, task2, and task3

Task<int>[] firstGroupTasks = { task1, task2, task3 };

Task<int>[] completedTasks = await
Task.WhenAny(Task.WhenAll(firstGroupTasks),
Task.WhenAny(firstGroupTasks));

Console.WriteLine("First group of tasks completed:");

foreach (var completedTask in completedTasks)
{
    Console.WriteLine("Completed Task Result: " +
completedTask.Result);
}
}

public static int DelayedOperation(int id, int delay)
{
    Task.Delay(delay).Wait(); // Simulate delay
    return id;
}
}
```
```