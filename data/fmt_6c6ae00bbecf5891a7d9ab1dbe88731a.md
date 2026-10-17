
你必须避免使用参数和局部变量，因为这些变量分配在另一个线程的栈上，无法被另一个线程或另一个方法访问。

## 第五部分 多线程

- 许多 C# 语言结构如 `try/catch/finally`、`using`、`for`、`do`、`while` 和 `foreach`，如果你想在一个方法中开始并在另一个方法结束，则无法使用。例如，在我的 `Server` 类中，我想使用 `using` 语句打开管道，然后让它在 `finally` 块中自动关闭。然而，我无法使用 `using`，因为我在 `Server` 的构造函数中打开管道，并在另一个方法 `WriteDone` 中关闭它。

- 很難实现许多开发者通常需要的其他功能，例如协调并发操作、支持取消和超时，以及将工作封送到 GUI 线程以更新控件。

这些是许多开发者避免 APM 的主要原因。然而，我创建了一个名为 `AsyncEnumerator` 的类，它简化了这一切并修复了上述所有问题。简而言之，我的 `AsyncEnumerator` 允许你利用 C# 的迭代器语言，通过同步编程模型执行异步操作。该类是我 Power Threading 库的一部分，并且完全免费使用。该库的版本支持桌面 CLR、Silverlight 和 Microsoft Framework。你可以从 `http://dotnet/PowerThreading.aspx` 下载库的最新版本和示例代码。该网页包含 MSDN 杂志《并发事务》专栏的链接，我在其中解释了 `AsyncEnumerator` 类是如何工作的。我还展示了一些如何使用它的视频，以及一个我提供免费技术支持的小组链接。

目前，让我分享 `AsyncEnumerator` 提供的某些功能，以便它可以与所有 .NET Framework 技术（如 ASP.Net 和 Windows Communication Foundation (WCF)）集成。这还允许异步子程序的组合，因为一个 `AsyncEnumerator` 可以调用另一个 `AsyncEnumerator`。

- 它协调多个并发的异步操作。也就是说，你可以发出许多异步操作，`AsyncEnumerator` 可以在所有操作完成后通知你，或者在每个操作完成时通知你。

- 它支持丢弃组（discard groups），这允许你发布一组异步操作，并让 `AsyncEnumerator` 对象在结果完成时丢弃它们。例如，你可以在单个丢弃组内从三个不同的 Web 服务器请求伦敦的温度。哪个服务器返回最快，就为你的应用程序提供继续处理所需的信息。然后你可以取消该丢弃组中剩余剩余的操作。

- 它允许你通过调用每个操作的 `EndXx` 方法（并忽略异常）来自动取消一组异步操作，前提是你不在乎结果。这对于 GUI 应用程序特别有用，因为它允许用户在厌倦等待结果时取消操作。此外，你还可以设置在指定的超时间隔后自动发生取消。这对于希望在特定时间内用服务器拥有的任何信息响应客户端的服务器应用程序特别有用。

## 第 27 章 I/O 密集型异步操作

- 它让你无需担心本章稍后“应用程序及其线程模型”部分中讨论的应用程序线程模型。例如，在 GUI 应用程序中，`AsyncEnumerator` 默认通过 GUI 线程调用你，以便你可以更新 UI 控件。对于 ASP.NET Web Form 或 XML Web 服务，`AsyncEnumerator` 会自动确保你的代码运行在客户端的线程和身份下。

- 它具有丰富的错误处理支持。如果迭代器返回而异步操作随后继续，`AsyncEnumerator` 类将抛出异常，通知你无法调用 `Endxx` 方法，因此应用程序正在离开资源。

- 它具有丰富的调试支持。通常，内存中会有许多 `AsyncEnumerator` 对象。对于服务器应用程序来说尤其如此。在调试器中，你可以查询 `AsyncEnumerator` 的静态方法 `GetInProgressList`，它返回当前所有 `AsyncEnumerator` 列表。列表按等待操作时间最长的对象排序。如果你的应用程序看起来很忙，查看列表顶部的项将带你进入等待操作完成的代码位置。当你在调试器查看单个 `AsyncEnumerator` 对象时，它会显示标识操作的用户定义标签、执行上次异步操作的时间、哪些操作已完成以及哪些操作尚未完成。它还会显示启动异步操作源代码文件和行号。

