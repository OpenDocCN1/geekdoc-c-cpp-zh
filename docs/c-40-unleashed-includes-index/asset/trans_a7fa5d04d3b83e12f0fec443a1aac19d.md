

## 任务的取消

在异步代码领域（以及其他线程和同步构造等）中，取消操作的方法一直是一个众所周知的难题。从 .NET 4 开始，取消操作被统一为两个概念：CancellationToken 和 CancellationTokenSource。

我们在此不详细讨论该机制的复杂性，而是专注于这个功能的基本要点。图 30.6 总结了用于取消的构造之间的基本交互。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1552_0.png)

图 30.6 任务的取消

第一个关键概念是 CancellationTokenSource。这个类通过调用 Cancel 来发出取消请求。被取消的操作可以通过所谓的 CancellationToken 结构来检查这一情况，该结构可以使用只读的 Token 属性从令牌源中获取。从 .NET 4 开始，这个轻量级对象可以传递给 TPL 和 System.Threading API 中的各种位置。在本章前面的“检索任务结果”一节中，你已经看到 Task 上的 Wait 方法如何接受 CancellationToken，从而允许取消该操作。

请注意，任务的取消是以协作方式完成的。与 Thread.Abort 方法（会抛出异步的 ThreadAbortException）不同，取消令牌仅仅表示一个标志，任务应定期检查该标志，以便在发现取消请求时退出任务代码。任务既可以使用令牌上的 IsCancellationRequested 属性，也可以通过调用 ThrowIfCancellationRequested 来实现这一点。后一种方法会抛出 OperationCanceledException，从而终止任务。显然，在等待任务或从延续函数中观察时，可以看到这个错误。

当任务中发生等待操作时，应该将同一个令牌传递给这些等待操作，以便取消也能解除这些等待操作的阻塞。由于取消的协作性质，取消被批准可能需要一段时间。这也要求任务代码以足够频繁的节奏检查取消请求。

下面展示了一个任务取消支持的示例：

```
var cts = new CancellationTokenSource();
var ct = cts.Token;

Task.Factory.StartNew(() =>
{
    while (true)
    {
        // Alternatively, ThrowIfCancellationRequested could be used,
        // requiring the caller to handle this case.
        if (ct.IsCancellationRequested)
            return;

        Console.WriteLine(DateTime.Now);
        Thread.Sleep(1000);
    }
}, ct);

Console.WriteLine("Press ENTER to stop the clock...");
Console.ReadLine();
cts.Cancel();

Console.WriteLine("Clock stopped");
Console.ReadLine();
```

在这段代码中，我们使用 IsCancellationRequested 属性来检查取消请求，并通过停止任务来处理该请求。使用这种技术，任务的状态不会转换为 Canceled，而是以 RanToCompletion 结束，因为它是正常终止的。这通常就足够了。然而，如果任务的所有者或延续需要检查已取消状态，那么抛出 OperationCanceledException 就是合适的方法。

这种模式的一个示例如下：

```
if (ct.IsCancellationRequested)
{
    // Do cleanup if necessary (if none, the if-check can be omitted).
    ct.ThrowIfCancellationRequested();
}
```

## 并行调用

在许多情况下，调用单个任务就足够了，但通过运行多个任务来实现并行通常也很有意义。虽然我们可以简单地创建多个任务，但 TPL 中存在一些更高层次的抽象。其中一种抽象是 Parallel.Invoke，它接受一个 Action 委托数组并行调用。你可以认为每个这样的操作都会导致创建一个任务。只有所有任务都完成后，Parallel.Invoke 调用才会返回。尽管如此，由于调度的工作方式，Parallel.Invoke 并不保证这些操作真正并行运行。（同一个工作者可能会处理所有操作，导致它们顺序执行。）

下面是 Parallel.Invoke 的一个示例：

```
Parallel.Invoke(
    () => Console.WriteLine("First task"),
    () => Console.WriteLine("Second task"),
    () => Console.WriteLine("Third task")
);
```

Invoke 方法的另一个重载首先接受一个 ParallelOptions 参数，该参数可用于指定一些选项。其中之一是并行度，用于限制执行工作而生成的最大并行工作者数量。另一个选项是取消令牌，其作用不言自明。

事实上，Parallel 类是任务并行与数据并行交汇的地方。本节只介绍 Invoke 方法，它更接近任务并行而非数据并行。在本章后面的“数据并行”一节中，我们将研究 Parallel 类上以静态方法形式公开的并行循环构造。

关于一个或多个任务中发生错误的情况，你可能已经猜到这些错误是如何呈现给 Parallel.Invoke 的调用者的。AggregateException 再一次成为你最好的朋友。类似地，并行调用工作的取消可能导致 OperationCanceledException 被包装在 AggregateException 内。

## 等待多个任务

前面部分展示的 Parallel.Invoke 方法将我们引向了 TPL 中一个有趣的设施。你看到它与常规任务相比最重要的一个区别了吗？就在这里：虽然传递给 Parallel.Invoke 的各个工作片段可以使用异步任务并行运行，但整体上是同步的。也就是说，Parallel.Invoke 要等到其所有操作都已执行（或发生某些错误或取消）后才会返回。

如果你仔细阅读了第 29 章，你可能会立刻想到一种在多个并行操作之间实现这种同步行为的方法。使用诸如 ManualResetEvent 之类的事件，甚至使用（.NET 4 中新增的）CountDownEvent 概念怎么样？

虽然这种技术可行，但要正确实现却相当困难（尤其是当错误和取消也掺杂其中时）。此外，如果处理不慎，由于某些等待原语是构建在 Win32 同步设施之上的底层结构，可能会引发昂贵的上下文切换。

幸运的是，TPL 提供了 WaitAll 和 WaitAny 构造，使我们能够等待多个任务的完成（要么等待所有任务完成，要么至少一个任务完成）。下面是一个简单的类似 Parallel.Invoke 的实现的示例：

```csharp
static void Main()
{
    var cts = new CancellationTokenSource();
    ParallelInvoke(cts.Token,
        () => Console.WriteLine("First task"),
        () => Console.WriteLine("Second task"),
        () => Console.WriteLine("Third task")
    );
}
```

```csharp
static void ParallelInvoke(CancellationToken ct, params Action[] actions)
{
    var tasks = (from action in actions
                 select Task.Factory.StartNew(action, ct))
                .ToArray();

    Task.WaitAll(tasks, ct);
}
```

为了演示，我加入了一种方法，将一个取消令牌贯穿于 WaitAll 调用和所有生成任务的 StartNew 调用中。这展示了 Task 上的 WaitAll 方法的一个重载。

WaitAll 的其他重载允许指定超时，而取消令牌的使用是可选的（和通常一样）。任何子任务中的错误都会集中出现在 WaitAll 调用抛出的 AggregateException 中。

WaitAny 方法也应该是不言自明的，尤其是如果你之前接触过 WaitHandle 上的等价方法。这些方法返回一个整数值，表示数组中已完成任务的索引。存在接受超时值或取消令牌的重载。取消令牌在整个 TPL API 中的存在，是与使用 WaitHandle 对象进行同步的经典方法之间的关键区别之一。以前，经常看到将虚拟事件传递给 Wait 方法以允许它们解除阻塞的情况：

```csharp
WaitHandle cancel = new ManualResetEvent(false);
// Assume other events exist
```

