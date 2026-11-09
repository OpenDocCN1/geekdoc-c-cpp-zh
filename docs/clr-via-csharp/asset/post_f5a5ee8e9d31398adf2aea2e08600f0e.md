
## Chapter 29
## Hybrid Thread Synchronization Constructs

In this chapter:

- A Simple Hybrid Lock ........................................................ 826
- Spinning, Thread Ownership, and Recursion ................................. 827
- A Potpourri of Hybrid Constructs ............................................ 829
- The Famous Double-Check Locking Technique ................................. 844
- The Condition Variable Pattern .............................................. 848
- Using Collections to Avoid Holding a Lock for a Long Time .................. 851
- The Concurrent Collection Classes ........................................... 856

In Chapter 28, "Primitive Thread Synchronization Constructs," I discussed the primitive user-mode and kernel-mode thread synchronization constructs. From these primitive constructs, all other thread synchronization constructs can be built. Typically, other thread synchronization constructs are built by combining the user-mode and kernel-mode constructs, and I call these hybrid thread synchronization constructs. Hybrid constructs provide the performance benefit of the primitive user-mode constructs when there is no thread contention. Hybrid constructs also use the primitive kernel-mode constructs to provide the benefit of not spinning (wasting CPU time) when multiple threads are contending for the construct at the same time. Since, in most applications, threads are rarely contending for a construct at the same time, the performance improvements can help your application greatly.

In this chapter, I will first show how hybrid constructs are built from the various primitive constructs. Then, I will introduce you to many of the hybrid constructs that ship with the Framework Class Library (FCL), describe their behavior, and give some insight as to how to use these constructs correctly. I will also mention some constructs that I have created and make available for free in Wintellect's Power Threading library, which can be downloaded from http://Wintellect.com/.

Toward the end of the chapter, I show how to minimize resource usage and improve performance by using the FCL's concurrent collection classes instead of using some of the hybrid constructs. And finally, I discuss the Power Threading library's ReaderWriterGate and SyncGate classes which offer reader-writer semantics without blocking any threads, thereby also reducing resource consumption and improving performance.

### A Simple Hybrid Lock

So, without further ado, let me start off by showing you an example of a hybrid thread synchronization lock:

```csharp
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
```

The **SimpleHybridLock** contains two fields: an **Int32**, which will be manipulated via the primitive user-mode constructs, and an **AutoResetEvent**, which is a primitive kernel-mode construct. To get great performance, the lock tries to use the **Int32** and avoid using the **AutoResetEvent** as much as possible. Just constructing a **SimpleHybridLock** object causes the **AutoResetEvent** to be created, and this is a massive performance hit compared to the overhead associated with the **Int32** field. Later in this chapter, we'll see another hybrid construct (**AutoResetEventSlim**) that avoids the performance hit of creating the **AutoResetEvent** until the first time contention is detected from multiple threads accessing the lock at the same time. The **Dispose** method closes the **AutoResetEvent**, and this is also a big performance hit compared to the overhead of destroying the **Int32** field.

While it would be nice to improve the performance of constructing and disposing of a **SimpleHybridLock** object, it would be better to focus on the performance of its **Enter** and **Leave** methods because these methods tend to be called many, many times over the object's lifetime. Let's focus on these methods now.

The first thread to call `Enter` causes `Interlocked.Increment` to add one to the `m_waiters` field, making its value 1. This thread sees that there were zero threads waiting before for this lock, so the thread gets to return from its call to `Enter`. The thing to appreciate here is that the thread acquired the lock very quickly. Now, if another thread comes along and calls `Enter`, this second thread increments `m_waiters` to 2 and sees that another thread has the lock, so this thread blocks by calling `WaitOne` using the `AutoResetEvent`. Calling `WaitOne` causes the thread to transition into the Windows kernel, and this is a big performance hit. However, the thread must stop running anyway, so it is not too bad to have a thread waste some time to stop completely. The good news is that the thread is now blocked and so it is not wasting CPU time by spinning on the CPU, which is what the `SimpleSpinLock`'s `Enter` method, introduced in Chapter 28, does.

Now let's look at the `Leave` method. When a thread calls `Leave`, `Interlocked.Decrement` is called to subtract 1 from the `m_waiters` field. If `m_waiters` is now 0, then no other threads are blocked inside a call to `Enter` and the thread calling `Leave` can simply return. Again, think about how fast this is: Leaving a lock means that a thread subtracts 1 from an `Int32`, performs a quick `if` test, and then returns! On the other hand, if the thread calling `Leave` sees that `m_waiters` was not 0, then the thread knows that there is contention and that there is at least one other thread blocked in the kernel. This thread must wake up one (and only one) of the blocked threads. It does this by calling `Set` on `AutoResetEvent`. This is a performance hit, as the thread must transition into the kernel and back, but this transition occurs only when there was contention. Of course, `AutoResetEvent` ensures that only one blocked thread wakes up; any other threads blocked on the `AutoResetEvent` will continue to block until the newly unblocked thread eventually calls `Leave`.

> **Note** In reality, any thread could call `Leave` at any time since the `Enter` method does not keep a record of which thread successfully acquired the lock. Adding the field and code to maintain this information is easy to do but it would increase the memory required for the lock object itself and hurt performance of the `Enter` and `Leave` methods because they would have to manipulate this field. I would rather have a fast-performing lock and make sure that my code uses it the right way. You'll notice that events and semaphores do not maintain this kind of information; only mutexes do.

### Spinning, Thread Ownership, and Recursion

Since transitions into the kernel incur such a big performance hit and threads tend to hold on to a lock for very short periods of time, an application's overall performance can be improved by having a thread spin in user mode for a little while before having the thread transition to kernel mode. If the lock that the thread is waiting for becomes available while spinning, then the transition to kernel mode is avoided.
