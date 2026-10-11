
```sharp
using System;
using System.Threading;
using System.Threading.Tasks;

namespace TasksWithResults
{
    class Program
    {
        static void Main(string[] args)
        {
            var task1 = Task.Factory.StartNew<int>(() =>
            {
                int result = 0;
                for (int i = 0; i < 1000000; i++) result = i + i%10;
                return result;
            });
            var task2 = Task.Factory.StartNew<double>(() =>
            {
                double result = Math.PI;
                for (int i = 0; i < 10; i++)
                {
                    Thread.Sleep(10);
                    result *= (i+1)*Math.E;
                }
                return result;
            });
            var task3 = Task.Factory.StartNew<string>(() => "The result is: " +
                Console.WriteLine(task1.Result + task2.Result));
            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }
    }
}
```

代码文件 [`Program.cs`] 可在 `Wrox.com` 下载。

三个任务 `task1`、`task2` 和 `task3` 用于通过最后一条语句中的 `Console.WriteLine` 调用计算一个字符串。由于它们是占位计数器，因此非常适合演示。所有任务在实例化后立即启动，这种良好的流程在到达 `Console.WriteLine` 调用时，很有可能 `task1` 和 `task3` 已经完成，但 `task2` 还没有（因为内部有一个 `Thread.Sleep(10)` 调用）。然而，你不需要处理这种情况。`Result` 属性会确保在计算出最终结果之前，每个特定因素都已计算。

# 执行任务

在启动任务后，TPL 负责执行它们。归根结底，每个任务都是在 `System.Threading.ThreadPool` 和 `System.Threading.TaskScheduler` 类的帮助下在工作线程上执行的。TPL 不会为每个任务创建一个线程。它使用了一种更轻级的机制来提供并发性。

通过一个简单的示例更容易理解这种机制的本质。让我们假设一个代码应用程序按顺序创建了两个任务：`Task 1` 和 `Task 2`。随后，当 `Task 2` 运行时，它又创建了另外三个任务，即 `Task 2A`、`Task 2B` 和 `Task 2C`，同样遵循这个顺序。

![](img/b5597c749e848b27b0d305153ae16106_489_0.png)

现在，当 `Task 2` 创建新任务时，这些任务将进入 `WT#N` 的本地队列，而不是全局队列（Global Queue）。假设 `WT#N` 首先完成对 `Task 2` 的处理，稍后，`WT#1` 完成了对 `Task 1` 的处理。工作线程此时并不会停止，也不会变为其他工作项目的可用状态！图 10-20 显示了接下来发生了什么。

# CLR 线程池

![](img/b5597c749e848b27b0d305153ae16106_490_0.png)

图 10-20：工作窃（Work-stealing）

现在，`WT#N` 的本地队列不是空的；有三个任务等待执行。该线程从队列中取出 `Task 2C`（就像队列是一个栈一样）并开始执行它。但 `Task 2C` 是最新创建的任务，它在 `Task 2A` 和 `2C` 之后被放入本地队列的。为什么 `WT#N` 选取这一个而不是 `Task 2A`？原因是性能——因为 `Task 2C` 比 `Task 2A` 创建得晚，更有可能 `Task 2C` 的更多资源已缓存到内存中，供 `Task 2A` 的资源使用。

当 `WT#1` 完成时（稍晚于 `WT#N`），它发现自己的本地队列是空的。然而，它也查看了本地队列，发现 `WT#N` 的队列中有两个任务。`WT#1` 从 `WT#N` 的本地队列中“窃取”了 `Task 2A` 并开始执行。这被称为“工作窃”（work-stealing）术语。“被窃取”的任务是有意地从队列头部取出的，否则就是出于性能考虑。

如果 `WT#N` 完成 `Task 2C` 的时间早于 `WT#1` 完成 `Task 2A`，`WT#N` 将抓取 `Task 2B` 执行；否则，`WT#1` 将窃取它。

