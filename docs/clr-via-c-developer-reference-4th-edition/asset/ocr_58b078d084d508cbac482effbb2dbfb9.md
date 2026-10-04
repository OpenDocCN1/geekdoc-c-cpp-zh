```
public LockRecursionPolicy RecursionPolicy { get; }
// Members related to upgrading from a reader to a writer not shown
}
```

Here is some code that demonstrates the use of this construct.

```
internal sealed class Transaction : IDisposable {
    private readonly ReaderWriterSlim m_lock =
        new ReaderWriterSlim(LockRecursionPolicy.NoRecursion);
    private DateTime m_timeOfLastTransaction;

    public void PerformTransaction() {
        m_lock.EnterWriteLock();
        // This code has exclusive access to the data...
        m_timeOfLastTransaction = DateTime.Now;
        m_lock.ExitWriteLock();
    }

    public DateTime LastTransaction {
        get {
            m_lock.EnterReadLock();
            // This code has shared access to the data...
            DateTime temp = m_timeOfLastTransaction;
            m_lock.ExitReadLock();
            return temp;
        }
    }

    public void Dispose() { m_lock.Dispose(); }
}
```

There are few concepts related to this construct that deserve special mention. Reader-ReaderWriterLockSlim's constructor allows you to pass in a LockRecursionPolicy flag, which is defined as follows.

```
public enum LockRecursionPolicy { NoRecursion, SupportsRecursion }
```

If you pass the SupportsRecursion flag, the lock will add thread ownership and recursion behaviors to the lock. As discussed earlier in this chapter, these behaviors negatively affect the lock's performance, so I recommend you always pass LockRecursionPolicy.NoRecursion to the constructor (as I've done). For a reader-writer lock, supporting ownership and recursion is notoriously expensive, because the lock must keep track of all the reader threads that it has let into the lock and keep a separate recursion count for each reader thread. To maintain this information in a thread-safe way, the ReaderWriterLockSlim internally uses a mutually exclusive spinlock! No, not kidding.

The ReaderWriterLockSlim class offers additional methods (not shown here) that allow a reading thread to upgrade itself to a writer thread. Later, the thread can downgrade itself to a reader thread. The thinking here is that a thread could start reading the data and based on the data's contents, the thread might want to modify it. To do this, the thread would upgrade itself from a reader to writer. Having the lock support deteriorates the lock's performance, and I don't think this is a useful feature at all. Here's a why: you can't just turn itself from a reader