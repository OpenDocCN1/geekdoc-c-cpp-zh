
- 它让你不必担心应用程序的线程模型（如本章后面“应用程序及其线程模型”一节所述）。例如，在 GUI 应用程序中，**AsyncEnumerator** 默认在 GUI 线程上调用你的代码，因此你可以更新 UI 控件。对于 ASP.NET Web Form 或 XML Web Service 应用程序，**AsyncEnumerator** 会自动确保你的代码在客户端的区域性和标识下运行。

- 它具有丰富的错误处理支持。如果你的迭代器返回，而某个异步操作随后完成，**AsyncEnumerator** 类会抛出异常，通知你无法调用 **EndXxx** 方法，因此你的应用程序正在泄漏资源。

- 它具有丰富的调试支持。通常，一个应用程序会在内存中有许多 **AsyncEnumerator** 对象。服务器应用程序尤其如此。在调试器中，你可以查询 **AsyncEnumerator** 的静态 **GetInProgressList** 方法，它返回当前存在的所有 **AsyncEnumerator** 对象的列表。该列表经过排序，等待操作完成时间最长的对象位于顶部。如果你的应用程序看起来已挂起，查看列表顶部的项通常会将你直接带到代码中正在等待操作完成的那一行。此外，当你在调试器中查看单个 **AsyncEnumerator** 对象时，它会显示一个用户可定义的标记，用于标识该操作、它执行的上一次异步操作的时间戳、哪些操作已完成以及哪些操作尚未完成。它还会向你显示源代码文件以及该文件中启动异步操作的行。

下面是为与我的 **AsyncEnumerator** 类配合使用而实现时，管道服务器代码的样子：

```csharp
private static IEnumerator<Int32> PipeServerAsyncEnumerator(AsyncEnumerator ae) {
    // Each server object performs asynchronous operations on this pipe
    using (var pipe = new NamedPipeServerStream(
        "Echo", PipeDirection.InOut, -1, PipeTransmissionMode.Message,
        PipeOptions.Asynchronous | PipeOptions.WriteThrough)) {

        // Asynchronously accept a client connection
        pipe.BeginWaitForConnection(ae.End(), null);
        yield return 1;

        // A client connected, let's accept another client
        var aeNewClient = new AsyncEnumerator();
        aeNewClient.BeginExecute(PipeServerAsyncEnumerator(aeNewClient),
            aeNewClient.EndExecute);

        // Accept the client connection
        pipe.EndWaitForConnection(ae.DequeueAsyncResult());

        // Asynchronously read a request from the client
        Byte[] data = new Byte[1000];
```

⁴ 本书的示例代码包含重新实现为使用 AsyncEnumerator 的管道客户端代码。此版本的代码遵循此处展示的相同结构。

幸运的是，FCL 定义了一个名为 **System.Threading.SynchronizationContext** 的基类，它解决了所有这些问题。简而言之，一个派生自 **SynchronizationContext** 的对象将应用程序模型连接到其线程模型。FCL 定义了几个派生自 **SynchronizationContext** 的类，但通常你不会直接与这些类打交道；事实上，其中许多类并未公开暴露或记录在文档中。下面是 **SynchronizationContext** 类的样子（我只展示与本次讨论相关的成员）：

```csharp
public class SynchronizationContext {
    public static SynchronizationContext Current { get; }
    public virtual void Post(SendOrPostCallback d, object state); // Call asynchronously
    public virtual void Send(SendOrPostCallback d, object state); // Call synchronously
}

// SendOrPostCallback is a delegate defined like this:
public delegate void SendOrPostCallback(Object state);
```

对于 Windows Forms 应用程序、WPF 应用程序和 Silverlight 应用程序，GUI 线程会有一个与之关联的派生自 **SynchronizationContext** 的类。你可以让 GUI 线程查询 **SynchronizationContext** 的静态 **Current** 属性，从而获得对该对象的引用。然后，你会将对 this object 的引用保存到某个共享变量中（比如你自己类中的 **static** 字段）。然后，每当线程池线程需要让 GUI 线程更新 UI 时，你会让该线程池线程引用已保存的派生自 **SynchronizationContext** 的对象，并调用其 **Post** 方法，传入应由 GUI 线程调用的方法（匹配 **SendOrPostCallback** 委托的签名）以及应传递给该方法的参数。