# 与任务相关的类型

有几种类型可以帮助你处理与任务相关的活动；它们大多数位于 `System.Threading.Tasks` 命名空间中。表 10-4 列出了它们并附有简要描述。

## 表 10-4：并发集合类

| TYPE NAME | DESCRIPTION |
|---|---|
| `Task` | 此类表示一个异步操作，并实现了之前讨论的任务抽象。 |
| `Task<TResult>` | 此类表示一个返回 `TResult` 类型的任务。 |
| `TaskCanceledException` | 此异常用于通信任务已取消。通过其 `Task` 属性可以访问已取消的任务。 |
| `TaskCompletionSource<TResult>` | 此类作为 `Task<Result>` 的生产者。 |
| `TaskFactory`, `TaskFactory<Result>` | 这些类提供了创建和调度任务的支持。其方法如 `StartNew`、`ContinueAll`、`ContinueAny`、`FromAsync` 以及泛型。 |
| `TaskScheduler` | 此类表示一个负责将任务调度到线程的对象。 |

# 协调数据结构

.NET Framework 4.0 引入了若干用于并行编程的新类型。这些类型被 TPL 和 PLINQ 执行引擎大量使用。它们仅供内部使用。此外，鼓励将它们构建到并发算法中这些类型可以分为以下几类：

- 并发集合类 —— `System.Collections.Concurrent` 中的集合类提供了线程安全的添加和删除操作。
- 同步原语 —— `System.Threading` 命名空间有了新的同步原语，通过避免遗留多线程代码中的昂贵锁实现了细粒度并发和更高的性能。
- 懒初始化类 —— 这些类帮助你将自定义类型封装在“懒”类中，直到需要时才分配内存和资源。
- 取消原语 —— 多线程中最困难的事情之一就是正确取消。取消原语可以帮助简化这一点。

## 表 10-5（续）

| 类型名称 | 描述 |
| --- | --- |
| `ConcurrentBag<T>` | 此类表示一个线程安全的、无序的对象的集合。当线程既产生又消费存储在包中的数据时，可以使用 `ConcurrentBag<T>`，因为 `ConcurrentBag<T>` 的性能针对此类场景进行了优化。 |
| `ConcurrentDictionary<TKey, TValue>` | 此类表示一个线程安全的键值对集合，可以被多个线程并发访问。你可以轻松地使用 `Dictionary<TKey, TValue>`，因为它实现了相同的语义。与 `Dictionary<TKey, TValue>` 相比，该类的内部实现在小字典和大字典中都为多线程提供了远比其无法实现的得优异的扩展性。 |
| `ConcurrentQueue<T>` | 此类表示一个线程安全的先进先出（FIFO）集合。 |
| `ConcurrentStack<T>` | 此类表示一个线程安全的后进先行（LIFO）集合。 |

除了 `ConcurrentDictionary<TKey, TValue>` 外，所有其他类都实现了 `IProducerConsumerCollection<T>` 接口，该接口表示一个允许线程安全添加和删除数据的集合。

# 同步原语

`System.Threading` 命名空间包含了新的类型，避免了遗留多线程代码中昂贵的锁定机制。这些类型大部分是轻量级的，并且与 .NET Framework 中的前身相比，能够实现细粒度的并发和更高的性能。

表 10-6 列出了这些同步原语。

## 表 10-6：同步原语

