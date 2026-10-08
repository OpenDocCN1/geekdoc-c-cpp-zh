
此方法基本上将 `ParallelQuery<T>` 转回 `IEnumerable<T>`，以便调用 `AsSequential` 之后执行的操作由一个线程执行。

通常，LINQ 查询产生的数据是通过某些 `foreach` 语句（如前文所示）求值的。这意味着只有一个线程迭代了查询的所有结果。如果你希望并行处理查询的结果，那么你应该使用 `ParallelEnumerable.ForAll` 处理结果查询：

```csharp
static void ForAll<TSource>(ParallelQuery<TSource> source, Action<TSource> body)
```

（注：提供的 OCR 文本在最后部分存在重复/损坏，我已在保持提供内容的基础上修复了结构错误。）

## 第 26 章 计算密集型异步操作 747

这些选项基本上允许你对速度和内存消耗进行某些控制。**NotBuffered**（不缓冲）节省内存但处理速度较慢。**FullyBuffered**（全缓冲）运行速度最快但消耗更多内存。**AutoBuffered**（自动缓冲）是 **NotBuffered** 和 **FullyBuffered** 之间的折中。实际上，对于任何给查询，选择哪种的最佳方法是尝试所有选项并比较性能结果，或者直接接受默认值，它通常对许多查询效果良好。关于 Parallel LINQ 如何跨 CPU 核心分区的更多信息，请参阅以下博客：

- http://blogs.msdn.com/pfxteam/archive/2009/05/28/9648672.aspx
- http://blogs.msdn.com/pfxteam/archive/2009/06/13/9741072.aspx

## 实现周期性计算密集型操作

`System.Threading` 命名空间定义了一个 `Timer` 类，你可以使用它让线程池定期调用线程。当你构造 `Timer` 类的实例时，你是在告诉线程池，你有一个方法将在你指定的未来时间被调用。`Timer` 类提供了几个构造函数，它们彼此之间非常相似：

```
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Timer(TimerCallback callback, Object state, Int32 dueTime, Int32 period);
    public Timer(TimerCallback callback, Object state, UInt32 dueTime, UInt32 period);
    public Timer(TimerCallback callback, Object state, Int64 dueTime, Int64 period);
    public Timer(TimerCallback callback, Object state, TimeSpan dueTime, TimeSpan period);
}
```

所有四个构造函数构造 `Timer` 的方式是完全相同的。`callback` 参数标识你希望由线程池调用的方法。当然，你写的回调方法必须匹配 `System.Threading.TimerCallback` 委托类型，其定义如下：

```
delegate void TimerCallback(Object state);
```

构造函数的 `state` 参数允许你在每次调用回调方法时向其传递状态数据；如果你没有状态要传递，则使用 `null`。你使用 `dueTime` 参数来告诉 CLR 在第一次调用你的回调之前等待多少毫秒。你可以通过有符号或无符号的 32 位值、有符号的 64 位值或 `TimeSpan` 值来指定毫秒数。如果你希望立即调用回调方法，请为 `dueTime` 参数指定 `0`。最后一个参数 `period` 允许你指定在每次连续调用回调方法之前等待多少毫秒。如果你为该参数传递 `Timeout.Infinite (-1)`，则线程池将只调用一次回调方法。

在内部，线程池有一个线程供所有的 Timer 对象使用。该线程知道下一个 Timer 对象何时到期。当下一个 Timer 对象到期时，该线程会被醒并调用 `Thread::QueueUserWork` 在线程池队列中插入一个条目，在指定时间执行你的回调方法，此时计时器触发。这可能会导致多个线程同时执行你的回调方法。为了解决这个问题，我建议采取以下措施：构造 Timer 时为 period 参数指定 `Timeout.Infinite`。现在，计时器将只触发一次。在你的回调中，调用 `Change` 方法并指定新时间，同时再次为 period 参数指定 `Timeout.Infinite`。以下是 `Change` 方法重载的形式：

```
public sealed class Timer : MarshalByRefObject, IDisposable {
  public Boolean Change(Int32 due, Int32 period);
  public Boolean Change(UInt32 due, UInt32 period);
  public Boolean Change(Int64 due, Int64 period);
  public Boolean Change(TimeSpan due, TimeSpan period);
}
```

Timer 还有一个 `Dispose` 方法，允许在等待的回调完成时取消计时器，并可选地通过 `notifyObject` 参数信号内核对象。Dispose 方法重载如下：

```
public sealed class Timer : MarshalByRefObject, IDisposable {
  public Boolean Dispose();
  public Boolean Dispose(WaitHandle notifyObject);
}
```

