
堆，这会导致发生更多垃圾回收。结果：应用程序性能更差。因此，如果你确知你的 I/O 操作会执行得极快，那么同步执行它们可能更合理。许多开发者（包括我自己）希望 APM 返回的是值类型，或者有其他某种轻量级方式来标识已排队的异步操作；也许微软有朝一日会通过支持这一点来改进 CLR。

## 有些 I/O 操作必须同步执行

Win32 API 提供了许多执行 I/O 操作的函数。不幸的是，其中一些方法不允许你异步执行 I/O。例如，Win32 `CreateFile` 方法（由 `FileStream` 的构造函数调用）始终同步执行。如果你尝试在网络服务器上创建或打开文件，`CreateFile` 返回前可能会花费数秒——在此期间调用线程一直空闲。为获得最佳性能和可伸缩性而设计的应用程序，理想情况下应调用一个允许异步创建或打开文件的 Win32 函数，这样你的线程就不会一直坐着等待服务器回复。不幸的是，Win32 没有类似 `CreateFile` 的函数让你做到这一点，因此 FCL 无法提供高效异步打开文件的方式。

下面是一个确实会出问题的例子。想象编写一个简单的 UI 控件，允许用户输入文件路径并提供自动补全（类似于常见的“文件打开”对话框）。该控件必须使用单独的线程来枚举目录以查找文件，因为 Windows 不提供任何异步枚举文件的函数。当用户继续在 UI 控件中输入时，你必须使用更多线程，并忽略任何先前创建的线程的结果。在 Windows Vista 中，微软引入了一个名为 `CancelSynchronousIo` 的新 Win32 函数。此函数允许一个线程取消另一个线程正在执行的同步 I/O 操作。FCL 未公开此函数，但如果你想从托管代码中利用它，也可以通过 P/Invoke 调用它。我将在本章下一节展示它的 P/Invoke 签名。

不过，我想让你记住的一点是，许多人认为同步 API 更易于使用，而在许多情况下确实如此。但在某些情况下，同步 API 会让事情变得困难得多。微软的 Windows 团队正在审视仅支持同步的 API，并决定在未来的 Windows 版本中哪些函数需要以异步 API 的形式公开。一旦他们完成这项工作，FCL 也会公开此功能。

你始终可以通过委托的 `BeginInvoke` 方法异步调用任何方法，但这样做时，你是在使用一个线程，因此会损失一些效率。而且实际上，你不能使用委托来调用构造函数。因此，异步构造 `FileStream` 对象的唯一方式是异步调用另一个方法，并让这另一个方法构造 `FileStream` 对象。Windows 不提供异步访问注册表、访问事件日志、获取目录的文件/子目录或更改文件/目录属性的函数，这里仅举几例。

从 Windows Vista 开始，线程现在可以在发出 I/O 请求时指定优先级。有关 I/O 优先级的更多详细信息，请参阅白皮书 http://www.microsoft.com/whdc/driver/priorityio.mspx。不幸的是，FCL 尚未包含此功能；希望它会在未来版本中添加。不过，你仍然可以通过 P/Invoke 调用本机 Win32 函数来利用此功能。以下是 P/Invoke 代码：

```csharp
internal static class ThreadIO {
    public static BackgroundProcessingDisposer BeginBackgroundProcessing(
        Boolean process = false) {

        ChangeBackgroundProcessing(process, true);
        return new BackgroundProcessingDisposer(process);
    }

    public static void EndBackgroundProcessing(Boolean process = false) {
        ChangeBackgroundProcessing(process, false);
    }

    private static void ChangeBackgroundProcessing(Boolean process, Boolean start) {
        Boolean ok = process
            ? SetPriorityClass(GetCurrentWin32ProcessHandle(),
                start ? ProcessBackgroundMode.Start : ProcessBackgroundMode.End)
            : SetThreadPriority(GetCurrentWin32ThreadHandle(),
                start ? ThreadBackgroundMode.Start : ThreadBackgroundMode.End);
        if (!ok) throw new Win32Exception();
    }

    // This struct lets C#'s using statement end the background processing mode
    public struct BackgroundProcessingDisposer : IDisposable {
        private readonly Boolean m_process;
        public BackgroundProcessingDisposer(Boolean process) { m_process = process; }
        public void Dispose() { EndBackgroundProcessing(m_process); }
    }

    // See Win32's THREAD_MODE_BACKGROUND_BEGIN and THREAD_MODE_BACKGROUND_END
    private enum ThreadBackgroundMode { Start = 0x10000, End = 0x20000 }

    // See Win32's PROCESS_MODE_BACKGROUND_BEGIN and PROCESS_MODE_BACKGROUND_END
    private enum ProcessBackgroundMode { Start = 0x100000, End = 0x200000 }

    [DllImport("Kernel32", EntryPoint = "GetCurrentProcess", ExactSpelling = true)]
    private static extern SafeWaitHandle GetCurrentWin32ProcessHandle();

    [DllImport("Kernel32", ExactSpelling = true, SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern Boolean SetPriorityClass(
        SafeWaitHandle hprocess, ProcessBackgroundMode mode);

    [DllImport("Kernel32", EntryPoint = "GetCurrentThread", ExactSpelling = true)]
    private static extern SafeWaitHandle GetCurrentWin32ThreadHandle();

    [DllImport("Kernel32", ExactSpelling = true, SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern Boolean SetThreadPriority(
        SafeWaitHandle hThread, ThreadBackgroundMode mode);

    // http://msdn.microsoft.com/en-us/library/aa480216.aspx
    [DllImport("Kernel32", SetLastError = true, EntryPoint = "CancelSynchronousIo")]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern Boolean CancelSynchronousIo(SafeWaitHandle hThread);
}
```

以下代码展示如何使用它：

```csharp
public static void Main () {
    using (ThreadIO.BeginBackgroundProcessing()) {
        // Issue low-priority I/O requests in here (eg: calls to BeginRead/BeginWrite)
    }
}
```

你通过调用 **ThreadIO 的 BeginBackgroundProcessing** 方法来告诉 Windows，你希望你的线程发出低优先级 I/O 请求。请注意，这还会降低线程的 CPU 调度优先级。你可以通过调用 **EndBackgroundProcessing**，或对 **BeginBackgroundProcessing** 返回的值调用 **Dispose**（如上文通过 C# 的 **using** 语句所示），使线程恢复发出正常优先级 I/O 请求（以及正常 CPU 调度优先级）。线程只能影响自身的后台处理模式；Windows 不允许一个线程更改另一个线程的后台处理模式。

如果你希望进程中的所有线程都发出低优先级 I/O 请求并具有低 CPU 调度优先级，可以调用 **BeginBackgroundProcessing**，并将 **process** 参数传入 **true**。进程只能影响自身的后台处理模式；Windows 不允许一个线程更改另一个进程的后台处理模式。

> **重要** 作为开发者，你有责任使用这些新的后台优先级来让前台应用程序响应更灵敏，同时注意避免*优先级反转*。在存在大量正常优先级 I/O 的情况下，以后台优先级运行的线程可能会被延迟*数秒*才能获得其 I/O 请求的结果。如果一个低优先级线程获取了正常优先级线程正在等待的线程同步锁，那么正常优先级线程可能最终要等待后台优先级线程，直到低优先级 I/O 请求完成。你的后台优先级线程甚至不必提交 I/O 就可能发生此问题。因此，应尽量减少（如果可能则消除）正常优先级线程与后台优先级线程之间共享同步对象的使用，以避免这些正常优先级线程被后台优先级线程持有的锁阻塞的优先级反转。

