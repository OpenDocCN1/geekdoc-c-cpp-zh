

## 取消任务

当然，你可以使用 `CancellationTokenSource` 来取消任务。首先，我们必须修改 `Sum` 方法，使其接受一个 `CancellationToken`。

```csharp
private static Int32 Sum(CancellationToken ct, Int32 n) {
    Int32 sum = 0;
    for (; n = 0; n < n; n--) {
        // 当对令牌所引用的 CancellationTokenSource 调用 Cancel
        // 时，以下行将抛出 OperationCanceledException
        ct.ThrowIfCancellationRequested();

        checked { sum += n }; // 如果 n 很大，这将抛出 System.OverflowException
    }
    return sum;
}
```

在此段代码中，计算密集操作的循环通过调用 `Cancellation.ThrowIfCancellationRequested` 定期检查操作是否已取消。此方法与之前在“协作取消和超时”部分中显示的 `Task.IsCancellationRequested` 属性相似。但是，如果 `TokenSource` 已被取消，`ThrowIfCancellationRequested` 会抛出 `OperationCanceledException`。抛出异常的原因是，与通过 `ThreadPool.UserWorkItem` 启动的工作项不同，任务具有“已完成”的概念，并且任务可以返回。因此，需要一种方法来区分已完成的任务和已取消的任务，而通过任务异常你可以知道任务没有一直运行到完成。

现在，我们将按照如下方式创建 `CancellationSource` 和 `Task` 对象。

```csharp
CancellationSource cts = new CancellationSource();
Task<Int32> t = Task.Run(() => Sum(cts.Token, 1000000000), cts.Token);
```

```csharp
// 一段时间后，取消 CancellationSource 以取消任务
cts.Cancel(); // 这是一个异步请求，任务可能已经完成了

try {
    // 如果任务被取消，Result 将抛出一个 AggregateException
    Console.WriteLine("The sum is: " + t.Result); // 一个 Int32 结果
} catch (AggregateException x) {
    // 将任何 OperationCanceledException 对象视为已处理。
    // 任何其他异常都会导致抛出一个新的 AggregateException，
    // 该异常仅包含未处理的异常
    x.Handle(e => e is OperationCanceledException);
}

// 如果所有异常都已处理，则执行以下操作
Console.WriteLine("Sum was canceled");
```

在创建任务时，你可以通过将 `CancellationToken` 传递给任务的构造函数（如前面的代码所示）来关联它。如果 `CancellationToken` 在任务调度之前被取消，任务将被取消且永远不会执行。但如果任务已经调度（通过调用 `Start` 方法），如果其操作在执行期间需要被取消，则任务代码必须显式支持取消。遗憾的是，虽然任务对象与其关联了一个 `CancellationToken`，但无法访问它，因此你必须将用于创建任务对象时的同一个 `CancellationToken` 获取到任务代码内部。使用这种方法最简单的方法是通过 Lambda 表达式并将 `CancellationToken` 作为闭包变量“传递”（正如我在上一个示例中做的那样）。

## 在另一个任务完成后自动启动新任务

为了编写可扩展的软件，你不能有线程阻塞。这意味着在任务未运行结束时使用 `Wait` 或查询任务的 `Result` 可能会导致线程池创建一个新线程，这会增加资源消耗并损害性能。坦率地说，有一种更好的方法来发现任务何时完成。当任务完成时，你可以启动另一个任务。这是一段不阻塞任何线程的代码重写。

```csharp
// 创建并启动一个任务，继续执行另一个任务
Task<Int32> t = Task.Run(() => Sum(CancellationToken.Token, 10000));
```

```csharp
// ContinueWith 返回一个 Task，但你并不关心
Task cwt = t.ContinueWith(task => Console.WriteLine("The sum is: " + task.Result));
```

现在，当 `ContinueWith` 开始执行任务时，该任务将启动另一个任务（在某个线程池上）来显示结果。执行代码的线程不会阻塞等待这两个任务中的任何一个完成；线程被允许执行其他代码，或者如果它是线程池线程，它可以返回池以执行其他操作。注意，执行 `Sum` 的任务可能会在调用 `ContinueWith` 之前完成。这不会成为问题，因为 `ContinueWith` 方法将看到 `Sum` 已完成，并立即启动显示结果的任务。

此外，请注意 `ContinueWith` 返回 `Task` 对象的引用（我的代码将其放置在 `cwt` 变量中）。当然，你可以使用此 `Task` 对象调用各种成员（`Wait`、`Result` 或 `ContinueWith`），但通常你会忽略此 `Task` 对象且不在变量中保存它的引用。

我还应该提到，`Task` 对象内部包含一个 `ContinueWith` 集合。因此，你实际上可以使用 `Task` 对象多次调用 `ContinueWith`。当任务完成时，所有的 `ContinueWith` 任务将排入线程池。此外，在调用 `ContinueWith` 时，你可以指定 `TaskContinuationOptions` 的按位或。前六个标志——`None`、`PreferFairness`、`LongRunning`、`AttachedToParent`、`DenyChildAttach`、

顺便说，如果你在任务启动之前尝试取消任务，将抛出 `InvalidOperationException`。

HideScheduler—这与之前显示的 `TaskCreationOptions` 枚举类型提供的标志相同。以下是 `TaskContinuationOptions` 的样子。

```csharp
[Flags, Serializable]
public enum TaskContinuationOptions {
    None = 0x0000,
    PreferFairness = 0x0001,
    LongRunning = 0x0002,
    AttachedToParent = 0x0004,
    DenyChildAttach = 0x0008,
    HideScheduler = 0x0010,
    ExecuteSynchronously = 0x0020,
    LazyCancellation = 0x0040,
    RanToCompletion = 0x0080,
    OnlyFaulted = 0x0100,
    OnlyCanceled = 0x0200,
}
```

