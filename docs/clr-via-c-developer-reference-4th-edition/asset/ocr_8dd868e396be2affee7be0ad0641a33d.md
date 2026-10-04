Each task maintains its own running total, in the localStorage variable for the files that it is given. As each task completes its work, the master total is updated in a thread-safe way by calling the Interlocked.Add method (discussed in Chapter 29, "Primitive Thread Synchronization Constructs\ Because each task has its own running total, no thread synchronization is required during the processing of the items. Because thread synchronization would hurt performance, requiring thread synchronization is costly. It is only after each task returns the masterTotal has to be updated in a thread-safe way, so the performance of calling Interlocked.Add occurs once per task instead of per work item.

You'll notice that the delegate is passed as a ParallelLoopState object, which looks like this:

```
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

```
public struct ParallelLoopResult {
    // Returns false if the operation was ended prematurely
    public Boolean IsCompleted { get; }
    public Int64? LowestIteration{ get; }
}
```