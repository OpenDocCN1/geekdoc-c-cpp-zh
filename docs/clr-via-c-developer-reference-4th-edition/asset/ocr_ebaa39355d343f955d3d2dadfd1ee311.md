You examine the properties to determine the result of the loop. If IsCompleted returns true, then the loop to completion and all the items were processed. If IsCompleted is false and LowestBreakIteration is null, then some thread participating in the work called the Stop method. If IsCompleted is false and LowestBreakIteration is not null, then some thread-participating in the work called the break method and the Int64 value returned from LowestBreakIteration indicates the index of the lowest item guaranteed to have been processed. If an exception is thrown, you should catch an AggregateException in order to recover gracefully.

# Parallel Language Integrated Query

Microsoft's Language Integrated Query LINQ feature offers a convenient syntax for performing queries over collections of data. Using LINQ, you can easily filter items, sort items, return a projected set of items, and more. When you use LINQ to objects, only one thread processes all the items in your data collection; we call this a sequential query. You can potentially improve the performance of this by using Parallel LINQ, which can turn your query into a parallel query, which uses tasks (to the default TaskScheduler) to spread the processing of the collection's items across multiple CPUs so that multiple items are processed concurrently. For Parallel1 methods, you will get the most benefit from Parallel LINQ if you have many items to process or if the processing of each item is a lengthy compute-bound operation.

The System.Linq.ParallelEnumerable class (defined in System.Core.dll) implements all of the Parallel LINQ functionality, and you must import your source code using C# using directive. In particular, this class exposes parallel versions of all the standard LINQ operators as Where, Select, SelectMany, GroupBy, Join, OrderBy, Skip, and so on. All of these are extension methods that extend the System.Linq.ParallelQuery<T> type. To have your LINQ to objects invoke the parallel versions of these methods, you must convert your sequential query (based on IEnumerable or IEnumerable<T>) to a parallel query (based on ParallelQuery or ParallelQuery<T>) using ParallelEnumerable.AsParallel() an extension method, which looks like this.

```
public static ParallelQuery<TSource> AsParallel<TSource>(this IEnumerable<TSource> source)
public static ParallelQuery AsParallel(this IEnumerable source)
```

Here is an example of a sequential query that has been converted to a parallel query. This query returns all the methods defined within an assembly.

```
private static void ObsoleteMethods(Assembly assembly) {
var query =
    from type in assembly.GetExportedTypes().AsParallel()

from method in type.GetMethods(BindingFlags.Public |
    BindingFlags.Instance | BindingFlags.Static)
let obsoleteAttrType = typeof(ObsoleteAttribute)
```

let obsoleteAttrType = typeof(ObsoleteAttribute)

+   3 The ParallelQuery<T> class is derived from the ParallelQuery class.