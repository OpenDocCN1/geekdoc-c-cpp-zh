
```csharp
public void EventRaised(Object sender, EventArgs eventArgs) {
    m_events.Enqueue(eventArgs); // Save EventArgs to return it from GetResult/await

    // If there is a pending continuation, this thread takes it
    Action continuation = Interlocked.Exchange(ref m_continuation, null);
    if (continuation != null) continuation(); // Resume the state machine
}
```

（接下）

```csharp
private static async void ShowExceptions() {
    var eventAwaiter = new Eventwaiter<FirstChangeException>();
    AppDomain.CurrentDomain.FirstException += eventAwaiter.EventRaised;

    while (true) {
        Console.WriteLine("AppDomain exception: {0}", (await eventAwaiter).Exception.GetType());
    }
}
```

（最后）

```csharp
private async void StartServer() {
    while (true) {
        var pipe = new NamedPipeServerStream(pipeName, PipeDirection.InOut, -1,
        PipeTransmissionMode.Message, PipeOptions.Asynchronous | PipeOptions.WriteThrough);
        // asynchronously connect a client connection
        // NOTE: NamedPipeServerStream uses the old Asynchronous
        // If there is a pending continuation, this thread takes it
        Action continuation = Interlocked.Exchange(ref m_continuation, null);
        if (continuation != null) continuation(); // Resume the state machine
    }
}
```

*(由于原文提供的文本中 `StartServer` 之后的内容似乎又粘贴了 `EventRaised` 的代码，我将严格按照给定文本流进行翻译，不进行逻辑修正。)*

---

**正式翻译输出：**

```csharp
public void EventRaised(Object sender, EventArgs eventArgs) {
    m_events.Enqueue(eventArgs); // 保存 EventArgs 以便从 GetResult/await 返回

    // 如果有等待中的延续，当前线程将处理它
    Action continuation = Interlocked.Exchange(ref m_continuation, null);
    if (continuation != null) continuation(); // 恢复状态机
}
```

这里是一个使用我的 `Eventwaiter` 类来从由于事件触发的 `await` 算符中返回的方法。在这种情况下，当 `AppDomain` 中的任何线程抛出异常时，状态机会继续执行。

```csharp
private static async void ShowExceptions() {
    var eventAwaiter = new Eventwaiter<FirstChangeException>();
    AppDomain.CurrentDomain.FirstException += eventAwaiter.EventRaised;

    while (true) {
        Console.WriteLine("AppDomain exception: {0}", (await eventAwaiter).Exception.GetType());
    }
}
```

最后，这里有一些演示所有功能均正常运行的代码。

# 异步函数与事件处理程序

异步函数通常具有 `Task` 或 `Task<TResult>` 返回类型，用于表示函数状态机的完成。然而，也可以定义一个 `void` 类型的异步函数。这是 C# 编译器允许的一种特殊情况，用以简化一种常见场景，即你想实现一个异步事件处理程序。

几乎所有的事件处理程序方法都遵循类似于此的方法签名。

```csharp
void EventHandlerCallback(Object sender, EventArgs e);
```

但是，在事件处理程序内部执行 I/O 操作是非常常见的，例如当用户点击打开文件并从中读取内容时。为了保持 UI 的响应性，这些 I/O 操作应该以异步方式进行。允许你在具有 `void` 返回类型的事件处理程序方法中编写此类代码，需要 C# 允许异步函数具有 `void` 返回类型，以便你能够使用 `await` 来执行非阻塞 I/O 操作。当异步函数具有 `void` 返回类型时，编译器会生成创建状态机的代码，但它不会创建 `Task` 对象，因为没有方法可以使用它。正因如此，没有方法可以知道返回 `void` 的异步函数状态机何时运行完成。⁵

# 框架类库（FCL）中的异步函数