使用你的 `AsyncEnumerator` 类实现的私有代码所示：

```cs
private static IEnumerator<Int32> PipeServerAsyncEnumerator(AsyncEnumerator ae) {
    // 每个服务器对象在该管道上执行异步操作
using (var pipe = new NamedPipeServerStream(
        "Echo", PipeDirection.Out, -1, PipeTransmissionMode.Message,
        PipeOptions.Asynchronous | PipeOptions.WriteThrough)) {

        // 异步接受客户端连接
        pipe.BeginWaitForConnection(ae.End(), null);
        yield return 1;

        // 客户端已连接，让我们接受另一个客户端
        var aeNewClient = new AsyncEnumerator();
        aeNewClient.BeginExecute(PipeServerAsyncEnumerator(aeNewClient),
        aeNewClient.Execute());

        // 接受客户端连接
        pipe.EndWaitForConnection(ae.DequeueAsyncResult());
    }
}
```

> 4 本书的示例代码包含了使用 `AsyncEnumerator` 实现的管道代码。该版本的代码与此处所示的结构相同。

```csharp
pipe.BeginRead(data, 0, data.Length, ae.End(), null);
yield return 1;
```

// 客户端向我们发送了请求，处理它。

Int32 bytesRead = pipe.EndRead(ae.DequeueAsyncResult());

我的服务器只是将所有字符转换为大写字母

// 但是，你可以用任何计算密集型操作替换此代码

data = Encoding.UTF8.GetBytes(Encoding.UTF8.GetString(data, 0, bytesRead).ToUpper().ToCharArray());

```

```csharp

// 异步向客户端发送响应

ipe.BeginWrite(data, 0, data.Length, ae.End(), null);

yield return 1;

```

```csharp

// 响应已发送到客户端，关闭我们这一侧的连接

ipe.EndWrite(ae.DequeueAsyncResult());

// 关闭操作现在发生在 finally 块中！

```

关于这个版本的代码，有几点需要注意：

- 所有的代码都在一个方法中，而不是分散在类中的多个方法。由于没有类，所以没有字段；所有的变量都是局部变量。
- 在我本该进行方法分离的地方，现在使用 `yield return 1` 语句。这允许线程返回到来源处，以便它可以执行更多工作。
- 对于每一个 BeginXX 方法，我都传递了 `ae.End()`；此方法返回一个指向 `AsyncEnumerator` 对象内部方法的委托。当操作完成时，线程池会通知 `AsyncEnumerator` 对象，随后它会在 `yield return 1` 语句之后继续执行你的迭代器。
- 我向每个 BeginXX 方法的最后一个参数传递了 `null`。因此，我不需要调用 `IAsyncResult` 的 `AsyncState` 属性并将其值转换为正确的类型；我使用局部变量。
- 对于每个 EndXX 方法，我传递了调用 `ae.DequeueAsyncResult()` 的结果。此方法返回在异步操作完成时传递给线程池的 `AsyncResult`。
- 最后，注意我可以使用 C# 的 `using` 语句来控制 `NamedPipeStream` 的生命周期。这意味着如果任何其他线程抛出意外异常，`NamedPipeStream` 对象将在 `finally` 块中被关闭。

这让你很好地了解了 `AsyncEnumerator` 类可以做什么以及它如何简化异步编程。上面的代码甚至没有展示一些更令人兴奋的特性。如果你感兴趣了解更多信息，我鼓励你访问之前提到的 Intellect 网站。

# APM 与异常

每当你调用一个 `BeginXXX` 方法时，它当然可能会抛出异常。如果发生这种情况，你可以假设异步操作尚未入队，因此线程池将不会调用你可能传递给 `BeginXXX` 方法的任何回调方法。

当 Windows 设备驱动程序处理异步 I/O 请求时，可能会出现问题，Windows 需要将此情况通知你的应用程序。例如，在发送或等待字节通过网络传输时，可能会发生超时。如果数据没有及时到达，设备驱动程序将告诉你异步操作带错误完成。为了实现这一点，设备驱动程序将已完成的 IRP 发送到 CLR 线程池，并有效地在 `IAsyncResult` 对象中放置一个错误代码。随后，线程池将调用你的回调方法，并传递 `IAsyncResult` 对象。你的回调方法将把 `IAsyncResult` 对象传递给适当的 `EndXXX` 方法，该方法将看到错误代码，将其转换为相应的 `Exception` 派生对象，然后抛出此异常。

结果是，异常的处理方式与同步编程相同。然而，你通常不关心从 `BeginXXX` 调用抛出的异常，但你通常关心从 `EndXXX` 调用抛出的异常。以下代码演示了异常处理和 APM 的使用：

```csharp

