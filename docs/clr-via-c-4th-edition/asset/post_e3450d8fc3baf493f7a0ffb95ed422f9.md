
or you could execute them in parallel, like this.

```
// The thread pool's threads execute the methods in parallel
Parallel.Invoke(
    () => Method1(),
    () => Method2(),
    () => Method3());
```

All of Parallel's methods have the calling thread participate in the processing of the work, which is good in terms of resource usage because we wouldn't want the calling thread to just suspend itself while waiting for thread pool threads to do all the work. However, if the calling thread finishes its work before the thread pool threads complete their part of the work, then the calling thread will suspend itself until all the work is done, which is also good because this gives you the same semantics as you'd have when using a for or foreach loop: the thread doesn't continue running until all the work is done. Also note that if any operation throws an unhandled exception, the Parallel method you called will ultimately throw an AggregateException.

Of course, you should not go through all your source code replacing for loops with calls to Parallel.For and foreach loops with calls to Parallel.ForEach. When calling the Parallel method, there is an assumption that it is OK for the work items to be performed concurrently. Therefore, do not use the Parallel methods if the work must be processed in sequential order. Also, avoid work items that modify any kind of shared data because the data could get corrupted if it is manipulated by multiple threads simultaneously. Normally, you would fix this by adding thread synchronization locks around the data access, but if you do this, then one thread at a time can access the data and you would lose the benefit of processing multiple items in parallel.

In addition, there is overhead associated with the Parallel methods; delegate objects have to be allocated, and these delegates are invoked once for each work item. If you have lots of work items that can be processed by multiple threads, then you might gain a performance increase. Also, if you have lots of work to do for each item, then the performance hit of calling through the delegate is negligible. You will actually hurt your performance if you use the Parallel methods for just a few work items or for work items that are processed very quickly.

I should mention that Parallel's For, ForEach, and Invoke methods all have overloads that accept a ParallelOptions object, which looks like this.

```
public class ParallelOptions{
    public ParallelOptions();

    // Allows cancellation of the operation
    public CancellationToken CancellationToken { get; set; }   // Default=CancellationToken.None

    // Allows you to specify the maximum number of work items
    // that can be operated on concurrently
    public Int32 MaxDegreeOfParallelism { get; set; }          // Default=-1 (# of available CPUs)

    // Allows you to specify which TaskScheduler to use
    public TaskScheduler TaskScheduler { get; set; }           // Default=TaskScheduler.Default
}
```

In addition, there are overloads of the For and ForEach methods that let you pass three delegates:

- The task local initialization delegate (localInit) is invoked once for each task participating in the work. This delegate is invoked before the task is asked to process a work item.
- The body delegate (body) is invoked once for each item being processed by the various threads participating in the work.
- The task local finally delegate (localFinally) is invoked once for each task participating in the work. This delegate is invoked after the task has processed all the work items that will be dispatched to it. It is even invoked if the body delegate code experiences an unhandled exception.

Here is some sample code that demonstrates the use of the three delegates by adding up the bytes for all files contained within a directory.

```csharp
private static Int64 DirectoryBytes(String path, String searchPattern,
    SearchOption searchOption) {
    var files = Directory.EnumerateFiles(path, searchPattern, searchOption);
    Int64 masterTotal = 0;

    ParallelLoopResult result = Parallel.ForEach<String, Int64>(
        files,

        () => { // localInit: Invoked once per task at start
            // Initialize that this task has seen 0 bytes
            return 0;   // Set taskLocalTotal initial value to 0
        },

        (file, loopState, index, taskLocalTotal) => { // body: Invoked once per work item
            // Get this file's size and add it to this task's running total
            Int64 fileLength = 0;
            FileStream fs = null;
            try {
                fs = File.OpenRead(file);
                fileLength = fs.Length;
            }
            catch (IOException) { /* Ignore any files we can't access */ }
            finally { if (fs != null) fs.Dispose(); }
            return taskLocalTotal + fileLength;
        },

        taskLocalTotal => { // localFinally: Invoked once per task at end
            // Atomically add this task's total to the "master" total
            Interlocked.Add(ref masterTotal, taskLocalTotal);
        });
    return masterTotal;
}
```

You can examine the properties to determine the result of the loop. If IsCompleted returns true, then the loop ran to completion and all the items were processed. If IsCompleted is false and LowestBreakIteration is null, then some thread participating in the work called the Stop method. If IsCompleted is false and LowestBreakIteration is not null, then some thread participating in the work called the Break method and the Int64 value returned from LowestBreakIteration indicates the index of the lowest item guaranteed to have been processed. If an exception is thrown, then you should catch an AggregateException in order to recover gracefully.

## Parallel Language Integrated Query

Microsoft’s Language Integrated Query (LINQ) feature offers a convenient syntax for performing queries over collections of data. Using LINQ, you can easily filter items, sort items, return a projected set of items, and much more. When you use LINQ to Objects, only one thread processes all the items in your data collection sequentially; we call this a sequential query. You can potentially improve the performance of this processing by using Parallel LINQ, which can turn your sequential query into a parallel query, which internally uses tasks (queued to the default TaskScheduler) to spread the processing of the collection’s items across multiple CPUs so that multiple items are processed concurrently. Like Parallel’s methods, you will get the most benefit from Parallel LINQ if you have many items to process or if the processing of each item is a lengthy compute-bound operation.

The static System.Linq.ParallelEnumerable class (defined in System.Core.dll) implements all of the Parallel LINQ functionality, and so you must import the System.Linq namespace into your source code via C#’s using directive. In particular, this class exposes parallel versions of all the standard LINQ operators such as Where, Select, SelectMany, GroupBy, Join, OrderBy, Skip, Take, and so on. All of these methods are extension methods that extend the System.Linq.ParallelQuery<T> type. To have your LINQ to Objects query invoke the parallel versions of these methods, you must convert your sequential query (based on IEnumerable or IEnumerable<T>) to a parallel query (based on ParallelQuery or ParallelQuery<T>) using ParallelEnumerable’s AsParallel extension method, which looks like this.<sup>3</sup>

```csharp
public static ParallelQuery<TSource> AsParallel<TSource>(this IEnumerable<TSource> source)
public static ParallelQuery       AsParallel(this IEnumerable source)
```

Here is an example of a sequential query that has been converted to a parallel query. This query returns all the obsolete methods defined within an assembly.

```csharp
private static void ObsoleteMethods(Assembly assembly) {
    var query =
        from type in assembly.GetExportedTypes().AsParallel()

        from method in type.GetMethods(BindingFlags.Public |
            BindingFlags.Instance | BindingFlags.Static)

        let obsoleteAttrType = typeof(ObsoleteAttribute)
```
