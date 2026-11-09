
- The thread pool automatically scales the tasks across available CPUs.
- As each task completes a phase, the thread running that task goes back to the thread pool, where it can do other work, if any is available for it.
- The thread pool has a process-global view of tasks and, as such, it can better schedule these tasks, reducing the number of threads in the process and also reducing context switching.

Locks are popular, but when held for a long time, they introduce significant scalability issues. What would really be useful is if we had asynchronous synchronization constructs where your code indicates that it wants a lock. If the thread can't have it, it can just return and perform some other work, rather than blocking indefinitely. Then, when the lock becomes available, your code somehow gets resumed, so it can access the resource that the lock protects. I came up with this idea after trying to solve a big scalability problem for a customer, and I then sold the patent rights to Microsoft. In 2009, the Patent Office issued the patent (Patent #7,603,502).

The SemaphoreSlim class implements this idea via its WaitAsync method. Here is the signature for the most complicated overload of this method:

```csharp
public Task<Boolean> WaitAsync(Int32 millisecondsTimeout, CancellationToken cancellationToken);
```

With this, you can synchronize access to a resource asynchronously (without blocking any thread):

```csharp
private static async Task AccessResourceViaAsyncSynchronization(SemaphoreSlim asyncLock) {
    // TODO: Execute whatever code you want here...

    await asyncLock.WaitAsync();    // Request exclusive access to a resource via its lock
    // When we get here, we know that no other thread has access to the resource
    // TODO: Access the resource (exclusively)...

    // When done accessing resource, relinquish lock so other code can access the resource
    asyncLock.Release();

    // TODO: Execute whatever code you want here...
}
```

The SemaphoreSlim's WaitAsync method is very useful but, of course, it gives you semaphore semantics. Usually, you'll create the SemaphoreSlim with a maximum count of 1, which gives you mutually exclusive access to the resource that the SemaphoreSlim protects. So, this is similar to the behavior you get when using Monitor, except that SemaphoreSlim does not offer thread ownership and recursion semantics (which is good).

But, what about reader-writer semantics? Well, the .NET Framework has a class called ConcurrentExclusiveSchedulerPair which looks like this:

```csharp
public class ConcurrentExclusiveSchedulerPair {
    public ConcurrentExclusiveSchedulerPair();

    public TaskScheduler ExclusiveScheduler { get; }
    public TaskScheduler ConcurrentScheduler { get; }

    // Other methods not shown...
}
```

An instance of this class comes with two TaskScheduler objects that work together to provide reader/writer semantics when scheduling tasks. Any tasks scheduled using ExclusiveScheduler will execute one at a time, as long as no tasks are running that were scheduled using the ConcurrentScheduler. And, any tasks scheduled using the ConcurrentScheduler can all run simultaneously, as long as no tasks are running that were scheduled using the ExclusiveScheduler. Here is some code that demonstrates the use of this class:

```csharp
private static void ConcurrentExclusiveSchedulerDemo() {
    var cesp = new ConcurrentExclusiveSchedulerPair();
    var tfExclusive = new TaskFactory(cesp.ExclusiveScheduler);
    var tfConcurrent = new TaskFactory(cesp.ConcurrentScheduler);

    for (Int32 operation = 0; operation < 5; operation++) {
        var exclusive = operation < 2; // For demo, I make 2 exclusive & 3 concurrent

        (exclusive ? tfExclusive : tfConcurrent).StartNew(() => {
            Console.WriteLine("{0} access", exclusive ? "exclusive" : "concurrent");
            // TODO: Do exclusive write or concurrent read computation here...
        });
    }
}
```

Unfortunately, the .NET Framework doesn't come with an asynchronous lock offering reader-writer semantics. However, I have built such a class, which I call AsyncOneManyLock. You use it the same way that you'd use a SemaphoreSlim. Here is an example:

```csharp
private static async Task AccessResourceViaAsyncSynchronization(AsyncOneManyLock asyncLock) {
    // TODO: Execute whatever code you want here...

    // Pass OneManyMode.Exclusive or OneManyMode.Shared depending on the concurrent access you need
    await asyncLock.AcquireAsync(OneManyMode.Shared); // Request shared access
    // When we get here, no threads are writing to the resource; other threads may be reading
    // TODO: Read from the resource...

    // When done accessing resource, relinquish lock so other code can access the resource
    asyncLock.Release();

    // TODO: Execute whatever code you want here...
}
```