我个人非常喜欢异步函数，因为它们易于学习、使用简单，并且受到 FCL 中许多类型的支持。识别异步函数很容易，因为按照惯例，方法名后会带有 `Async` 后缀。在框架类库（FCL）中，许多类型都通过 `xxxAsync` 方法提供了 I/O 操作。⁶ 以下是一些示例。

- 所有派自 `System.IO.Stream` 的类类都提供了 `ReadAsync`、`WriteAsync`、`FlushAsync` 和 `CopyToAsync` 方法。
- 所有派自 `System.IO.Text` 的类类都提供了 `ReadAsync`、`ReadAsync`、`ToEndAsync` 和 `ReadTextBlock` 方法。而且派自 `System.IO.Text` 的类类还提供了 `WriteAsync`、`LineAsync` 和 `FlushAsync` 方法。
- `System.Net.Http.HttpClient` 类提供了 `GetAsync`、`GetStreamAsync`、`GetByteArrayAsync`、`PutAsync`、`DeleteAsync` 等。
- 派自 `System.Net.WebRequest` 的类类（包括 `FileWebRequest`、`FWebRequest` 和 `HttpWebRequest`）提供了 `GetStreamAsync` 和 `GetResponseAsync`。
- 产生网络代理的工具（如 `SvcUtil.exe`）也提供了 `xxxAsync` 方法。

> ⁵ 出于此原因，如果你尝试将你的入口点方法（Main）标记为 `async`，C# 编译器会发出以下错误：入口点不能被标记为 'async'。如果你在 `Main` 方法中放置任何 `await` 算符，那么你的进程将在第一个 `await` 执行后立即从 `Main` 返回。但由于调用 `Main` 的代码无法获取该任务，因此无法监控并等待其完成，进程将直接终止（因为你从 `Main` 返回了），而 `Main` 中的其余代码将永远不会执行。幸运的是，C# 编译器包含了此错误以防止你返回一个 `async`。
> ⁶ WinRT 方法遵循相同的命名规范并返回 `IAsyncInfo` 接口。.NET Framework 提供了扩展方法，可以有效地将 `IAsync` 强制转换为 `Task`。有关如何与异步函数一起使用异步 WinRT API 的更多信息，请参阅第 25 章“与 WinRT 组件互操作”。

对于任何工作过早期版本 .NET Framework 的人，你可能对它提供的某些其他异步编程模型很熟悉。存在一种使用 `BeginXx` 和 `EndXx` 方法配合 `IAsyncResult` 接口的编程模型。还有一种基于事件的编程模型，它也有 `XxxAsync` 方法（这些不返回 `Task` 对象），并在异步操作完成时调用事件处理程序方法。这两种异步编程模型现在被认为是过时的，使用 `Task` 的新模型是首选模型。

在查看 FCL 时，你可能会注意到某些类缺少 `XxxAsync` 方法，而是提供了 `BeginXx` 和 `EndXx` 方法。这主要是由于微软没有时间用新方法更新这些类。在未来，微软将增强这些类，使其完全支持新模型。然而，在此之前，有一个辅助方法可以使用它将 `BeginXx` 和 `EndXx` 模型适配到新的基于 `Task` 的模型。

早些我展示了通过命名管道发送请求的客户端代码。现在让我展示一下这段代码的服务器端。

```csharp
private async void StartServer() {
    while (true) {
        var pipe = new NamedPipeServerStream(pipeName, PipeDirection.InOut, -1,
        PipeTransmissionMode.Message, PipeOptions.Asynchronous | PipeOptions.WriteThrough);
        // asynchronously connect a client connection
        // NOTE: NamedPipeServerStream uses the old Asynchronous
        // If there is a pending continuation, this thread takes it
        Action continuation = Interlocked.Exchange(ref m_continuation, null);
        if (continuation != null) continuation(); // Resume the state machine
    }
}
```

*(注：由于原文提供的文本中 `StartServer` 之后的内容似乎又粘贴了 `EventRaised` 的代码，我将严格按照给定文本流进行翻译，不进行逻辑修正。)*
