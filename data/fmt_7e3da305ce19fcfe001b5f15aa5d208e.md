
# 异步编程模型概述

- 派自 `System.Net.WebRequest` 的类类（包括 `FileWebRequest`、`FWebRequest` 和 `HttpWebRequest`）提供了 `GetStreamAsync` 和 `GetResponseAsync`。

- 产生网络代理的工具（如 `SvcUtil.exe`）也提供了 `xxxAsync` 方法。

> ⁵ 出于此原因，如果你尝试将你的入口点方法（`Main`）标记为 `async`，C# 编译器会发出以下错误：入口点不能被标记为 'async'。如果你在 `Main` 方法中放置任何 `await` 算符，那么你的进程将在第一个 `await` 执行后立即从 `Main` 返回。但由于调用 `Main` 的代码无法获取该任务，因此无法监控并等待其完成，进程将直接终止（因为你从 `Main` 返回了），而 `Main` 中的其余代码将永远不会执行。幸运的是，C# 编译器包含了此错误以防止你返回一个 `async`。

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

如果你的状态方法遇到了未处理的异常，代表你异步函数的 `Task` 对象将由于该未处理的异常而完成。任何等待等待此 `Task` 对象完成的代码都会看到该异常。然而，异步函数也可能是 `void` 返回类型。在这种情况下，调用者没有办法发现未处理的异常。因此，当返回 `void` 的异步函数抛出未处理的异常时，编译器生成的代码会捕获它并使用调用者的同步上下文（后文将讨论）重新抛出它。如果调用者是通过 GUI 线程执行的，GUI 线程最终重新抛出异常。如果调用者是通过非 GUI 线程执行的，线程池线程最终重新抛出异常。通常，重新抛出这些异常会导致整个进程终止。

## 其他异步函数特性

在这一节中，我想与你分享一些与异步函数相关的特性。Microsoft Visual Studio 对调试异步函数提供了很好的支持。当调试器停止在 `await` 迭代器上时，执行跳过（F10）将在操作完成后到达下一个语句时实际上会再次进入调试器。这非常有用，并简化了调试工作。

此外，如果你不小心进入了（F11）一个异步函数，你可以跳出（Shift+F11）返回调用者；你必须在异步函数的起始大括号处执行此操作。一旦你过了起始大括号，跳出（Shift+F11）在异步函数运行直到完成之前不会中断。如果你需要在状态机运行到完成之前调试调用方法，请在调用方法中设置断点并直接运行（F5）到那里。

某些异步操作执行得很快，几乎瞬间完成。当这种情况发生时，挂起状态机然后让另一个线程立即恢复状态机是低效的；让状态机继续执行要高效得多。坦率地说，`await` 操作符的编译器生成代码检查了这一点。如果异步操作在线程返回之前恰好完成，线程就不会返回，而是直接执行下一行代码。

这些都很好，但偶尔你会遇到一个函数在启动异步操作之前执行了大量的处理工作。如果你通过你的 GUI 线程调用该函数，你的用户界面将对用户无响应。而且，如果异步操作同步完成的，那么你的用户界面无响应的时间会更长。因此，如果你想从调用它的其他线程启动异步函数，可以使用 `Task` 的静态运行方法。

```
// Task.Run 在 GUI 线程上调用
Task.Run(async () => {
    // 此代码运行在线程池上
    // TODO: 在此处执行密集的计算型处理...

    await XxxAsync(); // 启动异步操作
    // 执行更多处理...
});
```

这段代码演示了另一个 C# 特性：异步 lambda 表达式。你可以你不能直接在普通 lambda 表达式的体内放置 `await` 操作符，因为编译器知道如何将方法转换为状态机。通过在 lambda 表达式之前放置 `async`，会导致产生返回 `Task` 或 `Task<TResult>` 的状态机，然后将其赋值给任何返回类型为 `Task` 或 `Task<TResult>` 的 `Func` 委托。

在编写代码时，很容易在调用异步函数时忘记使用 `await` 操作符；以下代码演示了：

```
static async Task OuterAsyncFunction() {
    // 哎，忘记在这一行加上 await 操作符了！

    // 当 InnerAsyncFunction 继续执行时，代码也继续执行...
}
```

