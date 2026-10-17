
- 3. 在 `generateGraphData` 方法中，注释掉检查 `CancellationToken` 对象 `IsCancellationRequested` 属性的 `if` 语句，并添加调用 `ThrowIfCancellationRequested` 方法的语句，如下所示：

```csharp
private void generateGraphData(byte[] data, int partitionStart, partitionEnd, CancellationToken token)
{
    for (int x = partitionStart; x < partitionEnd; x++)
    {
        for (double i = -p; i < p; i += 3)
        {
            // if (token.IsCancellationRequested)
            // {
            //   return;
            // }
            token.ThrowIfCancellationRequested();
        }
    }
}
```

- 4. 在调试菜单上，点击“不调试启动”。

- 5. 在 GraphDemo 窗口中，点击“绘图”，等待图表出现，并验证两个任务的状态都报告为 `RanToCompletion` 且图表已生成。

- 6. 再次点击“绘图”，然后快速点击“取消”。如果你足够，一个或两个任务的状态应该报告为 `Canceled`，时长文本框应显示文本“操作已取消”，且图表应显示空洞。如果你不够快，请重复此步骤再次尝试。

# 7. 关闭 GraphDemo 应用程序并返回 Visual Studio。

## 使用 AggregateException 类处理任务异常

在整本书中，你已经看到异常处理是任何商业级应用中的重要元素。到目前为止，你所遇到的异常处理结构易于使用，如果你仔细地使用它们，捕获异常并确定是哪部分代码抛出的异常是一件简单的事情。然而，当你开始将工作分为多个并发任务时，跟踪和处理异常就会变成一个更复杂的问题。上一个练习展示了你如何捕获取消任务时抛出的 `OperationCanceledException`。然而，可能会发生许多其他异常，而且不同的任务会生成它们各自的异常。因此，你需要一种方法来捕获并处理必须并发抛出的多个异常。

如果你正在使用 Task 等待方法来等待多个任务完成（实例方法 `Wait` 或静态的 `Task.WaitAll` 和 `Task.WaitAny` 方法），则这些任务正在运行的方法抛出的任何异常都将被汇总到一个称为 `AggregateException` 的异常中。它作为异常集合的包装器。集合中的每个异常可能由不同的任务抛出。在你的应用程序中，你可以捕获 `AggregateException` 异常，然后遍历此集合并执行任何必要的处理。为了帮助你，`AggregateException` 类提供了 `Handle` 方法。`Handle` 方法接收一个 `Func<Exception, bool>` 委托，该委托作为参数引用，并返回一个接受 `Exception` 对象并返回布尔值的方法。当你调用 `Handle` 时，被引用的方法会为 `AggregateException` 对象中的每个异常运行。引用的方法可以检查异常并采取适当的行动。如果引用的方法处理了异常，它应该返回 `true`。如果没有处理，则返回 `false`。当 `Handle` 方法完成时，任何未处理的异常将一起捆成一个新的新的 `AggregateException` 异常，并抛出该异常。随后的外部异常处理程序可以捕获此异常并对其处理。

接下来的代码片段显示了一个可以 `AggregateException` 异常处理程序注册的方法示例。如果该方法检测到 `DivideByZeroException` 异常，则只需显示“发生除零错误”的消息；如果发生 `IndexOutOfRangeException`，则显示“数组索引越界”的消息。任何其他异常将保持未处理。

点击此处查看代码图像

```csharp
private bool handleError(Exception e)
{
    if (e is DivideByZeroException)
    {
        displayErrorMessage("Division by zero occurred");
        return true;
    }
    if (e is IndexOutOfRangeException)
    {
        displayErrorMessage("Array index out of bounds");
        return true;
    }
    return false;
}
```

当你使用 Task 方法时，可以捕获 `AggregateException` 异常并注册 `handleError` 方法，如下：

点击此处查看代码图像

```csharp
try
{
    Task first = Task.Run(...);
    Task second = Task.Run(...);
    Task.WaitAll(first, second);
}
catch (AggregateException ae)
{
    ae.Handle(handleError);
}
```

如果任何任务生成 `DivideByZeroException` 异常或 `IndexOutOfRangeException` 异常，`handleError` 方法将显示适当的消息并确认异常已处理。任何其他异常将被归类为未处理，并将以通常方式从 `AggregateException` 异常处理程序传播出。

你应该注意的一个额外复杂性。当你取消任务时，你已经看到 CLR 抛出了 `OperationCanceled` 异常，如果你使用 `await` 运算符等待任务，这就是所报告的异常。然而，如果你正在使用 Task 等待方法之一，此异常将转换为 `TaskCanceledException` 异常，并且你你应该准备好在 `AggregateException` 句器中处理的异常类型。

## 对取消和失败的任务使用延续任务

