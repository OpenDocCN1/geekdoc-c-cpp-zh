
- 二十位表示等待（WW）进入锁的写入线程数。这些线程阻塞在另一个信号量对象上。

现在，由于锁的所有信息都放在一个 Int32 字段中，我可以通过使用 Interlocked 类的方法来操作该字段，因此这个锁非常快，并且只有在存在争用时才会导致线程阻塞。

当线程以共享访问方式进入锁时，会发生以下情况。

- 如果锁为 Free：将状态设置为 OwnedByReaders，RR=1，返回。
- 如果锁为 OwnedByReaders：RR++，返回。
- 否则：RW++，阻塞读者线程。当该线程被唤醒时，循环回来并重试。

当持有共享访问权的线程离开锁时，会发生以下情况。

- RR--
- 如果 RR > 0：返回
- 如果 WW > 0：将状态设置为 ReservedForWriter，WW--，释放 1 个被阻塞的写入线程，返回
- 如果 RW == 0 && WW == 0：将状态设置为 Free，返回

当线程以独占访问方式进入锁时，会发生以下情况：

- 如果锁为 Free：将状态设置为 OwnedByWriter，返回。
- 如果锁为 ReservedForWriter：将状态设置为 OwnedByWriter，返回。
- 如果锁为 OwnedByWriter：WW++，阻塞写入线程。当线程被唤醒时，循环回来并重试。
- 否则：将状态设置为 OwnedByReadersAndWriterPending，WW++，阻塞写入线程。当线程被唤醒时，循环回来并重试。

当持有独占访问权的线程离开锁时，会发生以下情况：

- 如果 WW == 0 && RW == 0：将状态设置为 Free，返回
- 如果 WW > 0：将状态设置为 ReservedForWriter，WW--，释放 1 个被阻塞的写入线程，返回
- 如果 WW == 0 && RW > 0：将状态设置为 Free，RW=0，唤醒所有被阻塞的读者线程，返回

假设当前有一个线程正在从锁中读取，而另一个线程想以写入方式进入锁。写入线程会首先检查锁是否为 Free，由于不是，该线程会继续执行下一次检查。然而，此时读者线程可能离开锁，并且看到 RR 和 WW 都为 0，于是该线程可能将锁的状态设置为 Free。这是一个问题，因为写入线程已经执行了这项测试并继续前进了。基本上，发生的情况是读者线程在写入线程不知情的情况下更改了后者正在访问的状态。我需要解决这个问题，以便锁能够正确工作。为了解决这个问题，所有这些位操作都使用我在第 29 章“The Interlocked Anything Pattern”一节中展示的技术来执行。如果你还记得，这个模式可以让你把任何操作变成线程安全的原子操作。正是这一点使这个锁如此快，并且比其他读写锁包含更少的状态。当我运行性能测试，将我的 OneManyLock 与 FCL 的 ReaderWriterLockSlim 和 ReaderWriterLock 类进行比较时，得到以下结果。

| 操作 | 耗时 | 相对性能 |
|---|---|---|
| 在 OneManyLock 中递增 x | 330 | 最快 |
| 在 ReaderWriterLockSlim 中递增 x | 554 | 约慢 1.7 倍 |
| 在 ReaderWriterLock 中递增 x | 984 | 约慢 3 倍 |

当然，因为所有读写锁都比互斥锁执行更多逻辑，所以它们的性能可能略差。但是，你必须权衡这一点与读写锁允许同时有多个读者进入锁这一事实。

在结束本节之前，我还要提到，我的 Power Threading 库（可从 http://Wintellect.com/PowerThreading.aspx 免费下载）提供了这个锁的一个略有不同的版本，称为 OneManyResourceLock。这个锁以及库中的其他锁提供了许多额外功能，例如死锁检测、启用锁所有权和递归的能力（尽管会带来性能损失）、所有锁的统一编程模型，以及观察锁运行时行为的能力。对于观察行为，你可以看到一个线程等待获取锁的最长时间，以及锁被持有的最短和最长时间。