The code for my AsyncOneManyLock is shown below:

```csharp
public enum OneManyMode { Exclusive, Shared }

public sealed class AsyncOneManyLock {
    #region Lock code
    private SpinLock m_lock = new SpinLock(true);   // Don't use readonly with a SpinLock
    private void Lock() { Boolean taken = false; m_lock.Enter(ref taken); }
    private void Unlock() { m_lock.Exit(); }
    #endregion
}
```

```csharp
    }
        Unlock();

        return accessGranter;
    }

    public void Release() {
        TaskCompletionSource<Object> accessGranter = null;   // Assume no code is released

        Lock();
        if (!sOwnedByWriter) MakeFree(); // The writer left
        else SubtractReader();           // A reader left

        if (!sFree) {
            // If free, wake 1 waiting writer or all waiting readers
            if (m_waitingWriters.Count > 0) {
                MakeWriter();
                accessGranter = m_waitingWriters.Dequeue();
            } else if (m_numWaitingReaders > 0) {
                AddReaders(m_numWaitingReaders);
                m_numWaitingReaders = 0;
                accessGranter = m_waitingReadersSignal;

                // Create a new TCS for future readers that need to wait
                m_waitingReadersSignal = new TaskCompletionSource<Object>();
            }
        }
        Unlock();

        // Wake the writer/reader outside the lock to reduce
        // chance of contention improving performance
        if (accessGranter != null) accessGranter.SetResult(null);
    }
```

As I said, this code never blocks a thread. The reason is because it doesn't use any kernel constructs internally. Now, it does use a SpinLock that internally uses user-mode constructs. But, if you recall from the discussion about SpinLocks in Chapter 29, a SpinLock can only be used when held over sections of code that are guaranteed to execute in a short and finite amount of time. If you examine my WaitAsync method, you'll notice that all I do while holding the lock is some integer calculations and comparison and perhaps construct a TaskCompletionSource and add it to a queue. This can't take very long at all, so the lock is guaranteed to be held for a very short period of time.

Similarly, if you examine my Release method, you'll notice that all I do is some integer calculations, a comparison and perhaps dequeue a TaskCompletionSource or possibly construct a TaskCompletionSource. Again, this can't take very long either. The end result is that I feel very comfortable using a SpinLock to guard access to the Queue. Therefore, threads never block when using this lock, which allows me to build responsive and scalable software.

## The Concurrent Collection Classes

The FCL ships with four thread-safe collection classes, all of which are in the System.Collections.Concurrent namespace: ConcurrentQueue, ConcurrentStack, ConcurrentDictionary, and ConcurrentBag. Here is what some of their most commonly used members look like:

```csharp
// Process items in a first-in, first-out order (FIFO)
public class ConcurrentQueue<T> : IProducerConsumerCollection<T>,
    IEnumerable<T>, ICollection, IEnumerable {

    public ConcurrentQueue();
    public void Enqueue(T item);
    public Boolean TryDequeue(out T result);
    public Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// Process items in a last-in, first-out order (LIFO)
public class ConcurrentStack<T> : IProducerConsumerCollection<T>,
    IEnumerable<T>, ICollection, IEnumerable {

    public ConcurrentStack();
    public void Push(T item);
    public Boolean TryPop(out T result);
    public Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// An unordered set of items where duplicates are allowed
public class ConcurrentBag<T> : IProducerConsumerCollection<T>,
    IEnumerable<T>, ICollection, IEnumerable {

    public ConcurrentBag();
    public void Add(T item);
    public Boolean TryTake(out T result);
    public Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// An unordered set of key/value pairs
public class ConcurrentDictionary<TKey, TValue> : IDictionary<TKey, TValue>,
    ICollection<KeyValuePair<TKey, TValue>>, IEnumerable<KeyValuePair<TKey, TValue>>,
    IDictionary, ICollection, IEnumerable {

    public ConcurrentDictionary();
    public Boolean TryAdd(TKey key, TValue value);
    public Boolean TryGetValue(TKey key, out TValue value);
    public TValue this[TKey key] { get; set; }
    public Boolean TryUpdate(TKey key, TValue newValue, TValue comparisonValue);
    public Boolean TryRemove(TKey key, out TValue value);
    public TValue AddOrUpdate(TKey key, TValue addValue,
```