如果你需要在任务被取消或抛出未处理异常时执行额外工作，请记住你可以使用带有适当 `TaskContinuationOptions` 值的 `ContinueWith` 方法。例如，下面的代码创建了一个运行 `doWork` 方法的任务。如果任务被取消，`ContinueWith` 方法将指定创建另一个任务并运行 `doCancellationWork` 方法。此方法可以执行一些简单的记录或清理。如果任务未取消，则延续任务不会运行。

点击此处查看代码图像

```csharp
Task task = new Task(doWork);
task.ContinueWith(doCancellationWork,
TaskContinuationOptions.OnlyOnCanceled);
task.Start();

private void doWork()
{
    // 任务在启动时运行此代码
}

private void doCancellationWork(Task task)
{
    // 任务在 doWork 完成时运行此代码
}
```

同样，你可以指定值 `TaskContinuationOptions.OnlyOnFaulted`，以指定一个在由任务运行的原始方法抛出未处理异常时运行的延续任务。

### 总结

在本章中，你学习了为什么编写可以跨多个处理器和处理器核心进行扩展的应用程序是重要的。你了解了如何使用 `Task` 类来并行运行操作，以及如何同步并发操作并等待它们完成。你学习了如何使用 `Parallel` 类来并行处理常见的语句结构，并使用了任务和线程来提高响应性和吞吐量，并学习了如何以整洁控制的方式取消任务。

- 如果你想继续下一章，请保持 Visual Studio。
- 如果你想退出 Visual Studio，如果看到保存对话框，点击“是”。

### 快速参考

