```
```csharp
public Boolean TryEnterReadLock(Int32 millisecondsTimeout);
public void    ExitReadLock();

public void    EnterWriteLock();
public Boolean TryEnterWriteLock(Int32 millisecondsTimeout);
public void    ExitWriteLock();

// Most applications will never query any of these properties
public Boolean IsReadLockHeld            { get; }
public Boolean IsWriteLockHeld           { get; }
public Int32   CurrentReadCount          { get; }
public Int32   RecursiveReadCount        { get; }
public Int32   RecursiveWriteCount       { get; }
public Int32   WaitingReadCount          { get; }
public Int32   WaitingWriteCount         { get; }
public LockRecursionPolicy RecursionPolicy { get; }
// Members related to upgrading from a reader to a writer not shown
}
```
```

Here is some code that demonstrates the use of this construct:

```
```csharp
internal sealed class Transaction : IDisposable {
    private readonly ReaderWriterLockSlim m_lock =
        new ReaderWriterLockSlim(LockRecursionPolicy.NoRecursion);
    private DateTime m_timeOfLastTrans;

    public void PerformTransaction() {
        m_lock.EnterWriteLock();
        // This code has exclusive access to the data...
        m_timeOfLastTrans = DateTime.Now;
        m_lock.ExitWriteLock();
    }

    public DateTime LastTransaction {
        get {
            m_lock.EnterReadLock();
            // This code has shared access to the data...
            DateTime temp = m_timeOfLastTrans;
            m_lock.ExitReadLock();
            return temp;
        }
    }

    public void Dispose() { m_lock.Dispose(); }
}
```
```

There are a few concepts related to this construct that deserve special mention. First, ReaderWriterLockSlim's constructor allows you to pass in a LockRecursionsPolicy flag, which is defined as follows:

```
```csharp
public enum LockRecursionPolicy { NoRecursion, SupportsRecursion }
```
```

If you pass the SupportsRecursion flag, then the lock will add thread ownership and recursion behaviors to the lock. As discussed earlier in this chapter, these behaviors negatively affect the lock's