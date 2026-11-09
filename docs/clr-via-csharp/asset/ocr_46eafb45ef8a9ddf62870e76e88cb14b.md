```
```csharp
Int32 threadId = Thread.CurrentThread.ManagedThreadId;
if (threadId != m_owningThreadId)
    throw new SynchronizationLockException("Lock not owned by calling thread");

// Decrement the recursion count. If this thread still owns the lock, just return
if (--m_recursion > 0) return;

m_owningThreadId = 0;   // No thread owns the lock now

// If no other threads are blocked, just return
if (Interlocked.Decrement(ref m_waiters) == 0)
    return;

// Other threads are blocked, wake 1 of them
m_waiterLock.Set();     // Bad performance hit here
}

public void Dispose() { m_waiterLock.Dispose(); }
}
```
```

As you can see, adding extra behavior to the lock increases the number of fields it has, which increases its memory consumption. The code is also more complex, and this code must execute, which decreases the lock's performance. In Chapter 28's "Event Constructs" section, I compared the performance of incrementing an **Int32** without any locking, with a primitive user-mode construct, and with a kernel-mode construct. I repeat the results of those performance tests here and I include the results of using the **SimpleHybridLock** and the **AnotherHybridLock**. The results are in fastest to slowest order:

+   - Incrementing x: 8  Fastest
+   - Incrementing x in M: 50  6x slower
+   - Incrementing x in SimpleSpinLock: 210  26x slower
+   - Incrementing x in SimpleHybridLock: 211  26x slower (similar to SimpleSpinLock)
+   - Incrementing x in AnotherHybridLock: 415  52x slower (due to ownership/recursion)
+   - Incrementing x in SimpleWaitLock: 17,615  2,201x slower

It is worth noting that the **AnotherHybridLock** takes twice as much time as the **SimpleHybridLock**. This is due to the additional logic and error checking required managing the thread ownership and recursion behaviors. As you see, every behavior added to a lock impacts its performance.

# # A Potpourri of Hybrid Constructs

The FCL ships with many hybrid constructs that use fancy logic to keep your threads in user mode, improving your application's performance. Some of these hybrid constructs also avoid creating the kernel-mode construct until the first time threads contend on the construct. If threads never contend on the construct, then your application avoids the performance of creating the object and also avoids allocating memory for the object. A number of the constructs also support the use of a **CancellationToken** (discussed in Chapter 26, "Compute-