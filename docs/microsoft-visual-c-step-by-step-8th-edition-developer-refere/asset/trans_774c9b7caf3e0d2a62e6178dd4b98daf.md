

在该方法完成之前无响应。你可以通过使用 *Task* 对象来运行 *doFirstLongRunningOperation* 方法并为同一个 *Task* 定义延续，使其依次运行 *doSecondLongRunningOperation* 和 *doThirdLongRunningOperation* 方法，从而使 *slowMethod* 方法更具响应性，如下所示：

Click here to view code image

```
private void slowMethod()
{
    Task task = new Task(doFirstLongRunningOperation);
    task.ContinueWith(doSecondLongRunningOperation);
    task.ContinueWith(doThirdLongRunningOperation);
    task.Start();
    message.Text = "Processing Completed"; // When does this message appear?
}
```

```
private void doFirstLongRunningOperation()
{
    ...
}
```

```
private void doSecondLongRunningOperation(Task t)
{
    ...
}
```

```
private void doThirdLongRunningOperation(Task t)
{
    ...
}
```

尽管这种重构看起来相当简单，但仍有一些需要注意的地方。具体来说，*doSecondLongRunningOperation* 和 *doThirdLongRunningOperation* 方法的签名已更改，以适应延续的要求（引发延续的 *Task* 对象作为参数传递给延续方法）。更重要的是，你需要问自己：“何时在 *TextBox* 控件中显示该消息？” 这个第二点的问题在于，尽管 *Start* 方法启动了 *Task*，但它不会等待其完成，因此消息会在处理过程中出现，而不是在处理完成后出现。

这是一个有点 trivial 的示例，但一般原则很重要，至少有两种解决方案。第一种是在显示消息之前等待 *Task* 完成，如下所示：

Click here to view code image

```
private void slowMethod()
{
    Task task = new Task(doFirstLongRunningOperation);
    task.ContinueWith(doSecondLongRunningOperation);
    task.ContinueWith(doThirdLongRunningOperation);
    task.Start();
    task.Wait();
    message.Text = "Processing Completed";
}
```

然而，调用 Wait 方法现在会阻塞执行 slowMethod 方法的线程，从而抵消了使用 Task 的初衷。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_658_0.png)

## Important

一般来说，你绝不应该在用户界面线程中直接调用 Wait 方法。

更好的解决方案是定义一个显示消息的延续，并安排它仅在 doThirdLongRunningOperation 方法完成后运行，在这种情况下可以删除对 Wait 方法的调用。你可能会被诱惑将此延续实现为如下代码中以粗体显示的委托（请记住，延续会作为参数接收一个 Task 对象；这就是委托的 t 参数的目的）：

Click here to view code image

```
private void slowMethod()
{
    Task task = new Task(doFirstLongRunningOperation);
    task.ContinueWith(doSecondLongRunningOperation);
    task.ContinueWith(doThirdLongRunningOperation);
    task.ContinueWith((t) => message.Text = "Processing Complete");
    task.Start();
}
```

不幸的是，这种方法暴露了另一个问题。如果你在 Debug 模式下尝试运行此代码，你会发现最终的延续会生成一个 System.Exception 异常，其信息相当晦涩：“The application called an interface that was marshaled for a different thread。” 问题在于只有用户界面线程可以操作用户界面控件，而现在你正尝试从另一个线程写入 TextBox 控件——用于运行 Task 的线程。你可以通过使用 Dispatcher 对象来解决此问题。Dispatcher 对象是用户界面基础设施的组件，你可以通过调用其 RunAsync 方法向其发送在用户界面线程上执行工作的请求。此方法接受一个 Action 委托来指定要运行的代码。Dispatcher 对象和 RunAsync 方法的细节超出了本书的范围，但以下示例展示了如何使用它们从延续中显示 slowMethod 方法所需的消息：

Click here to view code image

```
private void slowMethod()
{
    Task task = new Task(doFirstLongRunningOperation);
    task.ContinueWith(doSecondLongRunningOperation);
    task.ContinueWith(doThirdLongRunningOperation);
    task.ContinueWith((t) => this.Dispatcher.RunAsync(
        CoreDispatcherPriority.Normal,
        () => message.Text = "Processing Complete"));
    task.Start();
}
```

这可行，但很混乱且难以维护。你现在有一个委托（延续）指定另一个委托（由 RunAsync 运行的代码）。

## More info

你可以在 Microsoft 网站 https://msdn.microsoft.com/library/windows.ui.core.coredispatcher.runasync 上找到有关 Dispatcher 对象和 RunAsync 方法的更多信息

## Defining asynchronous methods: The solution

C# 中 async 和 await 关键字的目的是使你能够定义和调用可以异步运行的方法。这意味着你不必担心指定延续或安排代码在 Dispatcher 对象上运行以确保数据在正确的线程上被操作。非常简单：

- async 修饰符表示方法包含可以异步运行的功能。
- await 操作符指定应在此处执行此异步功能的点。

以下代码示例展示了 slowMethod 方法作为异步方法实现，使用 async 修饰符和 await 操作符：

Click here to view code image

```
private async void slowMethod()
{
    await doFirstLongRunningOperation();
    await doSecondLongRunningOperation();
    await doThirdLongRunningOperation();
    message.Text = "Processing Complete";
}
```

此方法现在看起来与原始版本非常相似，这就是 async 和 await 的强大之处。事实上，这种魔术不过是 C# 编译器对代码的重写练习。当 C# 编译器在 async 方法中遇到 await 操作符时，它有效地将该操作符后面的操作数重新格式化为在与 *async* 方法相同的线程上运行的任务。其余代码被转换为在任务完成后运行的延续，同样在同一线程上运行。现在，由于运行 *async* 方法的线程是运行用户界面的线程，它可以直接访问窗口中的控件，这意味着它可以直接更新它们，而无需通过 *Dispatcher* 对象路由。

尽管这种方法乍一看相当简单，但请务必牢记以下几点并避免一些可能的误解：

- *async* 修饰符并不表示方法在单独的线程上异步运行。它所做的只是指定方法中的代码可以被拆分为一个或多个延续。当这些延续运行时，它们在与原始方法调用相同的线程上执行。
- *await* 操作符指定 C# 编译器可以在此处将代码拆分为延续的点。*await* 操作符本身期望其操作数是一个 *awaitable* 对象。awaitable 对象是一种提供 *GetAwaiter* 方法的类型，该方法返回一个对象，进而提供运行代码和等待其完成的方法。C# 编译器将你的代码转换为使用这些方法创建适当延续的语句。

## Important

你只能在标记为 *async* 的方法中使用 *await* 操作符。在 *async* 方法之外，await 关键字被视为普通标识符（你甚至可以创建一个名为 *await* 的变量，尽管不推荐这样做）。

在当前 *await* 操作符的实现中，它期望你指定的操作数是一个 *Task*。这意味着你必须对 *doFirstLongRunningOperation*、*doSecondLongRunningOperation* 和 *doThirdLongRunningOperation* 方法进行一些修改。具体来说，每个方法现在必须创建并运行一个 *Task* 来执行其工作并返回对该 *Task* 的引用。以下示例展示了 *doFirstLongRunningOperation* 方法的修改版本：

Click here to view code image

```
private Task doFirstLongRunningOperation()
{
    Task t = Task.Run(() => { /* original code for this method goes here */ });
    return t;
}
```

