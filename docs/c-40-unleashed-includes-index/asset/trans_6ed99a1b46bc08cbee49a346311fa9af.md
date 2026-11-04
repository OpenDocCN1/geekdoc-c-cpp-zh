

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1510_0.png)

图 29.23 铁路信号机同步对一段铁路的访问。

从托管代码的角度看，信号量通过 Semaphore 类公开，该类使用两个整数值构造：一个表示初始计数，一个表示最大计数。其思路如下：最大计数表示受信号量保护的代码允许的并发进入数量。用铁路信号机作类比，这个计数会是 2，因为两列火车可以同时位于该铁路区段上（其中一列必须谨慎前行）：

```csharp
var railwaySemaphore = new Semaphore(2, 2);
```

初始计数的第一个参数表示最初允许多少个参与者“与”信号量一起运行。在前面的示例中，我们将该数字设为 2，这意味着铁路信号机是在该设备即将保护的路段上没有列车时竖立起来的。换句话说，铁路公司启用该信号机后，立即允许两列火车通过该信号机。

信号量上存在两个关键操作（忽略重载），如下所示。Release 方法用于递减信号量的值，可以减一，也可以减去指定计数。WaitOne 方法继承自 WaitHandle 基类（将在“使用事件发出信号”一节中讨论），并递增信号量的值。如果信号量已达到其最大计数，WaitOne 方法会阻塞，直到该值因 Release 调用而减少：

```csharp
public int Release();
public int Release(int releaseCount);

public virtual bool WaitOne();
// More WaitOne method overloads...
```

多个线程可以同时等待该信号量。在 WaitOne 操作成功后，哪个线程将获得运行机会是不可预测的，取决于操作系统调度器的心情。除非释放计数大于 1，否则不会有两个线程能够从 WaitOne 操作返回。毕竟，像信号量这样的原语会为其保护机制提供坚实的保证。就信号量而言，绝不应该出现同时使用信号量超过指定最大次数的情况。

这里展示了一个使用火车的示例。显然，这个简单示例并没有真正保护共享资源（只是一段想象中的铁路区段）。信号量的真正用途包括保护共享资源池，并对允许同时使用的次数设置上限。MSDN 上展示了这样一个示例。

```csharp
var rnd = new Random();

var railwaySemaphore = new Semaphore(2, 2);
for (int i = 0; i < 10; i++)
{
    new Thread(() =>
    {
        // Time to leave the railway station.
        Thread.Sleep(rnd.Next(500, 8000));
        Console.WriteLine(Thread.CurrentThread.Name + " departing.");

        // Time to reach the semaphore next to the track.
        Thread.Sleep(rnd.Next(100, 5000));
        Console.WriteLine(Thread.CurrentThread.Name + " at signal.");

        // Waiting for the first signal.
        // The train is allowed to pass if no two trains are in the segment.
        railwaySemaphore.WaitOne();
        Console.WriteLine(Thread.CurrentThread.Name + " passed signal.");

        // Time to reach the end of the protected railway segment.
        Thread.Sleep(rnd.Next(2000, 4000));
        Console.WriteLine(Thread.CurrentThread.Name + " exited segment.");
        railwaySemaphore.Release();
    }) { Name = "Train " + i }.Start();
}
```

如果信号量工作正常（它确实如此），那么在没有火车先离开该区段的情况下，你不应看到超过两条关于火车通过信号的消息。留给精通 UI 的读者一个练习：实现轨道、信号机以及不同火车在铁路上行驶的图形化可视化。

就像互斥体一样，信号量是暴露给托管代码的内置操作系统原语。在此处展示的代码中，我们一直使用无名称的本地信号量。但是，存在构造函数重载以及静态 OpenExisting 方法，可用于处理命名信号量。例如，此类信号量对象可以跨多个进程使用，以协调共享资源池的使用。

由于它们对操作系统线程调度的影响（在通过 WaitOne 获取信号量时使线程进入等待阻塞状态），你需要考虑一定的开销。为了在特定场景中减少这种开销，.NET 4 中引入了一个名为 SemaphoreSlim 的新类型。它不依赖操作系统级别的信号量概念，开销更低。它特别适合只有一个进程需要保护共享资源的情况，因为该类仅支持本地未命名信号量。换句话说，它是位于公共语言运行时层面、操作系统并不知晓的特性。