| 类型名称 | 描述 |
| --- | --- |
| `Barrier` | 此类是新建的，在之前的 .NET Framework 版本中没有前身。`Barrier` 允许多个任务通过多个阶段协作并行执行某种算法。你可以使用此类来管理一组任务，让它们通过通过一系列阶段来协作，其中组中的每个任务都会信号它已到达给定阶段的 `Barrier`，并隐含地等待其他人的到达。 |
| | 生活中的一个例子是公司车辆从西雅图开往迈密，横跨整个美国。司机们并没有护队行驶，而是约定了几个点（假设是丹佛和休斯顿），让他们在那里互相等待。当所有人到达这些屏障时，他们就开始开始路线的下一段。同一个 `Barrier` 实例可以用于多个阶段。 |
| `CountdownEvent` | 此类表示一种同步原语，当其计数达到零时发出信号。你可以在分叉与合并（fork-and-join）场景中使用它，因为它提供了一个易用的汇合机制。`CountdownEvent` 允许等待一个或多个线程完成某些其他操作。该类的实例用一个整数计数初始化，通常大于 0。线程在事件上阻塞等待，直到计数达到 0，此时计数将通过 `CountdownEvent` 的 `Decrement` 方法递减，该方法通常由完成某项（被事件跟踪的）工作单元的工作线程调用。 |
| `ManualResetEventSlim` | 此类型是其前身 `ManualResetEvent` 的精简版和轻量级版本，可以通知一个或多个等待的线程事件已发生。精简的代价是，你只能将 `ManualResetEventSlim` 实例用于进程内通信。 |
| `SemaphoreSlim` | 这种轻量级类可以用于限制访问资源或资源池的线程数量。它有一个由 .NET 2.0 引入的前身 `Semaphore`。然而，`Semaphore` 利用了 Windows 内核信号量，而 `SemaphoreSlim` 则没有。 |
| `SpinLock`, `SpinWait` | 这些同步原语允许线程等待。当预计等待时间很短时，它们通过避免昂贵的上下文切换和阻塞操作来提高性能。`SpinLock` 是一种互斥锁，它会导致获取锁的线程在循环中（或自旋）等待一段时间，然后让出其时间片。`SpinLock` 是一个值类型，出于性能考虑，当你传递 `SpinLock` 实例时，它应该按引用传递，而不是按值传递。`SpinWait` 是一个微小的轻量级类型，它会自旋指定的时间，如果超过计数，最终会将线程放入等待状态。`SpinWait` 是一个值类型；其成员不是线程安全的。如果多个线程自旋，每个线程都应该使用自己的 `SpinWait` 实例。 |

这些同步原语在 TPL（任务并行库）实现中起着重要作用。它们被频繁使用，并对 TPL 的卓越性能做出了巨大贡献。

# 延迟初始化类

将类型成员的初始化推迟到需要时是一种常用的编程模式。当通过消耗 CPU 周期、内存或其他资源进行初始化开销昂贵时，这种模式尤为有用。表 10-7 列出的延迟初始化类可以帮助应对这些场景。

**表 10-7：延迟初始化类型**

| 类型名称 | 描述 |
| --- | --- |
| `System.Lazy<T>` | 此类为 `T` 实例的延迟提供了支持。当你创建一个 `Lazy<T>` 实例时，它不会实例化 `T`。你可以通过其 `Value` 属性访问 `Lazy<T>` 后面的实例。延迟初始化发生在第一次访问 `Lazy<T>.Value` 属性或调用 `Lazy<T>.ToString` 方法时。 |
| `System.Threading.LazyInitializer` | 此静态类提供了延迟初始化例程。在 .NET Framework 4.0 中，你可以使用 `EnsureInitialized` 方法的几个重载。在未来，该类可能会扩展更多的辅助方法。在可能延迟初始化多个对象的场景下，你可能认为将每个对象封装在 `Lazy<T>` 中需要过多的内存或计算资源。或者，你对如何暴露延迟初始化有严格的要求。在这种情况下，你可以使用静态的 `EnsureInitialized` 方法进行延迟初始化，而无需将其封装在实例中。 |
| `System.Threading.ThreadLocal<T>` | 此类提供类型 `T` 的线程本地存储。虽然该类的实现实现了延迟初始化，但“延迟性”并不是它的主要功能。通过提供 `ThreadLocal<T>` 实例，可以确保通过 `Value` 属性访问的实例在创建它的线程共享。它的角色类似于用于装饰字段的 `ThreadStatic` 特性。然而，ThreadLocal 提供了更好的性能。 |