### CountdownEvent 类

下一个构造是 System.Threading.CountdownEvent。在内部，这个构造使用一个 ManualResetEventSlim 对象。这个构造会阻塞线程，直到其内部计数器达到 0。在某种程度上，这个构造的行为与 Semaphore 的行为相反（Semaphore 在其计数为 0 时阻塞线程）。这个类如下所示（未显示某些方法重载）。

```csharp
public class CountdownEvent : IDisposable {
    public CountdownEvent(Int32 initialCount);
    public void Dispose();
    public void Reset(Int32 count);              // Set CurrentCount to count
    public void AddCount(Int32 signalCount);     // Increments CurrentCount by signalCount
    public Boolean TryAddCount(Int32 signalCount); // Increments CurrentCount by signalCount
    public Boolean Signal(Int32 signalCount);    // Decrements CurrentCount by signalCount
    public Boolean Wait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

    public Int32       CurrentCount { get; }
    public Boolean     IsSet        { get; }      // true if CurrentCount is 0
    public WaitHandle  WaitHandle   { get; }
}
```

CountdownEvent 的 CurrentCount 达到 0 后就不能再更改。当 CurrentCount 为 0 时，AddCount 方法会抛出 InvalidOperationException，而 TryAddCount 方法在 CurrentCount 为 0 时只返回 false。

### Barrier 类

System.Threading.Barrier 构造旨在解决一个非常罕见的问题，因此你不太可能会用到它。Barrier 用于控制一组并行协作的线程，使它们能够一起逐步完成算法的各个阶段。也许举个例子比较合适：当 CLR 使用其垃圾回收器（GC）的服务器版本时，GC 算法会为每个核心创建一个线程。这些线程遍历不同应用程序线程的栈，并发地标记堆中的对象。当每个线程完成自己那部分工作后，它必须停下来等待其他线程完成各自那部分工作。在所有线程都标记完对象之后，线程可以并发地压缩堆的不同部分。当每个线程完成压缩自己那部分堆后，该线程必须阻塞等待其他线程。在所有线程都完成压缩自己那部分堆之后，所有线程会遍历应用程序线程的栈，修正根引用，使其指向被压缩对象的新位置。只有在所有线程都完成这项工作之后，垃圾回收器才算完成，应用程序的线程才能恢复运行。

使用 Barrier 类可以轻松解决此场景，该类如下所示（未显示某些方法重载）。

```csharp
public class Barrier : IDisposable {
    public Barrier(Int32 participantCount, Action<Barrier> postPhaseAction);
    public void Dispose();
    public Int64 AddParticipants(Int32 participantCount); // Adds participants
    public void RemoveParticipants(Int32 participantCount); // Subtracts participants
    public Boolean SignalAndWait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

    public Int64 CurrentPhaseNumber    { get; } // Indicates phase in process (starts at 0)
    public Int32 ParticipantCount      { get; } // Number of participants
    public Int32 ParticipantsRemaining { get; } // # of threads needing to call SignalAndWait
}
```

构造 Barrier 时，你要告诉它有多少个线程参与工作，还可以传入一个 Action<Barrier> 委托，指向每当所有参与者完成工作某一阶段时就会调用的代码。你可以通过调用 AddParticipants 和 RemoveParticipants 方法动态地向 Barrier 添加和移除参与线程，但在实践中很少这样做。当每个线程完成其工作阶段后，它应调用 SignalAndWait，这会告诉 Barrier 该线程已完成，并且 Barrier 会阻塞该线程（使用 ManualResetEventSlim）。在所有参与者都调用 SignalAndWait 之后，Barrier 会调用该委托（由最后一个调用 SignalAndWait 的线程执行），然后解除所有等待线程的阻塞，使它们可以开始下一阶段。

### 线程同步构造总结

我的建议始终是避免编写会阻塞任何线程的代码。在执行异步计算或 I/O 操作时，以这样的方式在线程之间传递数据：避免多个线程同时访问数据的可能性。如果你无法完全