> **重要** 当 Timer 对象被垃圾回收时，其终结代码会告诉线程池取消计时器使其不再触发。使用 Timer 对象时，请确保有一个变量保持 Timer 活动，否则你的回调方法将停止调用。这在第 21 章的“垃圾收集与调试”部分进行了讨论和演示。

以下代码演示了如何让线程池线程立即调用一个方法，然后在 2 秒后再次调用：

```
internal static class TimerDemo {
  private static Timer s_timer;
  public static void Go() {
    Console.WriteLine("Main thread: starting the timer");
    using (s_timer = new Timer(ComputeBoundOp, 5, 0, Timeout.Infinite)) {
      Console.WriteLine("Main thread: Doing other work...");
      Thread.Sleep(10000); // 模拟 10 秒的工作
    } // 现在取消计时器
  }
  // 此方法的签名必须匹配 TimerCallback 委托
  private static void ComputeBoundOp(Object state) {
      // 此方法由线程池执行
      Console.WriteLine("ComputeBoundOp: " + state);
      Thread.Sleep(1000); // 模拟工作
      // 工作完成后，让计时器在 2 秒后再次触发
      s_timer.Change(2000, Timeout.Infinite);
  }
}
```

## 748 线程

在内部，线程池有一个线程供所有的 Timer 对象使用。该线程知道下一个 Timer 对象何时到期。当下一个 Timer 对象到期时，该线程会被醒并调用 `Thread::QueueUserWork` 在线程池队列中插入一个条目，在指定时间执行你的回调方法，此时计时器触发。这可能会多个线程同时执行你的回调方法。为了解决这个问题，我建议：构造 Timer 时为 period 参数指定 `Timeout.Infinite`。现在，计时器将只触发一次。在你的回调中，调用 `Change` 方法并指定新时间，同时再次为 period 参数指定 `Timeout.Infinite`。以下是 `Change` 方法重载的形式：

```
public sealed class Timer : MarshalByRefObject, IDisposable {
  public Boolean Change(Int32 due, Int32 period);
  public Boolean Change(UInt32 due, UInt32 period);
  public Boolean Change(Int64 due, Int64 period);
  public Boolean Change(TimeSpan due, TimeSpan period);
}
```

Timer 还有一个 `Dispose` 方法，允许在等待的回调完成时取消计时器，并可选地通过 `notifyObject` 参数信号内核对象。Dispose 方法重载如下：

```
public sealed class Timer : MarshalByRefObject, IDisposable {
  public Boolean Dispose();
  public Boolean Dispose(WaitHandle notifyObject);
}
```

> **重要** 当 Timer 对象被垃圾回收时，其终结代码会告诉线程池取消计时器使其不再触发。使用 Timer 对象时，请确保有一个变量保持 Timer 活动，否则你的回调方法将停止调用。这在第 21 章“自动内存管理（垃圾收集）”部分进行了讨论和演示。

（后续后续重复内容已省略）

## 第 26 章 计算密集型异步操作

`System.Threading.ThreadPool` 类提供了静态方法，你可以调用这些方法来操作线程池中的线程数量：`GetMaxThreads`、`SetMaxThreads`、`GetMinThreads`、`SetMinThreads` 和 `GetAvailableThreads`。我建议你不要调用这些任何一个方法。调整线程限制通常会导致应用程序性能变差，而不是更好。如果你认为你的应用程序需要数百或数千个线程，那么你的应用程序架构以及使用线程的方式就存在严重问题。本章和第 27 章将演示使用线程的正确方法。

### 工作线程是如何被管理的

图 26-1 显示了构成分线程池工作线程部分的各种数据结构。`ThreadPool.QueueUserItem` 和 `Timer` 类总是将项推入全局队列。工作线程使用先进先出（FIFO）算法从该队列中拉取项并对其进行处理。由于多个工作线程可以同时从全局队列中移除项，因此所有工作线程都在线程同步锁上竞争，以确保不会两个或多个线程获取同一个工作项。这种线程同步锁在某些应用程序中可能会成为瓶颈，从而某种程度上限制了可扩展性和性能。

![](img/0ba8f96d6619cf5f73315fb4561d09b5_768_0.png)

图 26-1 CLR 线程池

现在让我们谈谈使用默认 TaskScheduler 调度的 Task 对象。当非工作线程调度 Task 时，该 Task 会被添加到全局队列。但是，每个工作线程都有自己的队列，当工作线程调度 Task 时，该 Task 会被添加到调用线程的本地队列中。

> 其他派生自 TaskScheduler 的对象可能会表现出与我在此描述不同的行为。

## 第五部分 多线程

