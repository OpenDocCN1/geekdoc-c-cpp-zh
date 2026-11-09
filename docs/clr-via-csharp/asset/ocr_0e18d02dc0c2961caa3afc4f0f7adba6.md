```
```csharp
public sealed class SimpleWaitLock : IDisposable {
    private Semaphore m_AvailableResources;

    public SimpleWaitLock(Int32 maximumConcurrentThreads) {
        m_AvailableResources =
            new Semaphore(maximumConcurrentThreads, maximumConcurrentThreads);
    }

    public void Enter() {
        // Wait efficiently in the kernel for resource access, then return
        m_AvailableResources.WaitOne();
    }

    public void Leave() {
        // This thread doesn't need access anymore; another thread can have it
        m_AvailableResources.Release();
    }

    public void Dispose() { m_AvailableResources.Close(); }
}
```
```

# ## Mutex Constructs

A mutex represents a mutual-exclusive lock. It works similar to an **AutoResetEvent** (or a **Semaphore** with a count of 1) since all three constructs release only one waiting thread at a time. Here is what the **Mutex** class looks like:

```
```csharp
public sealed class Mutex : WaitHandle {
    public Mutex();
    public void ReleaseMutex();
}
```
```

**Mutexes** have some additional logic in them which makes them more complex than the other constructs. First, **Mutex** objects record which thread obtained it by querying the calling thread's **Int32 ID**. When a thread calls **ReleaseMutex**, the **Mutex** makes sure that the calling thread is the same thread that obtained the **Mutex**. If the calling thread is not the thread that obtained the **Mutex**, then the **Mutex** object's state is unaltered and **ReleaseMutex** throws a **System.ApplicationException**. Also, if a thread owning a **Mutex** terminates for any reason, then some thread waiting on the **Mutex** will be awakened by having a **System.Threading.AbandonedMutexException** thrown. Usually, this exception will go unhandled, terminating the whole process. This is good because a thread acquired the **Mutex** and it is likely that the thread terminated before it finished updating the data that the **Mutex** was protecting. If a thread catches **AbandonedMutexException**, then it could attempt to access the corrupt data, leading to unpredictable results and security problems.

Second, **Mutex** objects maintain a recursion count indicating how many times the owning thread owns the **Mutex**. If a thread currently owns a **Mutex** and then that thread waits on the **Mutex** again, the recursion count is incremented and the thread is allowed to continue running. When that thread calls **ReleaseMutex**, the recursion count is decremented. Only when the recursion count becomes 0 can another thread become the owner of the **Mutex**.