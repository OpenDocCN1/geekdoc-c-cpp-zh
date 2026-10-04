
In addition, there are overloads of the For and Each methods that let pass three delegates:

- The local initialization delegate (localInit) is invoked once for each task participating in the work. This delegate is invoked before the task is asked to process a work item.

- The body delegate (body) is invoked once for each task being processed by the various threads participating in the work.

- The local finally delegate (localFinally) is invoked once for each task participating in work. This delegate is invoked after the task has processed all the work items that will be dispatched to it. It is even invoked if the body delegate code experiences an unhandled exception.

Here is some sample code that demonstrates the use of the three delegates by adding up the for files contained within a directory.

```c
private static Int64 DirectoryBytes(String path, String searchPattern, SearchOption searchOption) {
 var files = Directory.EnumerateFiles(path, searchPattern, searchOption);
Int64 masterTotal = 0;

ParallelLoopResult result = Parallel.ForEach<String, Int64>(
files,
() => // localInit: Invoked once per task at start
 // Initialize that this task has seen 0 bytes
 return 0; // Set localTotal initial value to 0
},

(file, loopState, index, taskTotal) => { // body: Invoked once per work item
 // Get this file's size and add it to this task's running total
Int64 contentLength = 0;
FileStream fs = null;
try {
 fs = File.OpenRead(file);
 contentLength = fs.Length;
 } catch (IOException exception) { /* Ignore any files we can't access */ }
 finally { if (fs != null) fs.Dispose(); }
 return taskLocalTotal + contentLength;
},

taskLocalTotal => { // localFinally: Invoked once per task at end
 // Atomically add this task's total to the "master" total
Interlocked.Add(ref masterTotal, taskTotal);
});

return masterTotal;
```

Each task maintains its own running total, in the localStorage variable for the files that it is given. As each task completes its work, the master total is updated in a thread-safe way by calling the Interlocked.Add method (discussed in Chapter 29, "Primitive Thread Synchronization Constructs"). Because each task has its own running total, no thread synchronization is required during the processing of the items. Because thread synchronization would hurt performance, requiring thread synchronization is costly. It is only after each task returns the masterTotal has to be updated in a thread-safe way, so the performance of calling Interlocked.Add occurs once per task instead of per work item.

You'll notice that the delegate is passed as a ParallelLoopState object, which looks like this:

```csharp
public class ParallelLoopState{
    public void Stop();
    public Boolean IsStopped { get; }

    public void Break();
    public Int64? LowestIteration{ get; }

    public Boolean IsExceptional { get; }
    public Boolean ShouldExitCurrentIteration { get; }
}
```

Each task participating in the work gets its own ParallelLoopState object, and it can use this object to interact with the other task participating in the work. The Stop method tells the loop to stop processing any more work, and further querying of the IsStopped property will return true. The Break method tells the loop to stop processing any items that are beyond the current item. For example, let's say that ForEach is told to process 100 items and Break is called while processing the fifth item, then the loop will make that the first five items are processed before ForEach returns. Note, however, that additional items may have been processed. The LowestIteration property returns the lowest item while processing the Break method. The LowestIteration property returns null if Break was never called.

The IsException property returns true if the processing of an item takes a long time, your code can query the ShouldExitCurrentIteration property to see if it should exit prematurely. This property returns true if Stop was called, Break called, the CancellationSource (referred to by the CancellationToken property) is canceled, or if the processing of an item resulted in an unhandled exception.

ParallelLoop's and ForEach both return a ParallelLoopResult instance, which looks like this:

```csharp
public struct ParallelLoopResult {
    // Returns false if the operation was ended prematurely
    public Boolean IsCompleted { get; }
    public Int64? LowestIteration{ get; }
}
```

You examine the properties to determine the result of the loop. If IsCompleted returns true, then the loop to completion and all the items were processed. If IsCompleted is false and LowestBreakIteration is null, then some thread participating in the work called the Stop method. If IsCompleted is false and LowestBreakIteration is not null, then some thread-participating in the work called the break method and the Int64 value returned from LowestBreakIteration indicates the index of the lowest item guaranteed to have been processed. If an exception is thrown, you should catch an AggregateException in order to recover gracefully.