internal static class ExceptionHandling {

    public static void Main() {

        // 尝试访问无效的 IP 地址

        WebRequest webRequest = WebRequest.Create("http://0.0.0.0/");

        webRequest.BeginGetResponse(ProcessResponse, webRequest);

        Console.ReadLine();

    }

    private static void ProcessResponse(IAsyncResult result) {

        WebRequest webRequest = (WebRequest)result.AsyncState;

        Response webResponse = null;

        try {

            webResponse = webRequest.EndGetResponse(result);

            Console.WriteLine("Content length: " + webResponse.ContentLength);

        } catch (WebException we) {

            Console.WriteLine(we.GetType() + ": " + we.Message());

        }

        finally {

            if (webResponse != null) webResponse.Close();

        }

    }

}

```

# 第 V 部分 线程

当我运行该程序时，我得到了以下输出：

System.Net.WebException: Unable to connect to the remote server

> 注意：在执行多个异步超文本传输协议 (HTTP) 请求时，存在一个常见问题，这让许多开发者感到意外。HTTP (RFC 2616) 规定客户端应用程序到单个服务器的并发连接不应超过两个。FCL 中的类实际上强制执行了这一点，任何尝试为特定服务器创建额外连接的线程都会被阻塞，直到其中两个连接之一关闭。你应该设计你的应用程序，使其在任何时间对单个服务器的待处理连接都不超过两个，或者通过设置 `System.Net.ServicePoint` 的静态属性 `DefaultConnectionLimit` 为应用程序所需的数值来增加最大并发连接数。

# 应用程序及其线程模型

NET Framework 支持多种不同的应用程序模型，每个应用程序都可能施加自己的线程模型。控制台应用程序和 Windows 服务（实际上是控制台应用程序；你只是这样运行它们）不施加任何线程模型。然而，GUI 应用程序包括 Windows Forms、Windows Presentation Foundation (WPF) 和 Silverlight 施加线程模型，即只有 GUI 线程允许更新窗口。像控制台应用程序，ASP.NET Web Services 允许任何线程随心所欲。当线程池需要让 GUI 线程更新 UI 时，你会让线程池使用保存的 `SynchronizationContext` 派生对象并调用其 `Post` 方法。像控制台应用程序，ASP.NET Web Services 允许任何线程随心所欲。当线程池开始处理请求时，它可以假设客户端的身份。

# 第 27 章 I/O 边界异步操作

幸运的是，FCL 定义了一个基类 `System.Threading.SynchronizationContext`，它解决了这些问题。简单来说，`SynchronizationContext` 将应用程序模型连接到线程模型。FCL 定义了多个派自 `SynchronizationContext` 的类，但你通常不需要处理这些类。这里是 `SynchronizationContext` 类的结构（仅显示相关的成员）：

```csharp

public class SynchronizationContext {

    public static SynchronizationContext Current { get; }

    public virtual void Post(SendPostCallback d, object state); // 异步调用

    public virtual void Send(SendPostCallback d, object state); // 同步调用

}

```

```csharp

// SendPostCallback 是这样的委托：

public delegate void SendPostCallback(object state);
```
