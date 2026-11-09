
In addition, some locks impose a limitation where the thread that acquires the lock must be the thread that releases the lock. And some locks allow the currently owning thread to own the lock recursively. The `Mutex` lock is an example of a lock that has these characteristics.¹ Using some fancy logic, it is possible to build a hybrid lock that offers spinning, thread ownership, and recursion. Here is what the code looks like:

```csharp
internal sealed class AnotherHybridLock : IDisposable {
   // The Int32 is used by the primitive user-mode constructs (Interlocked methods)
   private Int32 m_waiters = 0;

   // The AutoResetEvent is the primitive kernel-mode construct
   private AutoResetEvent m_waiterLock = new AutoResetEvent(false);

   // This field controls spinning in an effort to improve performance
   private Int32 m_spincount = 4000;   // Arbitrarily chosen count

   // These fields indicate which thread owns the lock and how many times it owns it
   private Int32 m_owningThreadId = 0, m_recursion = 0;

   public void Enter() {
      // If calling thread already owns the lock, increment recursion count and return
      Int32 threadId = Thread.CurrentThread.ManagedThreadId;
      if (threadId == m_owningThreadId) { m_recursion++; return; }

      // The calling thread doesn't own the lock, try to get it
      SpinWait spinwait = new SpinWait();
      for (Int32 spinCount = 0; spinCount < m_spincount; spinCount++) {
         // If the lock was free, this thread got it; set some state and return
         if (Interlocked.CompareExchange(ref m_waiters, 1, 0) == 0) goto GotLock;

         // Black magic: give other threads a chance to run
         // in hopes that the lock will be released
         spinwait.SpinOnce();
      }

      // Spinning is over and the lock was still not obtained, try one more time
      if (Interlocked.Increment(ref m_waiters) > 1) {
         // Other threads are blocked and this thread must block too
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

> ¹ Threads do not spin when waiting on a `Mutex` object because the `Mutex`'s code is in the kernel. This means that the thread had to have already transitioned into the kernel to check the `Mutex`'s state.

As you can see, adding extra behavior to the lock increases the number of fields it has, which increases its memory consumption. The code is also more complex, and this code must execute, which decreases the lock's performance. In Chapter 28's "Event Constructs" section, I compared the performance of incrementing an **Int32** without any locking, with a primitive user-mode construct, and with a kernel-mode construct. I repeat the results of those performance tests here and I include the results of using the **SimpleHybridLock** and the **AnotherHybridLock**. The results are in fastest to slowest order:

- Incrementing x: 8  Fastest
- Incrementing x in M: 50  6x slower
- Incrementing x in SimpleSpinLock: 210  26x slower
- Incrementing x in SimpleHybridLock: 211  26x slower (similar to SimpleSpinLock)
- Incrementing x in AnotherHybridLock: 415  52x slower (due to ownership/recursion)
- Incrementing x in SimpleWaitLock: 17,615  2,201x slower

It is worth noting that the **AnotherHybridLock** takes twice as much time as the **SimpleHybridLock**. This is due to the additional logic and error checking required managing the thread ownership and recursion behaviors. As you see, every behavior added to a lock impacts its performance.

## A Potpourri of Hybrid Constructs

The FCL ships with many hybrid constructs that use fancy logic to keep your threads in user mode, improving your application's performance. Some of these hybrid constructs also avoid creating the kernel-mode construct until the first time threads contend on the construct. If threads never contend on the construct, then your application avoids the performance of creating the object and also avoids allocating memory for the object. A number of the constructs also support the use of a **CancellationToken** (discussed in Chapter 26, "Compute-Bound Asynchronous Operations") so that a thread can forcibly unblock other threads that might be waiting on the construct. In this section, I introduce you to these hybrid constructs.

### The ManualResetEventSlim and SemaphoreSlim Classes

The first two hybrid constructs are **System.Threading.ManualResetEventSlim** and **System.Threading.SemaphoreSlim**.<sup>2</sup> These constructs work exactly like their kernel-mode counterparts except that both employ spinning in user mode and they both defer creating the kernel-mode construct until the first time contention occurs. Their **Wait** methods allow you to pass a timeout and a **CancellationToken**. Here is what these classes look like (some method overloads are not shown):

```csharp
public class ManualResetEventSlim : IDisposable {
    public ManualResetEventSlim(Boolean initialState, Int32 spinCount);
    public void Dispose();
    public void Reset();
    public void Set();
    public Boolean Wait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

