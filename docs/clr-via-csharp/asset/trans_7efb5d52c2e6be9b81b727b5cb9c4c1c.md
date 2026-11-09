

此外，有些锁会施加一种限制：获取锁的线程必须是释放该锁的线程。而有些锁允许当前拥有该锁的线程递归地拥有该锁。`Mutex` 锁就是具有这些特征的一种锁的示例。¹ 使用一些巧妙的逻辑，可以构建一个混合锁，它提供自旋、线程所有权和递归。代码如下所示：

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

> ¹ 线程在等待 `Mutex` 对象时不会自旋，因为 `Mutex` 的代码位于内核中。这意味着线程必须已经转换到内核中才能检查 `Mutex` 的状态。

如你所见，为锁添加额外行为会增加其字段数量，从而增加其内存消耗。代码也更复杂，而且这些代码必须执行，这会降低锁的性能。在第 28 章“事件构造”一节中，我比较了在没有任何锁、使用基元用户模式构造以及使用内核模式构造的情况下递增 **Int32** 的性能。我在这里重复那些性能测试的结果，并加入使用 **SimpleHybridLock** 和 **AnotherHybridLock** 的结果。结果按从最快到最慢的顺序排列：

- 递增 x：8 最快
- 在 M 中递增 x：50 慢 6 倍
- 在 SimpleSpinLock 中递增 x：210 慢 26 倍
- 在 SimpleHybridLock 中递增 x：211 慢 26 倍（与 SimpleSpinLock 类似）
- 在 AnotherHybridLock 中递增 x：415 慢 52 倍（由于所有权/递归）
- 在 SimpleWaitLock 中递增 x：17,615 慢 2,201 倍

值得注意的是，**AnotherHybridLock** 花费的时间是 **SimpleHybridLock** 的两倍。这是因为管理线程所有权和递归行为需要额外的逻辑和错误检查。如你所见，添加到锁中的每一种行为都会影响其性能。

## 混合构造大杂烩

FCL 附带了许多混合构造，它们使用巧妙的逻辑让你的线程保持在用户模式，从而提高应用程序的性能。其中一些混合构造还会避免在第一次出现线程争用该构造之前创建内核模式构造。如果线程从不在该构造上争用，那么你的应用程序就可以避免创建该对象的性能开销，也避免为该对象分配内存。许多构造还支持使用 **CancellationToken**（在第 26 章“计算密集型异步操作”中讨论），以便线程可以强制解除其他可能正在等待该构造的线程的阻塞。在本节中，我将向你介绍这些混合构造。

### ManualResetEventSlim 和 SemaphoreSlim 类

前两个混合构造是 **System.Threading.ManualResetEventSlim** 和 **System.Threading.SemaphoreSlim**。<sup>2</sup> 这些构造的工作方式与其内核模式对应物完全相同，只是二者都在用户模式下采用自旋，并且都会推迟创建内核模式构造，直到第一次发生争用。它们的 **Wait** 方法允许你传入超时和 **CancellationToken**。这些类如下所示（未显示某些方法重载）：

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

### Monitor 类和同步块

可能最常用的混合线程同步构造是 **Monitor** 类，它提供支持自旋、线程所有权和递归的互斥锁。它是最常用的构造，因为它存在的时间最长，C# 有内置关键字支持它，即时（JIT）编译器内置了对它的了解，并且公共语言运行时（CLR）本身也会代表你的应用程序使用它。然而，正如你将看到的，这个构造存在许多问题，很容易产生有缺陷的代码。我将先解释这个构造，然后展示这些问题以及一些规避这些问题的方法。

> <sup>2</sup> 虽然没有 **AutoResetEventSlim** 类，但在许多情况下，你可以构造一个 **maxCount** 为 1 的 **SemaphoreSlim** 对象。

堆上的每个对象都可以有一个与之关联的数据结构，称为*同步块*。同步块包含的字段类似于本章前面出现的 **AnotherHybridLock** 类。具体来说，它有用于内核对象、拥有线程的 ID、递归计数和等待线程计数的字段。**Monitor** 类是一个 **static** 类，其方法接受对任意堆对象的引用，这些方法操作指定对象的同步块中的字段。**Monitor** 类最常用的方法如下所示：

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

现在显然，为堆中的每个对象关联一个同步块数据结构是相当浪费的，尤其是大多数对象的同步块从未被使用。为了减少内存使用，CLR 团队使用一种更高效的方式来提供刚才描述的功能。其工作方式如下：当 CLR 初始化时，它会分配一个同步块数组。正如本书其他地方所讨论的，每当在堆中创建对象时，该对象都会获得两个与之关联的额外开销字段。第一个开销字段是类型对象指针，它包含该类型的类型对象的内存地址。第二个开销字段是同步块索引，它包含一个指向同步块数组的整数索引。

构造对象时，对象的同步块索引初始化为 -1，表示它不引用任何同步块。然后，当调用 **Monitor.Enter** 时，CLR 会在数组中找到空闲的同步块，并将对象的同步块索引设置为引用找到的同步块。换句话说，同步块是按需与对象关联的。调用 **Exit** 时，它会检查是否还有线程在等待使用该对象的同步块。如果没有线程在等待它，该同步块就是空闲的，**Exit** 会将对象的同步块索引设置回 -1，而这个空闲同步块将来可以关联到另一个对象。

图 29-1 展示了堆中的对象、它们的同步块索引以及 CLR 同步块数组中的元素之间的关系。Object-A、Object-B 和 Object-C 的类型对象指针成员都设置为引用 Type-T（一个类型对象）。这意味着这三个对象都属于同一类型。正如第 4 章“类型基础”中所讨论的，类型对象也是堆中的一个对象，并且像所有其他对象一样，类型对象有两个开销成员：同步块索引和类型对象指针。这意味着同步块可以与类型对象关联，并且对类型对象的引用可以传递给 **Monitor** 的方法。顺便说一下，同步块数组能够在必要时创建更多同步块，因此你不应该

