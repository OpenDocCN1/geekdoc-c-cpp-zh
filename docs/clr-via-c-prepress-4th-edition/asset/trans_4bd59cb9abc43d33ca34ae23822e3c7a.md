
如果计算密集型任务抛出了未处理的异常，该异常会被吞掉，存储在一个集合中，并允许线程池线程返回到线程池。当调用 Wait 方法或 Result 属性时，这些成员将抛出一个 System.AggregateException 对象。

AggregateException 类型用于封装异常对象的集合（当父任务生成多个抛出了异常的子任务时可能发生）。它包含一个 InnerExceptions 属性，该属性返回一个 ReadOnlyCollection<T> 对象。不要将 InnerExceptions 属性与 InnerException 属性混淆，后者是 AggregateException 类从 System.Exception 基类继承而来的。对于上面的例子，AggregateException 的 InnerExceptions 属性的元素 0 将引用由计算密集型方法（Sum）抛出的实际 System.OverflowException 对象。

为方便起见，AggregateException 重写了 Exception 的 GetBaseException 方法。AggregateException 的实现返回最内层的 AggregateException，它是问题的根本原因（假设集合中只有一个最内层的异常）。AggregateException 还提供了一个 Flatten 方法，该方法创建一个新的 AggregateException，其 InnerExceptions 属性包含通过遍历原始 AggregateException 的内部异常层次结构而生成的异常列表。最后，AggregateException 还提供了一个 Handle 方法，该方法为 AggregateException 中包含的每个异常调用一个回调方法。然后，回调可以对每个异常决定如何处理该异常；回调返回 true 表示该异常已处理，返回 false 表示未处理。如果在调用 Handle 之后，至少有一个异常未被处理，则会创建一个仅包含未处理异常的新 AggregateException 对象，并抛出该新 AggregateException 对象。在本章稍后的部分，我会展示使用 Flatten 和 Handle 方法的示例。

**重要说明** 如果你从未调用 Wait 或 Result，也未查询 Task 的 Exception 属性，那么你的代码永远不会观察到该异常已发生。这并不理想，因为你的程序经历了你未意识到的意外问题。为了帮助你检测未观察到的异常，你可以向 TaskScheduler 的静态 UnobservedTaskException 事件注册一个回调方法。每当带有未观察到的异常的 Task 被垃圾回收时，CLR 的终结器线程就会引发此事件。当该事件被引发时，你的事件处理方法将收到一个包含未观察到的 AggregateException 的 UnobservedTaskExceptionEventArgs 对象。

除了等待单个任务之外，Task 类还提供了两个静态方法，允许线程等待 Task 对象数组。Task 的静态 WaitAny 方法会阻塞调用线程，直到数组中的任意一个 Task 对象完成。该方法返回数组中的一个 Int32 索引，指示哪个 Task 对象已完成，从而使线程唤醒并继续运行。如果发生超时，该方法返回 -1；如果 WaitAny 通过 CancellationToken 被取消，则抛出 OperationCanceledException。

类似地，Task 类有一个静态 WaitAll 方法，该方法会阻塞调用线程，直到数组中的所有 Task 对象都已完成。如果所有 Task 对象都完成，WaitAll 方法返回 true；如果发生超时，则返回 false；如果 WaitAll 通过 `CancellationToken` 被取消，则会抛出 OperationCanceledException。

## 取消 Task

当然，你可以使用 `CancellationTokenSource` 来取消 Task。首先，我们必须修改 Sum 方法，使其接受一个 `CancellationToken`：

```csharp
private static Int32 Sum(CancellationToken ct, Int32 n) {
    Int32 sum = 0;
    for (; n > 0; n--) {

        // The following line throws OperationCanceledException when Cancel
        // is called on the CancellationTokenSource referred to by the token
        ct.ThrowIfCancellationRequested();

        checked { sum += n; }   // if n is large, this will throw System.OverflowException
    }
    return sum;
}
```

在这段代码中，计算密集型操作的循环会定期调用 `CancellationToken` 的 `ThrowIfCancellationRequested` 方法来检查操作是否已被取消。此方法类似于前面“协作式取消”一节中所示的 `CancellationToken` 的 `IsCancellationRequested` 属性。但是，如果 `CancellationTokenSource` 已被取消，`ThrowIfCancellationRequested` 会抛出 `OperationCanceledException`。抛出异常的原因是：与通过 ThreadPool 的 QueueUserWorkItem 方法启动的工作项不同，任务具有“已完成”的概念，而且任务甚至可以返回值。因此，需要有一种方式来区分已完成的任务和已取消的任务，而让任务抛出异常可以让你知道任务没有一路运行到完成。

现在，我们将创建 `CancellationTokenSource` 和 Task 对象，如下所示：

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
Task<Int32> t = Task.Run(() => Sum(cts.Token, 100000000), cts.Token);

// Sometime later, cancel the CancellationTokenSource to cancel the Task
cts.Cancel(); // This is an asynchronous request, the Task may have completed already

try {
    // If the task got canceled, Result will throw an AggregateException
    Console.WriteLine("The sum is: " + t.Result);   // An Int32 value
}
catch (AggregateException x) {
    // Consider any OperationCanceledException objects as handled.
    // Any other exceptions cause a new AggregateException containing
    // only the unhandled exceptions to be thrown
    x.Handle(e => e is OperationCanceledException);

    // If all the exceptions were handled, the following executes
    Console.WriteLine("Sum was canceled");
}
```

创建 Task 时，你可以通过将 CancellationToken 传递给 Task 的构造函数（如上所示）来将其与 Task 关联。如果在 Task 被调度之前 CancellationToken 被取消，Task 会被取消，并且根本不会执行⁴⁸。但如果 Task 已经被调度（通过调用 Start 方法），那么 Task 的代码必须显式支持取消，才能允许其操作在执行过程中被取消。不幸的是，虽然 Task 对象关联了一个 CancellationToken，但无法访问它，因此你必须以某种方式将用于创建 Task 对象的同一个 CancellationToken 传入 Task 的代码本身。编写此代码最简单的方法是使用 lambda 表达式，并将 CancellationToken 作为闭包变量“传递”（就像我在前面的代码示例中所做的那样）。

⁴⁸ 顺便说一下，如果你试图在任务尚未启动之前就取消任务，会抛出 InvalidOperationException。
