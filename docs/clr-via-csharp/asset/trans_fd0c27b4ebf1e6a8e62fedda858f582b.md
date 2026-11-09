
## C# 对 volatile 字段的支持

确保程序员正确调用 **VolatileRead** 和 **VolatileWrite** 方法是一项很高的要求。程序员很难把这一切都记在脑子里，并开始想象其他线程可能在后台对共享数据做什么。为了简化这一点，C# 编译器提供了 **volatile** 关键字，它可以应用于以下任意类型的静态或实例字段：**Byte, SByte, Int16, UInt16, Int32, UInt32, Char, Single,** 或 **Boolean**。你也可以将 **volatile** 关键字应用于引用类型和任何枚举字段，只要该枚举类型的底层类型为 **Byte, SByte, Int16, UInt16, Int32, UInt32, Single,** 或 **Boolean**。JIT 编译器确保对 volatile 字段的所有访问都作为 volatile 读取和写入执行，因此不必显式调用 **Thread** 的静态 **VolatileRead** 或 **VolatileWrite** 方法。此外，**volatile** 关键字告诉 C# 和 JIT 编译器不要将该字段缓存在 CPU 寄存器中，从而确保对该字段的所有读取和写入实际上都会从内存中读取该值。

使用 **volatile** 关键字，我们可以按如下方式重写 **ThreadsSharingData** 类：

```csharp
internal sealed class ThreadsSharingData {
    private volatile Int32 m_flag = 0;
    private          Int32 m_value = 0;

    // This method is executed by one thread
    public void Thread1() {
        // Note: 5 must be written to m_value before 1 is written to m_flag
        m_value = 5;
        m_flag = 1;
    }

    // This method is executed by another thread
    public void Thread2() {
        // Note: m_value must be read after m_flag is read
        if (m_flag == 1)
            Console.WriteLine(m_value);
    }
}
```

有些开发者（我也是其中之一）不喜欢 C# 的 **volatile** 关键字，他们认为该语言不应提供它。我们的数组：每个请求一个响应
    private WebResponse[] m_results = new WebResponse[2];

    public MultiWebRequests(Int32 timeout = Timeout.Infinite) {
        // Asynchronously initiate all the requests all at once
        for (Int32 n = 0; n < m_requests.Length; n++) {
            m_ac.AboutToBegin(1);
            m_requests[n].BeginGetResponse(EndGetResponse, n);
        }

        // Tell the helper class that all operations have been initiated
        // and to call AllDone when all operations complete, Cancel is
        // called, or the timeout occurs
        m_ac.AllBegun(AllDone, timeout);
    }

    // Calling this method indicates that the results don't matter anymore
    public void Cancel() { m_ac.Cancel(); }

    // As each Web server responds, this method is called
    private void EndGetResponse(IAsyncResult result) {
        // Get the index corresponding to the request
        Int32 n = (Int32)result.AsyncState;

        // Store the response in the same index as the request
        m_results[n] = m_requests[n].EndGetResponse(result);

        // Tell the helper class that a Web server responded
        m_ac.JustEnded();
    }
}
```

```csharp
// This method is called after all Web servers respond,
// Cancel is called, or the timeout occurs
private void AllDone(CoordinationStatus status) {
    switch (status) {
        case CoordinationStatus.Cancel:
            Console.WriteLine("The operation was canceled"); break;

        case CoordinationStatus.Timeout:
            Console.WriteLine("The operation timed-out"); break;

        case CoordinationStatus.AllDone:
            Console.WriteLine("Here are the results from all the Web servers");
            for (Int32 n = 0; n < m_requests.Length; n++) {
                Console.WriteLine("{0} returned {1} bytes.",
                    m_results[n].ResponseUri, m_results[n].ContentLength);
            }
            break;
    }
}
```

好的，上面的代码实际上并没有直接使用任何 **Interlocked** 方法，因为我把所有协调代码封装在一个名为 **AsyncCoordinator** 的可复用类中，我很快就会解释它。让我先解释这个类在做什么。当构造 **MultiWebRequests** 类时，它会初始化一个 **AsyncCoordinator**、**WebRequest** 对象数组和 **WebResponse** 对象数组。然后，它通过调用 **BeginGetResponse** 异步发出所有 Web 请求。就在发出每个请求之前，它会调用 **AsyncCoordinator** 的 **AboutToBegin** 方法，并向其传递即将发出的请求数。⁶

在所有 Web 服务器的请求都已发出之后，会调用 **AsyncCoordinator** 的 **AllBegun** 方法，并向其传递所有操作完成时应执行的方法名称（**AllDone**）以及超时值。当每个 Web 服务器响应时，各种线程池线程将调用 **MultiWebRequests** 类的 **EndGetResponse** 方法。此方法确定它正在处理哪个请求（通过检查 **IAsyncResult** 的 **AsyncState** 属性），然后将 **WebResponse** 对象保存在 **m_results** 数组中。存储每个结果后，会调用 **AsyncCoordinator** 的 **JustEnded** 方法，以让 **AsyncCoordinator** 对象知道某个操作已完成。

如果所有操作都已完成，那么 **AsyncCoordinator** 将调用 **AllDone** 方法来处理来自所有 Web 服务器的结果。执行 **AllDone** 方法的代码将是恰好获得最后一个 Web 服务器响应的线程池线程。如果发生超时或取消，那么 **AllDone** 将通过通知 **AsyncCoordinator** 超时的任意线程池线程，或使用恰好调用 **Cancel** 方法的任意线程来调用。还有一种可能：如果最后一个请求在调用 **AllBegun** 之前完成，那么发出 Web 服务器请求的线程也可能自行调用 **AllDone**。
