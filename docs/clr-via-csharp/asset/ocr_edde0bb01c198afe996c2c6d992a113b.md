# # A Simple Hybrid Lock

So, without further ado, let me start off by showing you an example of a hybrid thread synchronization lock:

```
~~~csharp
internal sealed class SimpleHybridLock : IDisposable {
    // The Int32 is used by the primitive user-mode constructs (Interlocked methods)
    private Int32 m_waiters = 0;

    // The AutoResetEvent is the primitive kernel-mode construct
    private AutoResetEvent m_waiterLock = new AutoResetEvent(false);

    public void Enter() {
        // Indicate that this thread wants the lock
        if (Interlocked.Increment(ref m_waiters) == 1)
            return; // Lock was free, no contention, just return

        // Another thread is waiting. There is contention, block this thread
        m_waiterLock.WaitOne(); // Bad performance hit here
        // When WaitOne returns, this thread now has the lock
    }

    public void Leave() {
        // This thread is releasing the lock
        if (Interlocked.Decrement(ref m_waiters) == 0)
            return; // No other threads are blocked, just return

        // Other threads are blocked, wake 1 of them
        m_waiterLock.Set(); // Bad performance hit here
    }

    public void Dispose() { m_waiterLock.Dispose(); }
}
~~~
```

The **SimpleHybridLock** contains two fields: an **Int32**, which will be manipulated via the primitive user-mode constructs, and an **AutoResetEvent**, which is a primitive kernel-mode construct. To get great performance, the lock tries to use the **Int32** and avoid using the **AutoResetEvent** as much as possible. Just constructing a **SimpleHybridLock** object causes the **AutoResetEvent** to be created, and this is a massive performance hit compared to the overhead associated with the **Int32** field. Later in this chapter, we'll see another hybrid construct (**AutoResetEventSlim**) that avoids the performance hit of creating the **AutoResetEvent** until the first time contention is detected from multiple threads accessing the lock at the same time. The **Dispose** method closes the **AutoResetEvent**, and this is also a big performance hit compared to the overhead of destroying the **Int32** field.

While it would be nice to improve the performance of constructing and disposing of a **SimpleHybridLock** object, it would be better to focus on the performance of its **Enter** and **Leave** methods because these methods tend to be called many, many times over the object's lifetime. Let's focus on these methods now.