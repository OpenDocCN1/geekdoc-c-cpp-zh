
**注意** 如果在 `CancellationTokenSource` 已经被取消之后，向该 `CancellationTokenSource` 注册回调方法，那么调用 `Register` 的线程会调用该回调（如果为 `useSynchronizationContext` 参数传递了 true，则可能通过调用线程的 `SynchronizationContext` 来调用）。

如果多次调用 `Register`，则会调用多个回调方法。这些回调方法可能引发未处理异常。如果调用 `CancellationTokenSource` 的 `Cancel` 并向其传递 true，那么第一个引发未处理异常的回调方法会阻止其他回调方法执行，并且所引发的异常也会从 `Cancel` 中抛出。如果调用 `Cancel` 并传递 false，则所有注册的回调方法都会被调用。发生的任何未处理异常都会添加到集合中。在所有回调方法执行完毕之后，如果其中任何一个引发了未处理异常，则 `Cancel` 会抛出 `AggregateException`，其 `InnerExceptions` 属性被设置为所抛出的异常对象的集合。如果没有任何注册的回调方法引发未处理异常，则 `Cancel` 只是返回，完全不抛出任何异常。

**重要** 无法将 `AggregateException` 的 `InnerExceptions` 集合中的异常对象与特定操作关联起来；你基本上只是被告知某个操作失败了，而异常类型会告诉你失败是什么。要追踪失败的具体位置，需要检查异常对象的 `StackTrace` 属性并手动扫描源代码。

`CancellationToken` 的 `Register` 方法返回一个 `CancellationTokenRegistration`，其形式如下：

```csharp
public struct CancellationTokenRegistration :
    IEquatable<CancellationTokenRegistration>, IDisposable {
    public void Dispose();
    // GetHashCode, Equals, operator== and operator!= members are not shown
}
```

可以调用 `Dispose`，从与其关联的 `CancellationTokenSource` 中移除已注册的回调，从而在调用 `Cancel` 时不会调用该回调。以下代码演示向单个 `CancellationTokenSource` 注册两个回调：

```csharp
var cts = new CancellationTokenSource();
cts.Token.Register(() => Console.WriteLine("Canceled 1"));
cts.Token.Register(() => Console.WriteLine("Canceled 2"));

// To test, let's just cancel it now and have the 2 callbacks execute
cts.Cancel();
```

运行此代码时，一旦调用 `Cancel` 方法，我就会得到以下输出：

```text
Canceled 2
Canceled 1
```

## 任务

调用 ThreadPool 的 QueueUserWorkItem 方法来启动异步计算密集型操作非常简单。然而，这种技术有许多限制。最大的问题是，没有内置方式让你知道操作何时完成，也无法在操作完成时获取返回值。为了解决这些限制及其他问题，微软引入了任务（task）的概念，你可以通过 System.Threading.Tasks 命名空间中的类型来使用它们。

因此，你可以通过任务来完成同样的事情，而不是调用 ThreadPool 的 QueueUserWorkItem 方法：

```csharp
ThreadPool.QueueUserWorkItem(ComputeBoundOp, 5); // Calling QueueUserWorkItem
new Task(ComputeBoundOp, 5).Start();             // Equivalent of above using Task
Task.Run(() => ComputeBoundOp(5));              // Another equivalent
```

在上面的第二行代码中，我创建 Task 对象，然后立即调用 Start 来安排任务运行。自然，你可以创建 Task 对象，稍后再对其调用 Start。可以想象这样的代码：创建一个 Task 对象，然后将其传递给某个其他方法，由该方法决定何时调用 Start 来安排任务。由于创建 Task 对象后立即对其调用 Start 很常见，因此可以调用 Task 便捷的静态 Run 方法，如上面最后一行代码所示。

创建 Task 时，需要调用构造函数，并向其传递一个 `Action` 或 `Action<Object>` 委托，以指示你希望执行的操作。如果传递的方法期望一个 Object，那么还必须向 Task 的构造函数传递你最终希望传给该操作的参数。调用 Run 时，可以传递一个 `Action` 或 `Func<TResult>` 委托，以指示你希望执行的操作。调用构造函数或调用 Run 时，可以选择传递一个 CancellationToken，这允许 Task 在被安排之前被取消（参见本章后面的“取消任务”一节）。

还可以选择向构造函数传递一些 TaskCreationOptions 标志，这些标志控制 Task 如何执行。TaskCreationOptions 是一个枚举类型，定义了一组可以用按位 OR 组合的标志。其定义如下：

```csharp
[Flags, Serializable]
public enum TaskCreationOptions {
    None            = 0x0000, // The default

    // Hints to the TaskScheduler that you want this task to run sooner than later.
    PreferFairness  = 0x0001,

    // Hints to the TaskScheduler that it should more aggressively create thread pool threads.
    LongRunning     = 0x0002,

    // Always honored: Associates a Task with its parent Task (discussed shortly)
    AttachedToParent= 0x0004,

    // If a task attempts to attach to this parent task, it is a normal task, not a child task.
    DenyChildAttach   = 0x0008,

    // Forces child tasks to use the default scheduler as opposed to the parent's scheduler.
    HideScheduler     = 0x0010
}
```

其中一些标志是提示，用于安排 Task 的 TaskScheduler 可能遵守也可能不遵守；AttachedToParent、DenyChildAttach 和 HideScheduler 标志始终会被遵守，因为它们与 TaskScheduler 本身无关。TaskScheduler 对象将在后面的“任务计划程序”一节中讨论。

### 等待任务完成并获取其结果

使用任务，还可以等待任务完成，然后获取其结果。假设我们有一个 Sum 方法，当 n 值很大时计算量很大：

```csharp
private static Int32 Sum(Int32 n) {
    Int32 sum = 0;
    for (; n > 0; n--)
        checked { sum += n; } // if n is large, this will throw System.OverflowException
    return sum;
}
```

现在可以构造一个 `Task<TResult>` 对象（它派生自 Task），并将计算密集型操作的返回类型作为泛型 TResult 参数传入。现在，在启动任务之后，我们可以使用以下代码等待任务完成并获取其结果：

```csharp
// Create a Task (it does not start running now)
Task<Int32> t = new Task<Int32>(n => Sum((Int32)n), 1000000000);

// You can start the task sometime later
t.Start();

// Optionally, you can explicitly wait for the task to complete
t.Wait(); // FYI: Overloads exist accepting timeout/CancellationToken

// You can get the result (the Result property internally calls Wait)
Console.WriteLine("The Sum is: " + t.Result);   // An Int32 value
```

**重要** 当线程调用 Wait 方法时，系统会检查该线程等待的 Task 是否已开始执行。如果已开始执行，则调用 Wait 的线程会阻塞，直到 Task 完成运行。但如果 Task 尚未开始执行，则系统可能（取决于 TaskScheduler）使用调用 Wait 的线程来执行 Task。如果发生这种情况，则调用 Wait 的线程不会阻塞；它会执行 Task 并立即返回。这样做的好处是没有线程被阻塞，从而减少资源使用（不创建线程来替代被阻塞的线程），同时提高性能（不花费时间创建线程，也没有上下文切换）。但也可能带来坏处，例如，如果线程在调用 Wait 之前获取了线程同步锁，然后 Task 尝试获取同一个锁，就会导致线程死锁！
