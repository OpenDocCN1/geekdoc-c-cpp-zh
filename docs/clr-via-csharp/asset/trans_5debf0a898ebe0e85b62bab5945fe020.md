

```csharp
internal static class CancellationDemo {
    public static void Go() {
        CancellationTokenSource cts = new CancellationTokenSource();

        // Pass the CancellationToken and the number-to-count-to into the operation
        ThreadPool.QueueUserWorkItem(o => Count(cts.Token, 1000));

        Console.WriteLine("Press <Enter> to cancel the operation.");
        Console.ReadLine();
        cts.Cancel(); // If Count returned already, Cancel has no effect on it
        // Cancel returns immediately, and the method continues running here...
    }

    private static void Count(CancellationToken token, Int32 countTo) {
        for (Int32 count = 0; count < countTo; count++) {
            if (token.IsCancellationRequested) {
                Console.WriteLine("Count is cancelled");
                break; // Exit the loop to stop the operation
            }

            Console.WriteLine(count);
            Thread.Sleep(200); // For demo, waste some time
        }
        Console.WriteLine("Count is done");
    }
}
```

> **注意** 如果你希望执行一个操作并阻止其被取消，你可以将调用 `CancellationToken` 的静态 `None` 属性所返回的 `CancellationToken` 传递给该操作。此属性返回一个特殊的 `CancellationToken` 实例，它不与任何 `CancellationTokenSource` 对象关联（其私有字段为 `null`）。由于没有 `CancellationTokenSource`，所以没有代码能调用 `Cancel`，而查询这个特殊 `CancellationToken` 的 `IsCancellationRequested` 属性的操作将始终得到 `false`。如果你使用这些特殊 `CancellationToken` 实例之一查询 `CancellationToken` 的 `CanBeCanceled` 属性，该属性将返回 `false`。对于通过查询 `CancellationTokenSource` 对象的 `Token` 属性而获得的所有其他 `CancellationToken` 实例，该属性返回 `true`。

如果你愿意，可以注册一个或多个在 `CancellationTokenSource` 被取消时调用的方法。不过，你使用 `CancellationToken` 的 `Register` 方法来注册每个回调方法。向此方法传递一个 `Action<Object>` 委托、一个将通过该委托传给回调的状态值，以及一个 `Boolean`，用于指示是否使用调用线程的 `SynchronizationContext` 来调用该委托。如果为 `useSynchronizationContext` 参数传递 `false`，那么调用 `Cancel` 的线程将按顺序调用所有已注册的方法。如果为 `useSynchronizationContext` 参数传递 `true`，那么回调会被发送（而不是张贴）到捕获的 `SynchronizationContext` 对象，由该对象决定哪个线程调用回调。`SynchronizationContext` 类将在第 27 章的“应用程序及其线程模型”一节中进一步讨论。

最后，你可以通过链接一组其他 `CancellationTokenSource` 对象来创建一个新的 `CancellationTokenSource` 对象。当任意一个被链接的 `CancellationTokenSource` 对象被取消时，这个新的 `CancellationTokenSource` 对象也会被取消。以下代码演示了这一点：

```csharp
// Create a CancellationTokenSource
var cts1 = new CancellationTokenSource();
cts1.Token.Register(() => Console.WriteLine("cts1 canceled"));

// Create another CancellationTokenSource
var cts2 = new CancellationTokenSource();
cts2.Token.Register(() => Console.WriteLine("cts2 canceled"));

// Create a new CancellationTokenSource that is canceled when cts1 or cts2 is canceled
var linkedCts = CancellationTokenSource.CreateLinkedTokenSource(cts1.Token, cts2.Token);
linkedCts.Token.Register(() => Console.WriteLine("linkedCts canceled"));

// Cancel one of the CancellationTokenSource objects (I chose cts2)
cts2.Cancel();

// Display which CancellationTokenSource objects are canceled
Console.WriteLine("cts1 canceled={0}, cts2 canceled={1}, linkedCts={2}",
    cts1.IsCancellationRequested, cts2.IsCancellationRequested,
    linkedCts.IsCancellationRequested);
```

当我运行上述代码时，得到以下输出：

```
linkedCts canceled
cts2 canceled
cts1 canceled=False, cts2 canceled=True, linkedCts=True
```

## 任务

调用 `ThreadPool` 的 `QueueUserWorkItem` 方法来启动异步的计算密集型操作非常简单。然而，这种技术有许多限制。最大的问题是，没有内置方式让你知道操作何时完成，也没有办法在操作完成时取回返回值。为了解决这些限制及其他问题，Microsoft 引入了**任务**的概念，你可以通过 `System.Threading.Tasks` 命名空间中的类型来使用它们。

因此，你可以通过任务完成同样的事情，而不是调用 `ThreadPool` 的 `QueueUserWorkItem` 方法：

```csharp
ThreadPool.QueueUserWorkItem(ComputeBoundOp, 5); // Calling QueueUserWorkItem
new Task(ComputeBoundOp, 5).Start();             // Equivalent of above using Task
```

在上面的代码中，我创建 `Task` 对象，然后立即调用 `Start` 将任务安排为运行。当然，你也可以创建 `Task` 对象，稍后再对其调用 `Start`。你可以想象这样的代码：创建一个 `Task` 对象，然后将其传递给另一个方法，由该方法决定何时调用 `Start` 来安排任务。