# Parallel Language Integrated Query

Microsoft's Language Integrated Query LINQ feature offers a convenient syntax for performing queries over collections of data. Using LINQ, you can easily filter items, sort items, return a projected set of items, and more. When you use LINQ to objects, only one thread processes all the items in your data collection; we call this a sequential query. You can potentially improve the performance of this by using Parallel LINQ, which can turn your query into a parallel query, which uses tasks (to the default TaskScheduler) to spread the processing of the collection's items across multiple CPUs so that multiple items are processed concurrently. For Parallel methods, you will get the most benefit from Parallel LINQ if you have many items to process or if the processing of each item is a lengthy compute-bound operation.

The System.Linq.ParallelEnumerable class (defined in System.Core.dll) implements all of the Parallel LINQ functionality, and you must import your source code using C# using directive. In particular, this class exposes parallel versions of all the standard LINQ operators as Where, Select, SelectMany, GroupBy, Join, OrderBy, Skip, and so on. All of these are extension methods that extend the System.Linq.ParallelQuery<T> type. To have your LINQ to objects invoke the parallel versions of these methods, you must convert your sequential query (based on IEnumerable or IEnumerable<T>) to a parallel query (based on ParallelQuery or ParallelQuery<T>) using ParallelEnumerable.AsParallel() an extension method, which looks like this.

```csharp
public static ParallelQuery<TSource> AsParallel<TSource>(this IEnumerable<TSource> source)
public static ParallelQuery AsParallel(this IEnumerable source)
```

Here is an example of a sequential query that has been converted to a parallel query. This query returns all the methods within an assembly.

```csharp
private static void ObsoleteMethods(Assembly assembly) {
var query = from type in assembly.GetExportedTypes().AsParallel()
from method in type.GetMethods(BindingFlags.Public | BindingFlags.Instance | BindingFlags.Static)
where Attribute.IsDefined(method, typeof(ObsoleteAttribute))
let obsoleteObj = (ObsoleteAttribute)Attribute.GetCustomAttribute(method, typeof(ObsoleteAttribute))
select String.Format("Type={0}\nMessage={1}\n", type.FullName, obsoleteObj.Message);

// Display the results
foreach (var result in query) Console.WriteLine(result);
}
```

Although uncommon, within a query you can switch from parallel operations back to performing operations by calling ParallelEnumerable.AsSequential method.

```csharp
public static IEnumerable<TSource> AsSequential<TSource>(this ParallelQuery<TSource> source)
```

This method basically runs a ParallelQuery<T> back to an Enumerable<T> so that operations performed after AsSequential are performed by one thread.

Normally, the result data produced by a LINQ query is evaluated by having some thread execute a forecast (as shown earlier). This means that one thread iterates over the query's results. If you want to have the query's results processed in parallel, then you should process the query by using ParallelEnumerable.ForEach method.

```csharp
static void ForAll<TSource>(this ParallelQuery<TSource> source, Action<TSource> action)
```

This method allows multiple threads to process the results simultaneously. I could modify my code earlier to use this method as follows.

```csharp
// Display the results
query.ForAll(Console.WriteLine);
```

However, having multiple threads call Console.WriteLine simultaneously actually hurts performance, because the Console class internally synchronizes threads, ensuring that only one at a time can access the console window. This prevents multiple threads from being interspersed, making the output unintelligible. For the All method when you intend to perform calculations on each result.

Because Parallel LINQ processes items using multiple threads, the items are processed currently and the results are returned in an unordered fashion. If you need to have Parallel LINQ preserve the order of items as they are processed, then you can call ParallelEnumerable.AsOrdered method. When you call this method, threads process items in groups and then the groups are merged back together, preserving the order; this will hurt performance. The following operators produce unordered operations: Distinct, Except, Intersect, Union, Join, GroupBy,
