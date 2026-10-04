```
public sealed class SimpleWaitLock : IDisposable {
    private readonly Semaphore m_available;

    public SimpleWaitLock(Int32 maxConcurrent) {
        m_available = new Semaphore(maxConcurrent, maxConcurrent);
    }

    public void Enter() {
        // Block in kernel until resource available
        m_available.WaitOne();
    }

    public void Leave() {
        // Let another thread access the resource
        m_available.Release(1);
    }

    public void Dispose() { m_available.Close(); }
}
```

# # Mutex Constructs

 Mutex represents a mutual-exclusive lock. It works similar to an AutoResetEvent or a Semaphore with a count of 1 because all constructs create only one waiting thread at a time. The following shows what the Mutex looks like.

```
public sealed class Mutex : WaitHandle {
    public Mutex();
    public void ReleaseMutex();
}
```

Mutexes have some additional logic in them, which makes them more complex than the other constructs. First, Mutex objects record which by querying the calling thread's Int32 ID. When a thread calls ReleaseMutex, the Mutex makes sure that the calling thread is the same thread that obtained the Mutex. If the calling thread is not the one that obtained the Mutex, then the Mutex object's state is unstated and ReleaseMutex throws a System.Application-Exception. Also, if a thread owning a Mutex terminates for any reason, then some waiting thread on the Mutex will be awakened by having a System.Threading.AbandonedMutexException thrown. Usually, this is because a thread acquired the Mutex and it is likely that the thread terminated before finished updating the data that the Mutex was protecting. If a thread catches AbandonedMutexException, then it could attempt to access the corrupt data, leading to unpredictable results and security problems.

Second, Mutex objects maintain a recursion count indicating how many times the thread owns the Mutex. If a thread currently owns a Mutex and then that thread waits on the Mutex again, the recursion count is incremented and the thread is allowed to continue running. When that thread calls ReleaseMutex, the recursion count is decremented. Only when the recursion count becomes 0 can another thread become the owner of the Mutex.