
当代表原始客户端请求执行工作时，区域性和标识需要“流动”到新的线程池线程，以便代表客户端执行的任何额外工作都使用客户端的区域性和标识信息。

幸运的是，FCL 定义了一个名为 `System.Threading.SynchronizationContext` 的基类，它解决了所有这些问题。简单来说，派生自 `SynchronizationContext` 的对象将应用程序模型与其线程模型连接起来。FCL 定义了若干派生自 `SynchronizationContext` 的类，但通常你不会直接与这些类打交道；事实上，其中许多类并未公开暴露或记录在文档中。

大多数情况下，应用程序开发者无需了解 `SynchronizationContext` 类的任何内容。当你等待（await）一个 `Task` 时，会获取调用线程的 `SynchronizationContext` 对象。当线程池线程完成该 `Task` 时，会使用 `SynchronizationContext` 对象，从而确保为你的应用程序模型采用正确的线程模型。因此，当 GUI 线程等待一个 `Task` 时，await 运算符后面的代码保证也会在 GUI 线程上执行，从而允许该代码更新 UI 元素。<sup>12</sup> 对于 ASP.NET 应用程序，await 运算符后面的代码保证会在一个关联了客户端区域性和主体信息的线程池线程上执行。

12 在内部，各种派生自 `SynchronizationContext` 的类使用 `System.Windows.Forms.Control.BeginInvoke`、`System.Windows.Threading.Dispatcher.BeginInvoke` 和 `Windows.UI.Core.CoreDispatcher.RunAsync` 等方法让 GUI 线程恢复状态机。

大多数时候，让状态机使用应用程序模型的线程模型恢复执行非常有用且方便。但在某些情况下，这可能会让你陷入麻烦。下面是一个导致 WPF 应用程序死锁的示例。

```csharp
private sealed class MyWpfWindow : Window {
    public MyWpfWindow() { Title = "WPF Window"; }

    protected override void OnActivated(EventArgs e) {
        // Querying the Result property prevents the GUI thread from returning;
        // the thread blocks waiting for the result
        String http = GetHttp().Result; // Get the string synchronously!

        base.OnActivated(e);
    }

    private async Task<String> GetHttp() {
        // Issue the HTTP request and let the thread return from GetHttp
        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/");
        // We never get here: The GUI thread is waiting for this method to finish but this method
        // can't finish because the GUI thread is waiting for it to finish --> DEADLOCK!

        return await msg.Content.ReadAsStringAsync();
    }
}
```

创建类库的开发者绝对需要了解 `SynchronizationContext` 类，以便编写能与所有应用程序模型配合工作的高性能代码。由于大量类库代码与应用程序模型无关，我们希望避免使用 `SynchronizationContext` 对象所带来的额外开销。此外，类库开发者应尽一切努力帮助应用程序开发者避免死锁情况。为了解决这两个问题，`Task` 和 `Task<TResult>` 类都提供了一个名为 `ConfigureAwait` 的方法，其签名如下所示。

```csharp
// Task defines this method:
public ConfiguredTaskAwaitable ConfigureAwait(Boolean continueOnCapturedContext);

// Task<TResult> defines this method:
public ConfiguredTaskAwaitable<TResult> ConfigureAwait(Boolean continueOnCapturedContext);
```

向此方法传递 true 所得到的行为与完全不调用该方法相同。但是，如果传递 false，await 运算符不会查询调用线程的 `SynchronizationContext` 对象，并且当线程池线程完成该 `Task` 时，它只是完成该任务，await 运算符之后的代码将通过线程池线程执行。

尽管我的 `GetHttp` 方法不是类库代码，但如果添加对 `ConfigureAwait` 的调用，死锁问题就会消失。以下是我的 `GetHttp` 方法的修改版本。

```csharp
private async Task<String> GetHttp() {
    // Issue the HTTP request and let the thread return from GetHttp
    HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/")
        .ConfigureAwait(false);
    // We DO get here now because a thread pool can execute this code
    // as opposed to forcing the GUI thread to execute it.

    return await msg.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

如前面的代码所示，必须对每个等待的 `Task` 对象应用 `ConfigureAwait(false)`。这是因为异步操作可能会同步完成，而当这种情况发生时，调用线程只是继续执行而不返回其调用方；你永远不知道哪个操作需要忽略 `SynchronizationContext` 对象，因此必须告诉所有操作忽略它。这也意味着你的类库代码应当与应用程序模型无关。

或者，我可以按如下方式重写我的 `GetHttp` 方法，使整个过程通过线程池线程执行。

```csharp
private Task<String> GetHttp() {
    return Task.Run(async () => {
        // We run on a thread pool thread now that has no SynchronizationContext on it
        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/");
        // We DO get here because some thread pool can execute this code

        return await msg.Content.ReadAsStringAsync();
    });
}
```

在这个版本的代码中，请注意我的 `GetHttp` 方法不是异步函数；我从方法签名中移除了 `async` 关键字，因为该方法不再包含 await 运算符。另一方面，我传递给 `Task.Run` 的 lambda 表达式是一个异步函数。

## 以异步方式实现服务器

多年来与许多开发者交流后，我发现很少有人意识到 .NET Framework 具有内置支持，可让你构建伸缩性非常好的异步服务器。在本书中，我无法解释如何为每一种服务器实现这一点，但我可以列出你应在 MSDN 文档中查找的内容。

- 构建异步 ASP.NET Web Forms：在 .aspx 文件中，向页面指令添加 `Async="true"`，并查阅 `System.Web.UI.Page` 的 `RegisterAsyncTask` 方法。
- 构建异步 ASP.NET MVC 控制器：让控制器类派生自 `System.Web.Mvc.AsyncController`，并只需让操作方法返回 `Task<ActionResult>`。
- 构建异步 ASP.NET 处理程序：让类派生自 `System.Web.HttpTaskAsyncHandler`，然后重写其抽象 `ProcessRequestAsync` 方法。
- 构建异步 WCF 服务：将服务实现为异步函数，并让其返回 `Task` 或 `Task<TResult>`。

### 取消 I/O 操作

一般来说，Windows 并未提供取消未完成 I/O 操作的方法。这是许多开发者希望拥有的功能，但实际上很难实现。毕竟，如果你向服务器发出请求，然后决定不再需要该响应，就无法告诉服务器放弃你原来的请求。处理方式就是让字节返回客户端计算机，然后将其丢弃。此外，这里存在竞态条件——你发出的取消请求可能恰好在服务器发送响应时到达。那么你的应用程序应该怎么做？你需要处理自己代码中可能发生的这种竞态条件，并决定是丢弃数据还是对其执行操作。

为帮助处理此问题，我建议实现一个扩展 `Task<TResult>` 的 `WithCancellation` 扩展方法（你还需要一个扩展 `Task` 的类似重载），如下所示。

```csharp
private struct Void { } // Because there isn't a non-generic TaskCompletionSource class.

private static async Task<TResult> WithCancellation<TResult>(this Task<TResult> originalTask,
    CancellationToken ct) {

    // Create a Task that completes when the CancellationToken is canceled
    var cancelTask = new TaskCompletionSource<Void>();

    // When the CancellationToken is canceled, complete the Task
    using (ct.Register(
        t => ((TaskCompletionSource<Void>)t).TrySetResult(new Void()), cancelTask)) {

        // Create a Task that completes when either the original or
        // CancellationToken Task completes
```
