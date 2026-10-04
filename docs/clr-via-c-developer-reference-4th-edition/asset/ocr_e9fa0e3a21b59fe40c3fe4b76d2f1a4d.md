```
if (m_waitingWriters.Count > 0) {
    MakeWriter();
    accessGranter = m_waitingWriters.Dequeue();
} else if (m_numwaitingReaders > 0) {
    AddReaders(m_numwaitingReaders);
    m_numwaitingReaders = 0;
    accessGranter = m_waitingReadersSignal;
}

// Create a TCS for future readers that need to wait
m_waitingReadersSignal = new TaskCompletionSource<Object>();
}
Unlock();
```

// Wake the writer/reader outside the lock to reduce
// chance of contention improving performance
if (accessGranter != null) accessGranter.SetResult(null);

As I said, this code never blocks a thread. The reason is that it doesn't use user-structs internally. Now, it uses a SpinLock that internally uses user-mode constructs. But, if you recall the discussion about SpinLocks in Chapter 29, a SpinLock can only be used when over sections of code that are guaranteed to execute in short and finite time. If you examine my Async you'll notice that all I do while holding the lock is some integer calculations and perhaps construct a TaskCompletionSource and add it to a queue. This can't take very long, so the lock is guaranteed to be held for a very short period of time.

Similarly, if you examine my Release method, you'll notice that all I do is some integer calculations, a comparison and perhaps dequeue a TaskCompletionSource or possibly construct a Task-CompletionSource. Again, this can't take very long either. The result is that I feel comfortable using a SpinLock to guard access to the Queue. Therefore, threads never block when using this lock, which allows me to build responsive and scalable software.

# The Concurrent Collection Classes

The FCL ships with four thread-safe collection classes, all of which are in the System.Collections namespace: ConcurrentQueue, ConcurrentStack, ConcurrentDictionary, and ConcurrentBag. Here is what some of their most commonly used members look like.

```
// Process items in a first-in, first-out order (FIFO)
public class ConcurrentQueue<T> : IProducerConsumerCollection<T>, 
IEnumerable<T>, ICollection, Iumerable {

    public ConcurrentQueue();
    public bool void Enqueue(T item);
    public boolean TryDequeue(out T result);
    public Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}
```