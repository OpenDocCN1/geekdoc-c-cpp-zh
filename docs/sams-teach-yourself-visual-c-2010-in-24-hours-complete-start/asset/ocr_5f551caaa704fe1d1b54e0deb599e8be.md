| Class | Description |
|---|---|
| OrderablePartitioner<TSource> | Represents a particular manner of splitting an orderable data source into multiple partitions |
| Partitioner | Provides common partitioning strategies for arrays, list, and enumerables |
| Partitioner<TSource> | Represents a particular manner of splitting a data source into multiple partitions |

# Task Parallelism

You can think of a task as representing an asynchronous operation. You can easily create and run implicit tasks using the `Parallel.Invoke` method, which enables you to run any number of arbitrary statements concurrently, as shown here:

```
`Parallel.Invoke(() => DoSomeWork(), () => DoSomeOtherWork());`
```

`Parallel.Invoke` accepts an array of `Action` delegates, each representing a single task to perform. The simplest way to create the delegates is to use lambda expressions.

As Listing 23.3 shows, you can also explicitly create and run a task by instantiating the `Task` or `Task<TResult>` class and passing the delegate that encapsulates the code the task executes.

```
**LISTING 23.3 Explicitly Creating New Tasks**
```csharp
class Program
{
    public static void Main(string[] args)
    {
        var task = new Task(() => Console.WriteLine("Hello from a task."));
        task.Start();
        Console.WriteLine("Hello from the calling thread.");
    }
}
```
```

![](bbox=[0.04, 0.78, 0.78, 0.83])

![](bbox=[0.04, 0.77, 0.74, 0.88])

If the task creation and scheduling do not need to be separated, the preferred method is to use the `Task.Factory.StartNew` method, as shown in Listing 23.4.