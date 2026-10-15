
run at the same time) via the ParallelOptions parameter on overloads of both the Parallel.For() and Parallel.ForEach<T>() loops. In some specific cases, the developer may know more about the particular algorithm or circumstance such that changing the maximum degree of parallelism makes sense. These circumstances include the following:

- Scenarios where you want to disable parallelism to make debugging or analysis easier. Setting the maximum degree of parallelism to 1 ensures that the loop iterations do not run concurrently.
- Scenarios where you know ahead of time that the degree of parallelism will be gated on an external factor such as a hardware constraint. For example, if your parallel operation involves using multiple USB ports, it is possible that there is no point in creating more threads than there are available ports.
- Scenarios with really long-running loop iterations (for example, minutes or hours). The thread pool can’t distinguish long-running iterations from blocked operations, so it could end up introducing many new threads, all of which will be consumed by the for loop. This can result in incremental thread growth over time, resulting in a huge number of threads in the process.

And so on. To control the maximum degree of parallelism, use the MaxDegreeOfParallelism property on the ParallelOptions object.

You can also use the ParallelOptions object’s TaskScheduler property to specify a custom task scheduler to use to schedule the tasks associated with each iteration. For example, you might have an asynchronous event handler that responds to the user’s click of a “Next” button. If the user clicks the button several times, you might want to use a custom task scheduler that prioritizes the most recently created task, rather than prioritizing the task that has waited the longest. The task scheduler provides a means of specifying how the tasks will execute in relation to one another.

The ParallelOptions object also has a CancellationToken property that provides a mechanism to communicate to the loop that no further iterations should start. Additionally, the body of an iteration can watch the cancellation token to determine if an early exit from the iteration is in order.

## ADVANCED TOPIC

## Breaking a Parallel Loop

Like a standard for loop, the Parallel.For() loop supports the concept of “breaking” to exit the loop and canceling any further iterations. In the context of parallel for execution, however, a break signifies that no new iterations following the breaking iteration should start. All currently executing iterations, however, will run to completion.

To break a parallel loop, you can provide a cancellation token and cancel it on another thread, as described in the preceding Advanced Topic. You can also use an overload of the Parallel.For() method whose body delegate takes two parameters: the index, and a ParallelLoopState object. An iteration that wishes to “break” the loop can call the Break() or Stop() method on the loop state object passed to the delegate. The Break() method indicates that no more iterations with index values higher than the current value need to execute; the Stop() method indicates that no more iterations need to run at all.

For example, suppose you have a Parallel.For() loop that is performing ten iterations in parallel. Some of those iterations might run faster than others, and the task scheduler does not guarantee that they will run in any particular order. Suppose the first iteration has completed; iterations 3, 5, 7, and 9 are “in flight,” scheduled to four different threads; and iterations 5 and 7 both call Break(). In this scenario, iterations 6 and 8 will never start, but iterations 2 and 4 will still be scheduled to run. Iterations 3 and 9 will run to completion because they were already started when the break happened.

The Parallel.For() and Parallel.ForEach<T>() methods return a reference to a ParallelLoopResult object that contains useful information about what happened during the loop. This result object has the following properties:

- IsCompleted returns a Boolean indicating whether all iterations started.
- LowestBreakIteration identifies the lowest iteration that executed a break. The value is of type long?, where a value of null indicates no break statement was encountered.

Returning to the ten-iteration example, the IsCompleted property will return false and the LowestBreakIteration will return a value of 5.

As Listing 18.30 shows, the change to enable parallel support is extremely small! All that it uses is a .NET Framework 4.0–introduced standard query operator, AsParallel(), which can be found on the static class System.Linq.ParallelEnumerable. This simple extension method tells the runtime that it can execute the query in parallel. The result is that on machines with multiple available CPUs, the total time taken to execute the query can be significantly shorter.

System.Linq.ParallelEnumerable includes a superset of the query operators available on System.Linq.Enumerable, resulting in possible performance improvements for all of the common query operators, including those used for sorting, filtering (Where()), projecting (Select()), joining, grouping, and aggregating. Listing 18.31 shows how to do a parallel sort.

### LISTING 18.31: Parallel LINQ with Standard Query Operators

```
// ...
OrderedParallelQuery<string> parallelGroups =
    data.AsParallel().OrderBy(item => item);

// Show the total count of items still
// matches the original count
System.Diagnostics.Trace.Assert(
    data.Count == parallelGroups.Sum(
        item => item.Count()));
// ...
```

As Listing 18.31 shows, invoking the parallel version simply involves a call to the AsParallel() extension method. Notice that the type of the result returned by the parallel standard query operators is either ParallelQuery<T> or OrderedParallelQuery<T>; both inform the compiler that it should continue to use the parallel versions of the standard query operations that are available.

Given that query expressions are simply a syntactic sugar for the method call form of the query used in Listings 18.30 and 18.31, you can just as easily use AsParallel() with the expression form. Listing 18.32 shows an example of executing a grouping operation in parallel using query expression syntax.

### LISTING 18.32: Parallel LINQ with Query Expressions

```
// ...
ParallelQuery<IGrouping<char, string>> parallelGroups;
parallelGroups =
    from text in data.AsParallel()
    orderby text
    group text by text[0];
```

```
// Show the total count of items still
// matches the original count
System.Diagnostics.Trace.Assert(
    data.Count == parallelGroups.Sum(
        item => item.Count()));
// ...
```

As you saw in the previous examples, converting a query or iteration loop to execute in parallel is simple. There is one significant caveat, however: As we will discuss in depth in Chapter 19, you must take care not to allow multiple threads to inappropriately access and modify the same memory simultaneously. Doing so will cause a race condition.

As we saw earlier in this chapter, the Parallel.For() and Parallel.ForEach<T>() methods will gather up any exceptions thrown during the parallel iterations and then throw one aggregating exception containing all of the original exceptions. PLINQ operations are no different. That is, they also have the potential of returning multiple exceptions for the exact same reason: When the query logic is run on each element in parallel, the code executing on each element can independently throw an exception. Unsurprisingly, PLINQ deals with this situation in exactly the same way as do parallel loops and the TPL: Exceptions thrown during parallel queries are accessible via the InnerExceptions property of the AggregateException. Therefore, wrapping a PLINQ query in a try/catch block with the exception type of System.AggregateException will successfully handle any exceptions within each iteration that were unhandled.

## Canceling a PLINQ Query

As expected, the cancellation request pattern is also available on PLINQ queries. Listing 18.33 (with Output 18.10) provides an example. Like the parallel loops, canceled PLINQ queries will throw a System.OperationCanceledException. Also like the parallel loops, executing a PLINQ query is a synchronous operation on the invoking thread. Thus, a common technique is to wrap the parallel query in a task that runs on another thread so that the current thread can cancel it if necessary—the same solution used in Listing 18.28.

### LISTING 18.33: Canceling a PLINQ Query

```
using System;
using System.Collections.Generic;
using System.Linq;
```
