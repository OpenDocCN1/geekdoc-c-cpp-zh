

## A Simple Hybrid Lock

So, without further ado, let me start off by showing you an example of a hybrid thread synchronization lock.

```csharp
internal sealed class SimpleHybridLock : IDisposable {
    // The Int32 is used by the primitive user-mode constructs (Interlocked methods)
    private Int32 m_waiters = 0;

    // The AutoResetEvent is the primitive kernel-mode construct
    private readonly AutoResetEvent m_waiterLock = new AutoResetEvent(false);

    public void Enter() {
        // Indicate that this thread wants the lock
        if (Interlocked.Increment(ref m_waiters) == 1)
            return; // Lock was free, no contention, just return

        // Another thread has the lock (contention), make this thread wait
        m_waiterLock.WaitOne(); // Bad performance hit here
        // When WaitOne returns, this thread now has the lock
    }

    public void Leave() {
        // This thread is releasing the lock
        if (Interlocked.Decrement(ref m_waiters) == 0)
            return; // No other threads are waiting, just return

        // Other threads are waiting, wake 1 of them
        m_waiterLock.Set(); // Bad performance hit here
    }

    public void Dispose() { m_waiterLock.Dispose(); }
}
```

The SimpleHybridLock contains two fields: an Int32, which will be manipulated via the primitive user-mode constructs, and an AutoResetEvent, which is a primitive kernel-mode construct. To get great performance, the lock tries to use the Int32 and avoid using the AutoResetEvent as much as possible. Just constructing a SimpleHybridLock object causes the AutoResetEvent to be created, and this is a massive performance hit compared to the overhead associated with the Int32 field. Later in this chapter, we'll see another hybrid construct (AutoResetEventSlim) that avoids the performance hit of creating the AutoResetEvent until the first time contention is detected from multiple threads accessing the lock at the same time. The Dispose method closes the AutoResetEvent, and this is also a big performance hit.

Although it would be nice to improve the performance of constructing and disposing of a SimpleHybridLock object, it would be better to focus on the performance of its Enter and Leave methods because these methods tend to be called many, many times over the object's lifetime. Let's focus on these methods now.

The first thread to call Enter causes Interlocked.Increment to add one to the m_waiters field, making its value 1. This thread sees that there were zero threads waiting for this lock, so the thread gets to return from its call to Enter. The thing to appreciate here is that the thread acquired the lock very quickly. Now, if another thread comes along and calls Enter, this second thread increments m_waiters to 2 and sees that another thread has the lock, so this thread blocks by calling WaitOne using the AutoResetEvent. Calling WaitOne causes the thread to transition into the Windows kernel, and this is a big performance hit. However, the thread must stop running anyway, so it is not too bad to have a thread waste some time to stop completely. The good news is that the thread is now blocked, and so it is not wasting CPU time by spinning on the CPU, which is what the SimpleSpinLock's Enter method, introduced in Chapter 29, does.

Now let's look at the Leave method. When a thread calls Leave, Interlocked.Decrement is called to subtract 1 from the m_waiters field. If m_waiters is now 0, then no other threads are blocked inside a call to Enter and the thread calling Leave can simply return. Again, think about how fast this is: leaving a lock means that a thread subtracts 1 from an Int32, performs a quick if test, and then returns! On the other hand, if the thread calling Leave sees that m_waiters was not 1, then the thread knows that there is contention and that there is at least one other thread blocked in the kernel. This thread must wake up one (and only one) of the blocked threads. It does this by calling Set on AutoResetEvent. This is a performance hit, because the thread must transition into the kernel and back, but this transition occurs only when there was contention. Of course, AutoResetEvent ensures that only one blocked thread wakes up; any other threads blocked on the AutoResetEvent will continue to block until the newly unblocked thread eventually calls Leave.

![](img/857bdf6cef9e242b53a37f88df9a1287_816_0.png)

> **Note** In reality, any thread could call Leave at any time because the Enter method does not keep a record of which thread successfully acquired the lock. Adding the field and code to maintain this information is easy to do, but it would increase the memory required for the lock object itself and hurt performance of the Enter and Leave methods because they would have to manipulate this field. I would rather have a fast-performing lock and make sure that my code uses it the right way. You'll notice that events and semaphores do not maintain this kind of information; only mutexes do.

### Spinning, Thread Ownership, and Recursion

Because transitions into the kernel incur such a big performance hit and threads tend to hold on to a lock for very short periods of time, an application's overall performance can be improved by having a thread spin in user mode for a little while before having the thread transition to kernel mode. If the lock that the thread is waiting for becomes available while spinning, then the transition to kernel mode is avoided.

In addition, some locks impose a limitation where the thread that acquires the lock must be the thread that releases the lock. And some locks allow the currently owning thread to own the lock recursively. The Mutex lock is an example of a lock that has these characteristics.¹ Using some fancy logic, it is possible to build a hybrid lock that offers spinning, thread ownership, and recursion. Here is what the code looks like.

```csharp
internal sealed class AnotherHybridLock : IDisposable {
   // The Int32 is used by the primitive user-mode constructs (Interlocked methods)
   private Int32 m_waiters = 0;

   // The AutoResetEvent is the primitive kernel-mode construct
   private AutoResetEvent m_waiterLock = new AutoResetEvent(false);

   // This field controls spinning in an effort to improve performance
   private Int32 m_spinCount = 4000;   // Arbitrarily chosen count

   // These fields indicate which thread owns the lock and how many times it owns it
   private Int32 m_owningThreadId = 0, m_recursion = 0;

   public void Enter() {
      // If calling thread already owns the lock, increment recursion count and return
      Int32 threadId = Thread.CurrentThread.ManagedThreadId;
      if (threadId == m_owningThreadId) { m_recursion++; return; }

      // The calling thread doesn't own the lock, try to get it
      SpinWait spinWait = new SpinWait();
      for (Int32 spinCount = 0; spinCount < m_spinCount; spinCount++) {
         // If the lock was free, this thread got it; set some state and return
         if (Interlocked.CompareExchange(ref m_waiters, 1, 0) == 0) goto GotLock;

         // Black magic: give other threads a chance to run
         // in hopes that the lock will be released
         spinWait.SpinOnce();
      }

      // Spinning is over and the lock was still not obtained, try one more time
      if (Interlocked.Increment(ref m_waiters) > 1) {
         // Still contention, this thread must wait
         m_waiterLock.WaitOne(); // Wait for the lock; performance hit
         // When this thread wakes, it owns the lock; set some state and return
      }

   GotLock:
      // When a thread gets the lock, we record its ID and
      // indicate that the thread owns the lock once
      m_owningThreadId = threadId; m_recursion = 1;
   }

   public void Leave() {
      // If the calling thread doesn't own the lock, there is a bug
      Int32 threadId = Thread.CurrentThread.ManagedThreadId;
      if (threadId != m_owningThreadId)
         throw new SynchronizationLockException("Lock not owned by calling thread");
```

¹ Threads do not spin when waiting on a Mutex object because the Mutex's code is in the kernel. This means that the thread had to have already transitioned into the kernel to check the Mutex's state.