# 取消原语

如果你知道这有多复杂。TPL 提供了几个类型来简化取消的复杂性。表 10-8 中列出的原语可以使用任务、PLINQ 表达式和并行循环。

## 表 10-8：取消原语

| 类型名称 | 描述 |
| --- | --- |
| `CancellationToken` | 此结构传播操作应被取消的通知。你可以将 `CancellationToken` 实例传递给阻塞调用，如 `BlockingCollection.Add(..)`、`BlockingCollection.Take(..)`、`ManualResetEventSlim.Wait(..)`、`Task.Wait(...)` 和 `Task.WaitAll(...)`。这些方法具有接受 `CancellationToken` 实例的重载，并在发生取消时完成。 |
| `CancellationTokenSource` | 此类信号操作应被取消。你可以将它作为协作取消场景中的指挥官。你可以将 `CancellationTokenSource` 的 `Token` 传递给接受它的方法。当调用 `Cancel` 方法时，属于该 `CancellationTokenSource` 实例的所有实例都将收到通知。 |

# 代码契约

现代软件架构使用具有精确边界和定义良好的职责的层和组件。没有这种方法，很难编写高质量的软件。组件之间的协作通常由契约定义。对于许多开发者来说，契约就是接口（接口类）以及组件用于通信表面的相关数据对象或实定义。例如，假设你正在开发仓库管理软件，其中一个接口是 `WarehouseService`，一个相关的实体是：

```csharp
public class WarehouseService
{
    public void QueueOrder(Order order)
    {
        // ...
    }
}
```

public class Order

```

```

{

    public string CustomerName { get; set; }

    public int ProductId { get; set; }

    public int Quantity { get; set; }

}

```

遗憾的是，这两个类存在问题。当你看到它们的定义并想要使用它们时，你必须向架构师（甚至是开发者）提一些关于这些类的问题才能成功使用它们。以下是你可能会问的一些问题：

- 如果向 `QueueOrder` 方法传递 `null` 会发生什么？你可能假设它抛出一个 `ArgumentNullException`，但你无法确定。
- 如果 `Order` 的 `ColumnName` 属性为 `null` 或空字符串怎么办？在这种情况下订单仍然有效吗？
- 如果 `Order` 的 `Quantity` 属性为负数怎么办？这是否意味着实际上有一个产品返回到了仓库？它可以为零吗？

如果有一种方式可以像合约签名一样以任何明确的方式描述 `QueueOrder` 方法的行为，那么这些问题就没必要了。实际上，这些问题的答案将成为定义 `WarehouseService` 行为的合约的一部分。

一种较新的 .NET Framework 方法——**代码契约（code contracts）编程**出现了。

代码契约背后的思想是：类和方法应该显式声明它们需要什么、保证什么以及当满足这些需求时会发生什么。这种做法最早由 Bertrand Meyer 通过 Eiffel 编程语言引入，微软研究院也有一个名为 Spec# 的项目，它带有一种用于 API 契约的正式语言（受 Eiffel、JML 和 Asml 语言的影响）。这些契约不仅是人类可读的，还可以被执行运行时检查或验证的工具捕获，或者可能将它们包含在生成的文档中。

# 理解代码契约系统

在 .NET Framework 4.0 中使用代码契约涉及两个部分。第一部分是**代码契约库**。契约使用 `System.Diagnostics.Contracts` 命名空间中 `Contract` 类定义的静态方法调用进行编码。契约是声明性的，你方法中的这些静态调用可以被视为方法签名的一部分。例如，之前考虑的 `QueueOrder` 方法可以扩展几个声明性契约：

```csharp
public void QueueOrder(Order order)
{
    Contract.Requires(order != null);
    Contract.Requires(order.Quantity > 0);
    // ...
}
```
