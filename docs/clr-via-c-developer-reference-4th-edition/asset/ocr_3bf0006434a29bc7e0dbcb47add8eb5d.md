lock, it sets lockTaken to true. The finally block examines lockTaken to know whether to call
Monitor.Exit or not. By the way, the SpinLock structure also supports this lockTaken pattern.

# ReaderWriterLockSlim Class

It is common to have threads read the contents of data. If this data is protected by a
exclusive lock (like the SimpleSpinLock, SimpleWaitLock, SimpleHybridLock, Another-
hybridLock, SpinLock, Mutex, or Monitor), if multiple threads attempt this concur-
ly one thread gets to run and all the other threads are blocked, which can reduce scalability
and throughput in your application substantially. However, if all the threads want to access the data
in a read-only fashion, there is no need to block them at all; they should be able to access the
data concurrently. On the other hand, if a thread wants to modify the data, this thread needs
exclusive access to the data. The ReaderWriterLockSlim encapsulates the logic to solve
this problem. Specifically, the control methods work like this:

+   - When one is writing to the data, all other threads requesting access are blocked.

+   - When one is reading from the data, other threads requesting access are allowed
to continue executing, but threads requesting access are blocked.

+   - When a thread writing to the data has completed, either a single writer is unblocked
it it can access the data or all the reader threads are unblocked so that all of them can access
data concurrently. If no threads are blocked, the lock is free and available for the next
reader or writer thread that wants it.

+   - When all reading from the data have completed, a single writer is unblocked
it to access the data. If no threads are blocked, the lock is free and available for the next
reader or writer thread that wants it.

Here is what this class looks like (some method overloads are not shown).

```
public class ReaderWriterLockSlim : IDisposable {
    public ReaderWriterLockSlim(LockRecursionPolicy recursionPolicy);
    public void Dispose();
```

```
    public void EnterLock();
    public Boolean TryEnterLock(Int32 millisecondsTimeout);
    public void ExitLock();
```

```
    public void EnterWriteLock();
    public Boolean TryEnterWriteLock(Int32 millisecondsTimeout);
    public void ExitWriteLock();
```

```
    // Most applications will never query any of these properties
    public Boolean IsReadLockHeld {
        { get; }
    public Boolean IsWriteLockHeld {
        { get; }
    public Int32 CurrentReadCount {
        { get; }
    public Int32 RecursiveReadCount {
        { get; }
    public Int32 RecursiveWriteCount {
        { get; }
    public Int32 WaitingReaderCount {
        { get; }
    public Int32 WaitingWriteCount {
        { get; }}
```