当工作线程准备好处理某项时，它总是会检查其本地队列是否存在 Task。如果存在 Task，工作线程会从其本地队列中移除 Task 并处理该项。注意，工作线程使用后进先出（LIFO）算法从其本地队列拉取任务。由于工作线程是唯一允许访问其本地队列头的线程，因此不需要线程同步，从队列中移除 Task 的速度很快。这种行为的副作用是 Task 的执行顺序与它们入队列的顺序相反。

> **重要** 线程池从未保证入队列项的处理顺序，尤其是当多个线程同时处理项时。然而，这种副作用加剧了这个问题。你必须确保应用程序对工作项或 Task 的执行顺序没有任何预期。

如果工作线程发现本地队列为空，该工作线程将尝试从另一个工作线程的本地队列中“偷取” Task。Task是从本地队列的尾部偷取的，这需要获取线程锁，这会稍微损害性能。希望是偷取很少发生，因此该锁很少被获取。如果所有队列都为空，工作线程将通过 FIFO 算法从全局队列中提取项（获取其锁）。如果全局队列为空，工作线程将进入睡眠等待新项出现。如果它睡眠了很长时间，它将醒来并销毁自己，允许系统回收该线程使用的资源（内核对象、堆栈、TEB）。

线程池会快速创建工作线程，使得工作线程的数量等于传递给 `ThreadPool.SetMinThreads` 方法的值。如果你从未调用过此方法（我建议你这样做），默认值等于你的进程根据进程亲和性（affinity）允许使用的 CPU 数量。通常你的进程被允许使用机器上所有的 CPU，因此线程池将快速创建多达机器 CPU 数量的线程。在创建许多线程后，线程池会监控工作项的完成率，如果项需要很长时间才能完成（其含义未文档），它将创建更多工作线程。如果项启动很快，则工作线程将被销毁。

### 缓存行与伪共享

为了提高重复访问内存的性能，今天的 CPU 拥有片上缓存内存。访问这种内存的速度极快，尤其是与 CPU 访问主板的速度相比。当线程第一次读取内存中的值时，CPU 从主板内存中获取该值并将其存储在 CPU 的片上缓存中。然而，从 CLR 版本 4 开始，在 64 位进程中运行时，最多使用 64 个 CPU，而在 32 位进程中运行时，最多使用 32 个 CPU。

事实上，为了提高性能，CPU 逻辑上将所有内存被划分为所谓的“缓存行”（cache line）。对于我电脑中的 CPU 来说，一个缓存行由 64 字节组成，因此 CPU 从 RAM 中获取并存储 64 字节大小的块块。因此，如果你的应用程序需要读取一个 Int32 值，包含该 Int32 的 64 字节将被全部获取。获取比需要的内容更多通常会导致性能提升，因为大多数应用程序倾向于访问存储在应用程序已访问的数据周围的数据。这些相邻数据现在将位于 CPU 缓存中，避免了访问 RAM。

然而，如果两个或多个核心访问同一个缓存中的字节，那么核心之间将相互通信并有效地将缓存行从一个核心传递到另一个核心，导致多个核心没有同时操作相邻字节。这会对你的计算密集型任务的性能产生糟糕的影响。让我用代码代码演示这一点：

```csharp
internal class FalseSharing
{
    // 这些字段是相邻的，并且最可能在同一条缓存行中
    public Int32 field1;
    public Int32 field2;
    static const Int32 iterations = 10000000;
    static long s_operations;
    static long sStartTime;
    public static void Main()
    {
        Data data = new Data();
        sStartTime = Stopwatch.GetTimestamp();
        ThreadPool.QueueUserItem(() => AccessData(data));
        ThreadPool.QueueUserItem(() => AccessData(data));
        while (Interlocked.Decrement(ref s_operations) > 0)
        {
        }
        Console.WriteLine("Access time: {0}", Stopwatch.GetTimestamp() - sStartTime);
    }
    private static void AccessData(Data data)
    {
        for (int x = 0; x < iterations; x++)
        {
            if (x % 2 == 0)
            {
                data.field1++;
            }
            else
            {
                data.field2++;
            }
        }
    }
}
class Data
{
    public Int32 field1;
    public Int32 field2;
}
```

当我在我的机器上运行它时，得到的结果是 15856074 毫秒。现在，让我们修改 Data 类使其如下所示：

```csharp
[StructLayout(LayoutKind.Explicit)]
class Data
{
    // 现在这些字段被分开了，不再位于同一缓存行中
    [FieldOffset(0)] public Int32 field1;
    [FieldOffset(64)] public Int32 field2;
}
```
