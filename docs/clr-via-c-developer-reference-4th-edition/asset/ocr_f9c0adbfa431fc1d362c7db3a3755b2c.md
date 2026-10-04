```
// The calling thread doesn't own the lock, wait for it
m_lock.WaitOne();

// The calling now owns the lock, initialize the owning thread ID & recursion count
m_owningThreadId = currentThreadId;
m_recursionCount = 1;
}

public void Leave() {
    // If the calling thread doesn't own the lock, we have an error
    if (m_owningThreadId != Thread.CurrentThread.ManagedThreadId)
        throw new InvalidOperationException();

    // Subtract 1 from the recursion count
    if (--m_recursionCount == 0) {
        // If the recursion count is 0, then no thread owns the lock
        m_owningThreadId = 0;
        m_lock.Set(); // Wake up 1 waiting thread (if any)
    }
}

public void Dispose() { m_lock.Dispose(); }
```

Although the behavior of the RecursiveAutoResetEvent class is identical to that of the Mutex class, RecursiveAutoResetEvent object will have far superior performance when a thread tries to acquire the lock recursively, because all the code that is required to track thread ownership and recursion is now in managed code. A thread has to transition into the Windows kernel only when first acquiring the AutoResetEvent or when finally relinquishing it to another thread.