我建议调用 **Post** 方法，因为它会将回调排队到 GUI 线程，并允许线程池线程立即返回。另一方面，**Send** 会将回调排队到 GUI 线程，然后阻塞线程池线程，直到 GUI 线程完成对回调的调用。阻塞线程池线程很可能导致线程池创建新线程，从而增加资源消耗并降低性能。这就是为什么我总是避免调用 **Send** 方法。

> **注意** 给好奇的读者：下面是各种派生自 **SynchronizationContext** 的类如何让 GUI 线程调用 **SendOrPostCallback** 方法。对于 Windows Forms，**System.Windows.Forms.WindowsFormsSynchronizationContext** 类的 **Post** 方法在内部调用 **System.Windows.Forms.Control** 的 **BeginInvoke** 方法，而其 **Send** 方法在内部调用 **Control** 的 **Invoke** 方法。对于 WPF 和 Silverlight，**System.Windows.Threading.DispatcherSynchronizationContext** 类的 **Post** 方法在内部调用 **System.Windows.Threading.Dispatcher** 的 **BeginInvoke** 方法，而其 **Send** 方法在内部调用 **Dispatcher** 的 **Invoke** 方法。

### 调用 Endxxx 方法时始终使用同一个对象

无论调用 **Beginxxx** 时使用什么对象，都应是调用 **Endxxx** 时使用的同一个对象。例如，不要构造一个委托并调用其 **BeginInvoke** 方法，然后构造另一个委托（类型相同、引用同一对象/方法）并用它调用其 **EndInvoke** 方法。虽然这看起来似乎可行（因为两个委托对象在各方面都完全相同），但它并不可行，因为 **IAsyncResult** 对象在内部保留了对调用 **BeginInvoke** 时所使用的原始对象的引用；如果二者不匹配，**EndInvoke** 会抛出 **InvalidOperationException**，其字符串消息为 **“提供的 IAsyncResult 对象与此委托不匹配。”** 同样，使用一个对象调用 **BeginInvoke**、另一个对象调用 **EndInvoke**，对某些对象类型可能可行，具体取决于它们的实现方式。

### 将 ref、out 和 params 参数与 Beginxxx 和 Endxxx 方法一起使用

如果方法的非异步版本使用任何 **out/ref** 参数，或者带有标记为 **params** 关键字的参数，那么 **Beginxxx** 和 **Endxxx** 方法的参数会与我在本章中描述的模式略有偏差。由于这种情况非常罕见，我不会展示示例，但你应该注意这一点。当你需要时，很容易弄清楚如何正确调用这些方法。

### 无法取消异步 I/O 绑定操作

目前没有办法取消未完成的异步 I/O 绑定操作。这是许多开发者想要的功能，但实际上很难实现。毕竟，如果你向服务器请求 1,000 字节，然后决定不再需要这些字节，实际上没有办法告诉服务器忘记你的请求。处理方式就是让这些字节返回给你，然后丢弃它们。此外，这里存在竞态条件：你发出的取消请求可能恰好在读取最后一个字节时到来。那么你的应用程序应该怎么做？你需要在代码中处理这种可能发生的竞态条件，并决定是丢弃数据还是对其采取操作。某些 **Beginxxx** 方法可能返回一个实现 **IAsyncResult** 接口的对象，并且还提供某种取消方法。在这种情况下，你可以取消该操作。你必须查看 **Beginxxx** 方法或其返回类的文档，以确认是否支持取消。

### 内存消耗

每当你调用 **Beginxxx** 方法时，它都会构造一个实现 **IAsyncResult** 接口的类型的实例。这意味着你希望执行的每个异步操作都会创建一个对象。这会增加更多开销，并在……