```
static async Task InnerAsyncFunction() { /* 此处的代码不重要 */ }
```

幸运的是，当你这样做时，C# 编译器会给出以下警告：由于此调用未被等待，在调用完成之前，当前方法的执行将继续。请考虑对调用的结果应用 'await' 操作符。这在极少数情况下是很有用的，即你实际上并不不在乎 `InnerAsyncFunction` 何时完成，并且你想避免编写该代码而不让编译器发出警告。

为了消除警告，你只需简单地将 `InnerAsyncFunction` 返回的 `Task` 赋值给变量然后忽略它即可。

```
static async Task OuterAsyncFunction() {
    var noWarning = InnerAsyncFunction(); // 我打算不在这这一行加上 await 操作符。

    // 当 InnerAsyncFunction 继续执行时，代码也继续执行...
}
```

或者，我更倾向于定义一个这样的扩展方法。

```
[MethodImpl](MethodOptions.AggressiveInlining)] // 导致编译器优化掉调用
public static void NoWarning(this Task task) { /* 此处不包含任何代码 */ }
```

然后可以这样使用它：

```
static async Task OuterAsyncFunction() {
    InnerAsyncFunction().NoWarning(); // 我打算不在这这一行加上 await 操作符。

    // 当 InnerAsyncFunction 继续执行时，代码也继续执行...
}
```

执行异步 I/O 操作的真正伟大特性之一是，你可以并发启动许多此类操作，以便它们能够并行执行。这可以为你的应用带来巨大的性能提升。

> 幸运的是，编译器不会对局部变量的使用给出警告。

一个惊人的提升。我向你展示了启动了管道服务器并创建了大量的客户端请求。现在给你看代码。

```
public static async Task Go() {
    // 启动服务器，它立即返回，因为
    // 它异步等待客户端请求
    StartServer();

    // 创建大量的异步请求；保存每个请求的 Task<String>
    List<String> requests = new List<String>(10000);
    for (Int32 n = 0; n < requests.Capacity; n++) {
        requests.Add(ClientRequestAsync("localhost", "Request " + n));
    }

    // 异步等待所有客户端请求完成
    // 注意：如果任务抛出异常，WhenAll 将重新抛出异常
    String[] responses = await Task.All(requests);

    // 处理所有响应
    for (Int32 n = 0; n < responses.Length; n++) {
        Console.WriteLine(responses[n]);
    }
}
```

在前面的代码中，我希望在处理结果之前等待所有客户端请求获取响应。我通过调用 `Task.All` 方法来实现这一点。在内部，该方法创建一个 `Task<String[]>` 对象，该对象在列表的所有对象完成后完成。我们 `await` 这个 `Task[]` 对象，这样状态机就会在所有任务完成后执行。我们一次性遍历所有的响应并处理它们（调用 `Console.WriteLine`）。

也许你更喜欢在每个响应发生时处理它，而不是等待它们全部完成。实现这一点就像使用 `Task.WhenAny` 一样简单。修改后的代码如下：

```
public static async Task Go() {
    // 启动服务器，它立即返回，因为
    // 它异步等待客户端请求
    StartServer();

    // 创建大量的异步请求；保存每个请求的 Task<String>
    List<String> requests = new List<String>(10000);

¹⁰观察：当我在我的机器上测试此代码时，我那台8 处理器机器的 CPU 使用率飙升到了 100%，当然。因为 CPU 忙碌，机器变热了，风扇也响了！处理完成后，CPU 使用率下降了，风扇也安静了。乐趣是验证一切都按预期运行的一种新价值。


```csharp

for(Int32 n = 0; n < requests.Capacity; n++)

    requests.Add(ClientRequestAsync("localhost", "Request #" + n));

```

```csharp

// 在每个任务完成时继续执行

while (requests.Count > 0) {

    // 按顺序处理每个完成的响应

    Task<String> response = await Task.WhenAny(requests);

    requests.Remove(response); // 从集合中移除完成的任务

    // 处理单个客户端的响应

    Console.WriteLine(response.Result);

}

