

# 异步实现服务器

通过多年来与许多开发者交流，我发现极少开发者意识到 .NET Framework 内置了支持，可以让你构建扩展性极佳的异步服务器。在书中，我无法解释如何为每种服务器实现这一点，但我可以列出你在 MSDN 文档中应该寻找的内容。

- 构建异步的 ASP.NET Web Forms：在你的 .aspx 文件中，在页面指令中添加 "Async=true"，并查找 `System.Web.UI.Page.RegisterAsyncTask` 方法。
- 构建异步的 ASP.NET MVC 控制：让你的控制器类派自 `System.Web.Mvc.Controller`，只需让你的操作方法返回 `Task<ActionResult>`。
- 构建异步的 ASP.NET handler：让你的类派自 `System.Web.HttpAsyncTaskHandler`，然后重写它的抽象方法 `ProcessRequestAsync`。
- 构建异步 WCF 服务：将你的服务实现为异步函数并返回 `Task` 或 `Task<TResult>`。

# 取消 I/O 操作

通常情况下，Windows 并不提供取消正在进行的 I/O 操作的方法。这是许多开发者希望拥的功能但实现起来非常困难。毕竟，如果你从服务器发送了请求，然后决定不再需要响应，你没有办法告诉服务器放弃你的原始请求。处理这种情况的方法只是让字节返回到客户端机器，然后将其丢弃。此外，这里存在竞态条件——你的取消请求可能在服务器发送响应时到达。现在你的应用程序应该怎么做？你需要在自己的代码中处理这种竞态条件，并决定如何抛弃数据或对其进行处理。

为了协助这一点，建议你实现一个扩展 `Task<TResult>` 的 `WithCancellation` 方法（使用扩展 `Task` 的类似重载），如下所示：

```csharp
private async Task<TResult> WithCancellation<TResult>(this Task<TResult> originalTask, CancellationToken ct) {
    // 创建一个在 CancellationToken 取消时完成的任务
    var cancelTask = new TaskCompletionSource<Void>();

    // 当 CancellationToken 取消时，完成任务
    using (ct.Register(t => ((TaskCompletionSource<Void>)t).SetResult(new Void())), cancelTask)) {
    }

    // 创建一个在原始任务或
    // CancellationToken Token 完成时完成的任务
    Task any = await Task.WhenAny(originalTask, cancelTask.Task);

    // 如果任何任务是由 CancellationToken 完成的，抛出 OperationCanceledException
    if (any == cancelTask.Task) ct.ThrowIfCancellationRequested();

    // await originalTask (同步地); 如果它失败，等待
    // 将抛出一个内部异常，而不是 AggregateException
    return originalTask;
}
```

现在，你可以按照如下方式调用此扩展方法。

```csharp
public static async Task Go() {
    // 创建一个在 # 毫秒后自取消的 CancellationTokenSource
    var cts = new CancellationTokenSource(5000); // 如果要更早取消，调用 cts.Cancel()
    var ct = cts.Token;

    try {
        // 我使用 Task.Delay 进行测试；将其替换为另一个返回 Task 的方法
        await Task.Delay(10000).WithCancellation(ct);
        Console.WriteLine("Task completed");
    }
    catch (OperationCanceledException) {
        Console.WriteLine("Task cancelled");
    }
}
```

# 某些 I/O 操作必须同步执行

Win32 API 提供了许多执行 I/O 操作的函数。遗憾的是，这些方法中的某些并不允许你执行异步 I/O。例如，Win32File 方法（由 `FileStream` 构造函数调用）始终是同步执行。如果你尝试在网络服务器上创建或打开文件，`CreateFile` 返回之前可能需要几秒钟，而调用线程一直处于空闲状态。为响应性和扩展性设计的应用程序理想情况下调用允许创建或打开文件的 Win32 函数，这样你的线程就不会一直等待服务器的响应。遗憾的是，Win32 没有类似于 `CreateFile` 的函数让你执行此操作，因此 FCL 无法提供异步打开文件的有效方式。Windows 也没有提供异步访问注册表、访问事件日志、获取目录/多个目录，或更改文件/目录属性的函数（仅列举几例）。

这是一个真实问题的示例。想象编写一个简单的 UI，允许用户输入文件路径并提供自动补全（到常见的对话对话框）。该控件必须使用单独的线程枚举目录以寻找文件，因为 Windows 不提供异步枚举文件的函数。当用户继续在 UI 中输入时，你必须使用更多线程并忽略任何之前启动的线程的结果。在 Windows Vista 中，微软引入了一个名为 `Cancel-SynchronousIO` 的新 Win32 函数。该函数允许取消由另一个线程执行的同步 I/O 操作。此函数没有由 FCL 暴露，但如果你想在用托管代码实现的桌面应用程序中利用它，也可以通过 P/Invoke 来调用。在本章末尾显示了 P/Invoke 签名。

不过我想表达的观点是，许多人认为同步 API 更容易处理，在很多情况下确实如此。但在某些情况下，同步 API 会让事情变得困难。

由于执行 I/O 操作时存在的问题，Windows 团队在设计 Windows Runtime 时，决定暴露所有执行异步 I/O 的方法。请参见 `Windows.Storage.StorageFile` 的 `OpenAsync` 方法。事实上，Windows Runtime 没有提供任何允许你执行 I/O 操作的 API。幸运的是，在调用这些 API 时，你可以 C# 的异步函数来简化你的代码。

# FileStream 特有问题

当你创建一个 `FileStream` 对象时，通过 `FileOptions.Asynchronous` 标志指定你想与同步还是异步操作进行通信（这等同于调用 Win32 `CreateFile` 函数并传递 `FILE_FLAG_OVERLAPPED` 标志）。如果你没有指定此标志，Windows 将对文件执行所有操作。当然，你仍然可以调用 `FileStream` 的 `ReadAsync`，对你的应用程序来说，操作像是异步执行的，但在内部，`FileStream` 类使用其他方法来模拟异步行为，这是浪费且损害性能的。

另一方面，你可以通过指定 `FileOptions.Asynchronous` 标志来创建一个 `FileStream`。然后你可以调用 `FileStream` 的 `Read` 方法来执行同步操作。在内部，`FileStream` 类通过启动一个异步操作并立即让调用线程睡眠直到操作完成来模拟这种行为。这同样低效，但它不如使用未指定 `FileOptions.Asynchronous` 标志构造的 `FileStream` 调用 `ReadAsync` 高效。

所以总结一下，在处理 `FileStream` 时，你必须决定打算对文件执行同步还是异步 I/O，并通过指定（或不指定）`FileOptions.Asynchronous` 标志来指示选择。如果你指定了此标志，始终调用 `ReadAsync`。如果你没有指定此标志，并且要对 `FileStream` 执行某些同步和异步操作，使用 `FileOptions.Asynchronous` 标志构造它会更高效。或者，你可以针对同一个文件创建两个 `FileStream` 对象；打开一个用于异步 I/O，打开另一个用于同步 I/O。`System.IO.File` 类提供了返回 `FileStream` 对象的辅助方法（Create、Open 和 OpenWrite）。在内部，这些这些方法都没有指定 `FileOptions.Asynchronous` 标志，因此如果你想创建一个响应迅速或可扩展的应用程序，应该避免使用这些方法。