    public Boolean IsSet { get; }
    public Int32 SpinCount { get; }
    public WaitHandle WaitHandle { get; }
}
public class SemaphoreSlim : IDisposable {
    public SemaphoreSlim(Int32 initialCount, Int32 maxCount);
    public void Dispose();
    public Int32 Release(Int32 releaseCount);
    public Boolean Wait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

    public Int32 CurrentCount { get; }
    public WaitHandle AvailableWaitHandle { get; }
}
```

### The Monitor Class and Sync Blocks

Probably the most-used hybrid thread synchronization construct is the **Monitor** class, which provides a mutual-exclusive lock supporting spinning, thread ownership, and recursion. This is the most-used construct because it has been around the longest, C# has a built-in keyword to support it, the just-in-time (JIT) compiler has built-in knowledge of it, and the common language runtime (CLR) itself uses it on your application's behalf. However, as you'll see, there are many problems with this construct, making it easy to produce buggy code. I'll start by explaining the construct, and then I'll show the problems and some ways to work around these problems.

> <sup>2</sup> While there is no **AutoResetEventSlim** class, in many situations you can construct a **SemaphoreSlim** object with a **maxCount** of 1.

Every object on the heap can have a data structure, called a *sync block*, associated with it. A sync block contains fields similar to that of the **AnotherHybridLock** class that appeared earlier in this chapter. Specifically, it has fields for a kernel object, the owning thread's ID, a recursion count, and a waiting threads count. The **Monitor** class is a **static** class whose methods accept a reference to any heap object, and these methods manipulate the fields in the specified object's sync block. Here is what the most commonly used methods of the **Monitor** class look like:

```csharp
public static class Monitor {
    public static void Enter(Object obj);
    public static void Exit(Object obj);

    // You can also specify a timeout when entering the lock (not commonly used):
    public static Boolean TryEnter(Object obj, Int32 millisecondsTimeout);

    // I'll discuss the lockTaken argument later
    public static void Enter(Object obj, ref Boolean lockTaken);
    public static void TryEnter(Object obj, Int32 millisecondsTimeout,
        ref Boolean lockTaken);
}
```

Now obviously, associating a sync block data structure with every object in the heap is quite wasteful, especially since most objects' sync blocks are never used. To reduce memory usage, the CLR team uses a more efficient way to offer the functionality just described. Here's how it works: When the CLR initializes, it allocates an array of sync blocks. As discussed elsewhere in this book, whenever an object is created in the heap, it gets two additional overhead fields associated with it. The first overhead field, the type object pointer, contains the memory address of the type's type object. The second overhead field, the sync block index, contains an integer index into the array of sync blocks.

When an object is constructed, the object's sync block index is initialized to -1, which indicates that it doesn't refer to any sync block. Then, when **Monitor.Enter** is called, the CLR finds a free sync block in the array and sets the object's sync block index to refer to the sync block that was found. In other words, sync blocks are associated with an object on the fly. When **Exit** is called, it checks to see if there are any more threads waiting to use the object's sync block. If there are no threads waiting for it, the sync block is free, **Exit** sets the object's sync block index back to -1, and the free sync block can be associated with another object in the future.

Figure 29-1 shows the relationship between objects in the heap, their sync block indexes, and elements in the CLR's sync block array. Object-A, Object-B, and Object-C all have their type object pointer member set to refer to Type-T (a type object). This means that all three objects are of the same type. As discussed in Chapter 4, "Type Fundamentals," a type object is also an object in the heap, and like all other objects, a type object has the two overhead members: a sync block index and a type object pointer. This means that a sync block can be associated with a type object and a reference to a type object can be passed to **Monitor**'s methods. By the way, the sync block array is able to create more sync blocks if necessary, so you shouldn't