一个 API 层面的差异是使用 Wait 方法而不是 WaitOne 方法。实际上，WaitOne 是从 WaitHandle 基类继承而来的（字面意义上），该基类用于各种操作系统级同步原语包装器。SemaphoreSlim 并不是这样的原语，因此它不派生自该类。但是，如果希望使用 WaitHandle 执行等待操作，可以使用 AvailableWaitHandle 属性。我们暂时不详细阐述等待句柄的概念；在“使用事件发出信号”一节的讨论中会更详细地讨论它们。

最后，Semaphore 类不公开信号量的当前计数，而 SemaphoreSlim 类通过 CurrentCount 属性公开该计数。

## 更高级的锁

分别于 .NET 3.5 和 .NET 4 中新增的 ReaderWriterLockSlim 和 SpinLock 原语也常常很有用。它们的用途相当专门化，因此我们将只进行基本讨论。

## ReaderWriterLock(Slim)

各种并发与同步问题的核心问题归结为对共享资源的并发读取和写入访问。通常，允许多个读取器存在，而写入器应彼此保护以防止损害。因此，经典的基于监视器的锁通常过于粗粒度，因为它无法区分读取器和写入器访问。

ReaderWriterLock 和 ReaderWriterLockSlim 可适应此类场景。后者在 .NET 3.5 中引入，推荐使用。读取器/写入器锁的使用仅限于当前进程，并且该锁不包装操作系统提供的功能。在这种情况下，“越精简越好”的口号绝对成立，因此如今建议使用 ReaderWriterLockSlim。我们讨论这个类只是为了让你了解该锁的用法。

从本质上讲，ReaderWriterLockSlim 为不同种类的访问公开成对的 Enter 和 Exit 方法，如下所示：

- **读取模式：** 任意数量的线程可以同时读取；换句话说，允许共享。
- **写入模式：** 只有一个线程可以拥有此独占写入访问权限。处于此模式会因其独占性质而阻止其他线程进入锁。
- **可升级模式是一种特殊的读取模式：** 在未来某个时刻，读取器线程可能决定升级锁以获得写入访问权限。

尝试获取锁的精确行为取决于锁当前所处的状态。MSDN 上的一个表格详细说明了这一点。简而言之，其理念是允许许多读取器，并防止写入器弄乱状态。为此，写入器会阻塞所有试图以任何模式访问该锁的其他线程。另一方面，读取器允许更多读取器进入，除非有写入器正在等待获取访问权限。获取写入访问权限的尝试会阻塞，直到其他所有线程都已离开该锁。

应该提到，存在两类进入方法。一组方法的形式为 Enter 后跟所需的访问级别。这些方法会阻塞，直到请求的访问被允许。TryEnter 系列方法返回布尔值，指示进入锁的请求（可带可选超时）是否成功。

以下代码片段展示了一个读取器/写入器锁的简单示例：

```csharp
var @lock = new ReaderWriterLockSlim();

int counter = 0;
new Thread(() =>
{
    while (true)
    {
        @lock.EnterWriteLock();
        counter++;
        counter--;
        @lock.ExitWriteLock();
    }
}).Start();

while (true)
{
    Thread.Sleep(100);

    @lock.EnterReadLock();
    Console.WriteLine(counter);
    @lock.ExitReadLock();
}
```

这里的主线程充当某个计数器的监视器。许多这样的监视器可以同时观察计数器值而不会造成任何损害。但是，某个后台线程在不断更新计数器。此类更新绝不应在中间的非原子状态下被观察到。因此，我们需要锁。

试着去掉任意一个锁，就会看到计数器不变式被破坏。特别是，计数器绝不应读取到零以外的值，因为递增和递减操作应保持平衡。还鼓励你向其中加入更多读取器和写入器线程，以展示读取器/写入器锁正确保护了对计数器的读取和写入访问。弄乱与某段代码关联的访问级别（对于