创建 `Task` 时，你总是调用构造函数，向它传递一个 `Action` 或 `Action<Object>` 委托，以指示你希望执行的操作。如果你传递的方法期望一个 `Object`，那么你还必须向 `Task` 的构造函数传递最终希望传给该操作的参数。你还可以选择向 `Task` 的构造函数传递一个 `CancellationToken`，这允许 `Task` 在被安排之前取消（参见本章后面的“取消任务”一节）。

你还可以选择向构造函数传递一些 `TaskCreationOptions` 标志，以控制 `Task` 的执行方式。`TaskCreationOptions` 是一个枚举类型，定义了一组可以通过按位 OR 组合的标志。它的定义如下：

```csharp
[Flags, Serializable]
public enum TaskCreationOptions {
    None            = 0x0000, // The default

    // Causes the default TaskScheduler to put the task in the thread pool's
    // global queue instead of a worker thread's local queue.
    PreferFairness  = 0x0001,

    // This flag is a hint to the TaskScheduler and it determines how to interpret this hint.
    // Today, the default TaskScheduler creates a thread for the task instead of queuing the
    // task to a thread pool thread. This behavior could change in the future.
    LongRunning     = 0x0002,

    // Always honored: Associates a Task with its parent Task (discussed shortly)
    AttachedToParent = 0x0004,
}
```

这些标志大多是提示，可能被用于调度 `Task` 的 `TaskScheduler` 采纳，也可能不被采纳；`AttachedToParent` 标志始终会被采纳，因为它与 `TaskScheduler` 本身无关。`TaskScheduler` 对象将在后面的“任务调度器”一节中讨论。

### 等待任务完成并获取其结果

使用任务，还可以等待它们完成，然后获取其结果。假设我们有一个 `Sum` 方法，当 `n` 是一个很大的值时，该方法是计算密集型的：

```csharp
private static Int32 Sum(Int32 n) {
    Int32 sum = 0;
    for (; n > 0; n--)
        checked { sum += n; }  // if n is large, this will throw System.OverflowException
    return sum;
}
```

现在我们可以构造一个 `Task<TResult>` 对象（它派生自 `Task`），并为泛型 `TResult` 参数传入计算密集型操作的返回类型。现在，在启动任务之后，我们可以使用以下代码等待它完成并获取其结果：

```csharp
// Create a Task (it does not start running now)
Task<Int32> t = new Task<Int32>(n => Sum((Int32)n), 1000000000);

// You can start the task sometime later
t.Start();

// Optionally, you can explicitly wait for the task to complete
t.Wait(); // FYI: Overloads exist accepting timeout/CancellationToken

// You can get the result (the Result property internally calls Wait)
Console.WriteLine("The Sum is: " + t.Result); // An Int32 value
```

> **重要** 当线程调用 `Wait` 方法时，系统会检查该线程正在等待的 `Task` 是否已开始执行。如果已开始，那么调用 `Wait` 的线程将阻塞，直到 `Task` 运行完成。但如果 `Task` 尚未开始执行，那么系统*可能*（取决于 *TaskScheduler*）使用调用 `Wait` 的线程来执行 `Task`。如果发生这种情况，调用 `Wait` 的线程不会阻塞；它会执行 `Task` 并立即返回。这样做的好处是没有线程被阻塞，从而减少资源使用（不必创建线程来替换被阻塞的线程），同时提升性能（不花费时间创建线程，也没有上下文切换）。但这也可能带来坏处，例如，如果线程在调用 `Wait` 之前获取了线程同步锁，然后 `Task` 又尝试获取同一把锁，就会导致线程死锁！

如果计算密集型任务抛出一个未处理的异常，该异常会被吞掉，存储在一个集合中，并允许线程池线程返回线程池。当调用 `Wait` 方法或 `Result` 属性时，这些成员将抛出 `System.AggregateException` 对象。

`AggregateException` 类型用于封装异常对象的集合（如果父任务生成多个抛出异常的子任务，就可能发生这种情况）。它包含一个 `InnerExceptions` 属性，该属性返回一个 `ReadOnlyCollection<Exception>` 对象。不要将 `InnerExceptions` 属性与 `InnerException` 属性混淆，后者是 `AggregateException` 类从 `System.Exception` 基类继承的。对于上面的示例，`AggregateException` 的 `InnerExceptions` 属性的元素 0 将引用由计算密集型方法（`Sum`）抛出的实际 `System.OverflowException` 对象。

为方便起见，`AggregateException` 重写了 `Exception` 的 `GetBaseException` 方法。`AggregateException` 的实现返回作为问题根本原因的最内层异常（假设集合中只有一个最内层异常）。`AggregateException` 还提供一个 `Flatten` 方法，该方法创建一个新的 `AggregateException`，其 `InnerExceptions` 属性包含通过遍历原始 `AggregateException` 的内部异常层次结构而生成的异常列表。最后，`AggregateException` 还提供一个 `Handle` 方法，该方法为 `AggregateException` 中包含的每个异常调用一个回调方法。然后回调可以针对每个异常决定如何处理该异常；回调返回 `true` 以认为该