| 操作 | 这样做 |
| --- | --- |
| 创建任务并运行 | 使用 `Task` 类的静态 `Run` 方法创建并运行任务：<br>[点击此处查看代码图像](```csharp\ntask = Task.Run(() => doWork());\nprivate void doWork()\n    // 任务在启动时运行此代码\n});``` 或者，创建一个新的 `Task` 对象并引用一个方法然后调用 `Start` 方法：<br>```csharp\ntask = new Task(doWork);\ntask.Start();``` |

| 等待任务完成 | 调用 `Task` 对象的 `Wait` 方法：<br>```csharp\ntask = ...;\ntask.Wait();``` 或使用 `await` 运算符（仅在异步方法中）：await task; |
| 等待多个任务完成 | 调用 `Task` 类的静态 `WaitAll` 方法，并指定要等待的任务：<br>[点击此处查看代码图像](```csharp\ntask1 = ...;\nTask task2 = ...;\nTask task3 = ...;\nTask task4 = ...;\n...\nTask.WaitAll(task1, task2, task3, task4);``` |

| 当任务完成后在新任务中指定方法 | 调用任务的 `ContinueWith` 方法并指定该方法作为延续任务：<br>[点击此处查看代码图像](```csharp\ntask = new Task(doWork);\ntask.ContinueWith(doMoreWork, TaskContinuationOptions.NotFaulted);``` |
| 使用并行执行循环迭代和语句序列 | 使用 `Parallel.For` 和 `Parallel.ForEach` 方法使用任务执行循环迭代：<br>[点击此处查看代码图像](```csharp\nParallel.For(0, 100, performLoopProcessing);\nprivate void performLoopProcessing(int x)\n{\n    // 执行循环处理\n}``` |

| 使用 `Parallel.Invoke` 方法使用独立任务执行并发方法调用：<br>[点击此处查看代码图像](```csharp\nParallel.Invoke(\ndwork,\ndoMoreWork,\ndoYetWork\n);```) |
| 处理由一个或多个任务抛出的异常 | 捕获 `AggregateException` 异常。使用 `Handle` 方法指定一个可以处理 `AggregateException` 对象中每个异常的方法。如果异常处理方法处理了异常，则返回 `true`；否则，返回 `false`：<br>点击此处查看代码图像 |

```cs
try
{
  Task task = Task.Run(...);
  task.Wait();
...
}
catch (AggregateException ae)
{
  ae.Handle(handleException);
}
...
private bool handleException(Exception e)
{
  if (e is TaskCanceledException)
  {
    ...
    return true;
  }
  else
  {
    return false;
  }
}
```

在任务中启用取消

通过创建 `CancellationTokenSource` 对象并在任务运行的方法中使用 `CancellationToken` 参数来实现协作式取消。在任务方法中，调用 `CancellationToken` 参数的 `ThrowIfCancellationRequested` 方法来抛出 `OperationCanceledException` 异常并终止任务：

点击此处查看代码图片

```cs
private void generateGraphData(..., CancellationToken token)
{
token.ThrowIfCancellationRequested();
...
}
```

### 通过异步操作提高响应时间

完成本章后，你将能够：

- 定义并使用异步方法，以提高执行耗时和 I/O 密集型操作应用程序的交互响应时间。
- 解释如何通过并行化来减少执行复杂 LINQ 查询所需的时间。
- 使用并发集合类在并行任务之间安全地共享数据。

第 23 章“使用任务提高吞吐量”演示了如何使用 `Task` 执行并行操作，并提高计算密集型应用程序的吞吐量。然而，虽然最大化应用程序可用的处理能力可以使其运行得更快，但响应能力同样重要。请记住，Windows 用户界面使用单线程执行，但当用户点击表单上的按钮时，他们期望应用程序能够做出响应，即使应用程序当前正在执行大型且复杂的计算。此外，某些任务即使不是计算密集型的，也可能需要很长时间才能运行（例如，等待从远程网站跨网络接收信息的 I/O 密集型任务），在等待可能不确定何时发生的事件时阻塞用户交互，显然不是一种良好的做法。解决这两个问题的方案是相同的：以异步方式执行执行任务，并让用户界面线程空闲以处理用户交互。

响应时间问题不仅限于用户界面。例如，第 21 章“使用查询表达式查询内存数据”展示了你如何使用集成语言的查询（LINQ）以声明式的方式访问内存中的数据。典型的 LINQ 查询生成一个可枚举结果，你可以串行迭代该结果以检索数据。如果用于生成结果的数据源很大，运行 LINQ 查询可能会花费很长时间。许多数据库管理系统面临着通过算法优化此类问题的问题，这些算法将查询数据的识别过程分解为一系列任务，然后并行运行这些任务，并在任务完成后组合结果以生成完整结果。Microsoft .NET Framework 的设计者决定为 LINQ 提供类似的的机制，其结果就是并行 LINQ（Parallel LINQ，或 PLINQ）。你将在本章的第二部分学习 PLINQ。

### 异步性与可扩展性

异步是一个强大的概念，如果你正在构建企业级 Web 应用程序和服务等大型解决方案，你就需要理解它。Web 服务器通常资源有限，需要处理来自可能大量受众的请求，其中每个成员都期望其请求能被快速处理。在许多情况下，用户请求可能会调用一系列可能花费大量时间的操作（可能长达一或两秒）。考虑一个电子商务系统，例如，用户正在查询产品目录或下订单。这两种操作通常涉及读取和写入存储在数据库中的数据，该数据库可能由远程 Web 服务器的数据库服务器管理。许多 Web 服务器只能支持有限数量的并发连接，如果与连接关联线程正在等待 I/O 操作完成，那么该连接实际上就被阻塞了。如果线程创建一个单独的任务来异步处理 I/O，那么线程就可以被释放，连接也可以回收给另一个用户。这种方法比实现同步操作具有得多的扩展性。

要了解关于为什么在这种情况下执行同步 I/O 是糟糕的示例和详细说明，请阅读微软 公开 Patterns & Practices Git 仓库中关于“同步 I/O 反模式”的文章，地址如下：

https://github.com/mspnp/performance-optimization/tree/master/SynchronousIO.

### 实现异步方法

异步方法是一种不会阻塞其开始运行的当前线程的方法。当应用程序调用异步方法时，一个隐含的合约期望该方法很快地将控制权返回给调用环境，并在单独线程上执行其工作。“相当快速”的定义并不是一个数学上的量化，但预期是，如果异步方法执行了可能会延迟调用者的操作，它应该通过使用后台线程来执行，从而允许调用者在当前线程上继续运行。这个过程听起来很复杂，而且在 .NET Framework 的早期版本中确实如此。然而，C# 现在提供了 `async` 方法和 `await` 操作符，它们将许多复杂性抽象给了编译器，这意味着（在大多数情况下）你不再需要担心多线程的复杂性。

### 定义异步方法：问题所在

你已经看到了如何使用 `Task` 对象实现并发操作。为了快速获取，你通过使用 `Task` 类型的 `Start` 或 `Run` 方法来启动任务，通用语言运行时（CLR）使用它自己的调度算法将任务分配给线程，并在资源充足时在操作系统方便的时间设置该线程运行。

这种方法使你的代码摆脱了识别和管理计算机工作负载的限制。如果你在特定任务完成后需要执行另一个操作，你有以下选择：

- 你可以使用由 `Task` 类型暴露的 `Wait` 方法手动等待任务完成。然后你可以启动新操作，可能通过定义另一个任务来实现。
- 你可以定义延续（continuation）。延续只需指定在给定任务完成后要执行的操作。.NET Framework 会在原始任务结束时，作为一个它调度的任务自动执行延续操作。延续将重用与原始任务相同的线程。

然而，尽管 `Task` 类型提供了操作的便捷泛化，但你仍然需要编写可能笨拙的代码来解决开发者在使用后台线程时遇到的一些常见问题。例如，假设你定义了以下方法，它执行一系列必须以串行方式运行的耗时操作，并在屏幕上的 TextBox 控件上显示消息：

点击此处查看代码图片

```cs
private void slowMethod()
{
doFirstLongRunningOperation();
doSecondLongRunningOperation();
doThirdLongRunningOperation();
message.Text = "Processing Completed";
}
```

```cs
private void doFirstLongRunningOperation()
{
..
}
```

```cs
