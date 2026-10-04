As mentioned before, Parallel LINQ has multiple threads processing items, and then the results must be merged back together. You can control how the items are buffered and merged by calling WithMergeOptions, passing one of the ParallelMergeOptions flags.

```
public enum ParallelMergeOptions {
    Default = 0, // As AutoBuffered today (could change in the future)
    NotBuffered = 1, // Results are processed as ready
    AutoBuffered = 2, // Each thread buffers some results before processed
    FullyBuffered = 3 // Each thread buffers all results before processed
}
```

These options basically give you some control over versus memory consumption. FullyBuffered saves memory but consumes more while running fastest. AutoBuffered is the compromise between NotBuffered and FullyBuffered. Really, the best way to know which of these to choose for any given query is to try them all and compare their performance results, or just accept the default, which works quite well for many queries. See the following blog posts for more information about how Parallel LINQ partitions work cores.

+   * http://blogs.msn.com/pfxtream/archive/2009/05/28/9648672.aspx
* http://blogs.msn.com/pfxtream/archive/2009/06/13/9741072.aspx

# Performing a Periodic Compute-Bound Operation

The System.Threading namespace defines a Timer class, which you can use to have a thread pool call periodically. When you construct an instance of the Timer class, you are telling the thread pool that you want a method of yours called back at a future time that you specify. The Timer class offers several constructors, all similar to each other.

```
public sealed class Timer : MarshalObject, IDisposable {
    public Timer(TimerCallback callback, Object state, Int32 dueTime, Int32 period);
    public Timer(TimerCallback callback, Object state, UInt32 dueTime, UInt32 period);
    public Timer(TimerCallback callback, Object state, Int64 dueTime, Int64 period);
    public Timer(TimerCallback callback, Object state, TimeSpan dueTime, TimeSpan period);
}
```

All four constructors construct a Timer object identically. The callback parameter identifies the method that you want to called back by a thread pool. Of course, the callback method that you write must match the System.Threading.TimerCallback delegate type, which is defined as follows.

```
delegate void TimerCallback(Object state);
```