```

在这里，我创建了一个 while 循环，按客户端请求进行迭代。在循环内部，我 await 了 `Task.WhenAny` 方法，该方法一次返回一个 `Task<String>` 对象，表示服务器已响应某个客户端请求。获取该 `Task<String>` 对象后，我将其从集合中移除，并查询其结果以进行处理（传递给 `Console.WriteLine`）。

# 应用程序及其线程模型

.NET Framework 支持多种应用程序模型，Windows 服务可能会施加其自己的线程模型。控制台应用程序和 Windows 服务（实际上是控制台应用程序；只是你看不到控制台）不施加任何类型的线程模型；也就是说，它们想做什么做什么就做什么。

然而，GUI 应用程序（包括 Windows Forms、Windows Presentation Foundation (WPF)、Silverlight 和 Windows Apps）施加了一种线程模型，即创建 UI 元素的线程是更新该 UI 元素的唯一线程。GUI 线程产生一个异步操作是常见做法，这样 GUI 线程就不会阻塞并停止响应用户输入（如鼠标、击键、笔触和触摸事件）。但是，当异步操作完成时，线程池线程会完成 Task 状态机。

对于某些应用程序模型，这是可以接受的甚至是理想的，因为它是高效的。对于其他应用程序模型（如 GUI 应用程序），这是一个问题，因为如果代码尝试通过线程池更新 UI 元素，将抛出异常。在某种程度上，线程池必须让 GUI 线程来更新 UI 元素。

ASP.NET 允许任何线程随心所欲。当线程池开始处理客户端请求时，它可以假设客户端的区域（`System.Globalization.CultureInfo`），允许 Web 服务器返回特定区域的数字、日期和时间格式。¹¹ 此外，Web 服务器可以假设客户端的身份（`System.Security.Principal.IPPrincipal`），因此服务器可以访问其被允许访问的资源。当线程池产生异步操作时，它可能由另一个线程池完成，这将是异步操作的结果。当

>代表原始客户端请求执行工作时，区域和身份会“流”到新的线程池，因此代表客户端执行的任何额外工作将使用客户端的区域和身份信息进行。

> ¹ 更多信息，请访问 http://msdn.microsoft.com/en-us/library/bz9tc508.aspx。

幸运的是，FCL 定义了一个名为 `System.Threading.SynchronizationContext` 的基类，解决了所有这些问题。简单来说，派自 `SynchronizationContext` 的对象将应用程序模型与其线程模型连接起来。FCL 定义了几个派自 `SynchronizationContext` 的类，但通常你不会直接使用这些类；事实上，其中许多类并没有公开暴露或文档说明。

在大多数情况下，应用程序开发者不需要了解关于 `SynchronizationContext` 类的任何知识。当你 `await` 一个 Task 时，会获取调用线程的 `SynchronizationContext` 对象。当线程池完成 Task 时，会使用该 `SynchronizationContext` 对象，并为你的应用程序模型使用正确的线程模型。因此，当 GUI `await` 一个 Task 时，`await` 算符后面的代码保证在 GUI 线程上执行，从而允许该代码更新 UI 元素.¹¹² 对于 ASP.NET 应用程序，`await` 算符后面的代码保证在关联了客户端区域和主体信息的线程池上执行。

在大多数时候，使用应用程序模型线程模型的状态机是极其有用且方便的。但在某些情况下，这可能会让你陷入麻烦。这是一个导致 WPF 应用程序死锁的示例。

12 在内部，各种派自 `SynchronizationContext` 的类使用 `System.Forms.Control.BeginInvoke`、`System.Windows.Threading.Dispatcher.BeginInvoke` 和 `Windows.UI.Core.Dispatcher.RunAsync` 等方法让 GUI 线程返回状态机。

```csharp

private sealed class MyWpfWindow : Window {

    public MyWpfWindow() { Title = "WPF Window"; }

    protected override void OnActivated(EventArgs e) {

        // 查询 Result 属性会阻止 GUI 线程返回；

        // 线程阻塞等待结果

        string http = GetHttp().Result; // 同步获取字符串！

        base.OnActivated(e);

    }

    private async Task<string> GetHttp() {

        // HTTP 请求并让线程从 GetHttp 返回

        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Intellect.com/");

        // 我们永远无法结果：GUI 线程正在等待此方法完成，但此方法

        // 无法完成，因为 GUI 线程正在等待它完成——死锁！

        return await msg.Content.ReadAsStringAsync();

    }

}
```
