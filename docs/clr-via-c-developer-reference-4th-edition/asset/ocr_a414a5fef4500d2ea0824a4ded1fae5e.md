or you could execute them in parallel, like this.

```
// The thread pool's executes the methods in parallel
Parallel.Invoke(
    () => Method1(),
    () => Method2(),
    () => Method3());
```

All of Parallel's methods have the calling thread participate in the processing of the work, which is good in terms of resource usage because we wouldn't want the calling thread to suspend itself while waiting for thread pool threads to do all the work. However, if the calling thread finishes its work before the thread pool completes its part of the work, then the calling thread will suspend itself until all the work is done, which also gives you the same semantics as you've when using a for or foreach loop: the thread doesn't continue until all the work is done. Also, if any operation throws an unhandled exception, the Parallel method you called will ultimately throw an AggregateException.

Of course, you should not go through all your source code replacing for loops with calls to Parallel.ForEach. Each when calling the Parallel method, there is an assumption that it is OK for the items to be performed concurrently. Therefore, do not use the Parallel method if the work must be processed in sequential order. Also, avoid work items that modify any kind of shared data because the data could get corrupted if multiple threads access simultaneously. Normally, you would fix this by adding thread synchronization around the data, but if you do, then one at a time can access the data and you would lose the benefit of processing multiple items in parallel.

In addition, there is overhead associated with the Parallel methods: delegate objects have to be allocated, and these are invoked for each work item. If you have lots of work items that can be processed by multiple threads, then you might gain a performance increase. Also, if you have lots of work to do for each item, the performance hit of calling the delegate is negligible. You will actually lose your performance if you use the Parallel methods for a few work items or work items that are processed very quickly.

I should mention that Parallel's For, ForEach, and Invoke methods have all overloads that accept a ParallelOptions object, looks like this.

```
public class ParallelOptions{
    public ParallelOptions();
}
```

```
// Allows cancellation of the operation
public CancellationToken CancellationToken { get; set; } // Default=CancellationToken.None
```

```
// Allows you to specify the maximum number of work items
// that can be operated on concurrently
```

```
public Int32 DegreeOfParallelism { get; set; } // Default=-1 (of of available CPUs)
```

```
// Allows you to specify which TaskScheduler to use
```

```
public TaskScheduler TaskScheduler { get; set; } // Default=TaskScheduler.Default
}
```