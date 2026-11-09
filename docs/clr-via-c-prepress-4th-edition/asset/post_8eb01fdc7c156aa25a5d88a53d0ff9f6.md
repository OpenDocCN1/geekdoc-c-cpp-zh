
```csharp
public Boolean TryEnterReadLock(Int32 millisecondsTimeout);
public void ExitReadLock();

public void EnterWriteLock();
public Boolean TryEnterWriteLock(Int32 millisecondsTimeout);
public void ExitWriteLock();

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

Here is some code that demonstrates the use of this construct:

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

There are a few concepts related to this construct that deserve special mention. First, ReaderWriterLockSlim's constructor allows you to pass in a LockRecursionPolicy flag, which is defined as follows:

```csharp
public enum LockRecursionPolicy { NoRecursion, SupportsRecursion }
```

If you pass the SupportsRecursion flag, then the lock will add thread ownership and recursion behaviors to the lock. As discussed earlier in this chapter, these behaviors negatively affect the lock's performance, so I recommend that you always pass LockRecursionPolicy.NoRecursion to the constructor (as I've done). For a reader-writer lock, supporting thread ownership and recursion is phenomenally expensive, because the lock must keep track of all the reader threads that it has let into the lock and keep a separate recursion count for each reader thread. In fact, to maintain all this information in a thread-safe way, the ReaderWriterLockSlim internally uses a mutually exclusive spinlock! No, I'm not kidding.

The ReaderWriterLockSlim class offers additional methods (not shown earlier) that allow a reading thread to upgrade itself to a writer thread. Later, the thread can downgrade itself to a reader thread. The thinking here is that a thread could start reading the data and based on the data's contents, the thread might want to modify the data. To do this, the thread would upgrade itself from a reader to a writer. Having the lock support this behavior deteriorates the lock's performance, and I don't think that this is a useful feature at all. Here's why: A thread can't just turn itself from a reader into a writer. Other threads may be reading, too, and these threads will have to exit the lock completely before the thread trying to upgrade is allowed to become a writer. This is the same as having the reader thread exit the lock and then immediately acquire it for writing.

**Note** The FCL also ships a ReaderWriterLock construct, which was introduced in the Microsoft .NET Framework version 1.0. This construct had so many problems that Microsoft introduced the ReaderWriterLockSlim construct in .NET Framework version 3.5. The team didn't improve the ReaderWriterLock construct for fear of losing compatibility with applications that were using it. Here are the problems with the ReaderWriterLock. Even without thread contention, it is very slow. There is no way to opt out of the thread ownership and recursion behaviors, making the lock even slower. It favors reader threads over writer threads, and therefore, writer threads can get queued up and are rarely serviced, which results in denial of service problems.

## The OneManyLock Class

I have created my own reader-writer construct that is faster than the FCL's ReaderWriterLockSlim class.<sup>75</sup> My class is called OneManyLock because it allows access to either one writer thread or many reader threads. The class basically looks like this:

```csharp
public sealed class OneManyLock : IDisposable {
   public OneManyLock();
   public void Dispose();

   public void Enter(Boolean exclusive);
   public void Leave();
}
```

Now I'd like to give you a sense of how it works. Internally, the class has an Int64 field for the state of the lock, a Semaphore object that reader threads block on, and an AutoResetEvent object that writer threads block on. The Int64 state field is divided into four subfields as follows:

- Four bits represent the state of the lock itself. The possibilities are 0=Free, 1=OwnedByWriter, 2=OwnedByReaders, 3=OwnedByReadersAndWriterPending, and 4=ReservedForWriter. The other values are not used.
- Twenty bits (a number from 0 to 1,048,575) represent the number of reader threads reading (RR) that the lock has currently allowed in.
- Twenty bits represent the number of reader threads waiting (RW) to get into the lock. These threads block on the auto-reset event object.
- Twenty bits represent the number of writer threads waiting (WW) to get into the lock. These threads block on the other semaphore object.

Now, since all the information about the lock fits in a single Int64 field, I can manipulate this field using the methods of the Interlocked class so the lock is incredibly fast and causes a thread to block only when there is contention.

Here's what happens when a thread enters the lock for shared access:

- If the lock is Free: Set state to OwnedByReaders, RR=1, Return
- If the lock is OwnedByReaders: RR++, Return
- Else: RW++, Block reader thread. When the thread wakes, loop around and try again.

Here's what happens when a thread that has shared access leaves the lock:

- RR--
- If RR > 0: Return
- If WW > 0: Set state to ReservedForWriter, WW--, Release 1 blocked writer thread, Return
- If RW == 0 && WW == 0: Set state to Free, Return

Here's what happens when a thread enters the lock for exclusive access:

- If the lock is Free: Set state to OwnedByWriter, Return
- If the lock is ReservedForWriter: Set state to OwnedByWriter, Return
- If the lock is OwnedByWriter: WW++, Block writer thread. When thread wakes, loop around and try again.
- Else: Set state to OwnedByReadersAndWriterPending, WW++, Block writer thread. When thread wakes, loop around and try again.

Here's what happens when a thread that has exclusive access leaves the lock:

you want to synchronize threads that are running in different AppDomains or processes. To atomically manipulate state via a set of operations, use the `Monitor` class with a private field.^76 Alternatively, you could use a reader-writer lock instead of `Monitor`. Reader-writer locks are generally slower than `Monitor`, but they allow multiple reader threads to execute concurrently, which improves overall performance and minimizes the chance of blocking the reader threads.

In addition, avoid using recursive locks (especially recursive reader-writer locks) because they hurt performance. However, `Monitor` is recursive and its performance is very good.^77 Also, avoid releasing a lock in a `finally` block because entering and leaving exception-handling blocks incurs a performance hit, and if an exception is thrown while mutating state, then the state is corrupted, and other threads that manipulate it will experience unpredictable behavior and security bugs.

Of course, if you do write code that holds a lock, your code should not hold the lock for a long time, because this increases the likelihood of threads blocking. In the “Asynchronous Synchronization” section, I will show a technique that uses collection classes as a way to avoid holding a lock for a long time.

Finally, for compute-bound work, you can use tasks (discussed in Chapter 27) to avoid a lot of the thread synchronization constructs. In particular, I love that each task can have one or more continue-with tasks associated with it that execute via some thread pool thread when some operation completes. This is much better than having a thread block waiting for some operation to complete. For I/O-bound work, call the various XxxAsync methods which cause your code to continue running after the I/O operation completes; this is similar to a task’s continue-with task.

## The Famous Double-Check Locking Technique

There is a famous technique called double-check locking, which is used by developers who want to defer constructing a singleton object until an application requests it (sometimes called lazy initialization). If the application never requests the object, it never gets constructed, saving time and memory. A potential problem occurs when multiple threads request the singleton object simultaneously. In this case, some form of thread synchronization must be used to ensure that the singleton object gets constructed just once.

This technique is not famous because it is particularly interesting or useful. It is famous because there has been much written about it. This technique was used heavily in Java, and later it was discovered that Java couldn’t guarantee that it would work everywhere. The famous document that describes the problem can be found on this webpage: www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html.

^75 The code is inside the Ch30-1-HybridThreadSync.cs file that is part of the code that accompanies this book. You can download this code from http://Wintellect.com/Books.

^76 You could use a `SpinLock` instead of `Monitor` because `SpinLock`s are slightly faster. But a `SpinLock` is potentially dangerous because at least one core must waste CPU time and, in my opinion, it is not sufficiently faster than `Monitor` to justify its use.

^77 This is partially because `Monitor` is actually implemented in native code, not managed code.
