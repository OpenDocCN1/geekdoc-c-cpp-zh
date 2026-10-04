

# I/O 请求优先级

在第 26 章“线程基础”中，我展示了设置线程优先级如何影响线程的调度。然而，线程也会执行 I/O 请求以从各种硬件设备读取和写入数据。如果一个低优先级的线程获得了 CPU 时间，它可能在短时间内轻松地队列成成百上千个 I/O 请求。由于 I/O 请求通常需要时间，低优先级线程可能会通过挂起高优先级线程并阻止其完成工作，从而显著影响系统的响应能力。正因如此，你会发现在执行长时间运行的低优先级服务（如磁盘碎片整理、杀病毒扫描程序、内容索引器等）时，机器的响应速度会变慢.¹13

Windows 允许在发出 I/O 请求时指定优先级。请参阅 http://www.microsoft.com/whc/driver/priorityin.mspx 处的白皮书。遗憾的是，FCL 目前尚未包含此功能；希望它会在未来的版本中添加。不过，你仍然可以通过 P/Invoking 调用原生 Win32 函数来利用这一特性。

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
            : SetPriorityClass(GetCurrentWin32ThreadHandle(),
                start ? ThreadBackgroundMode.Start : ThreadBackgroundMode.End);
        if (!ok) throw new Win32Exception();
    }
}
```

```csharp
// 此结构体让 C# using 语句结束后台处理模式
public struct BackgroundProcessingDisposer : IDisposable {
    private readonly Boolean m_process;
    public BackgroundProcessingDisposer(Boolean process) { m_process = process; }
    public void Dispose() { EndBackgroundProcessing(m_process); }
}
```

¹³ Windows SuperFetch 功能利用了低优先级的 I/O 请求。

```csharp
// 查看 Win32 的 THREAD_MODE_BACKGROUND_BEGIN 和 THREAD_MODE_BACKGROUND_END
private enum ThreadBackgroundMode { Start = 0x100000, End = 0x200000 }

// 查看 Win32 的 PROCESS_MODE_BACKGROUND_BEGIN 和 PROCESS_MODE_BACKGROUND_END
private enum ProcessBackgroundMode { Start = 0x100000, End = 0x200000 }
```

```csharp
[DllImport("Kernel32"), EntryPoint = "GetCurrentProcess", ExactSpelling = true]
private static SafeWaitHandle GetCurrentWin32ProcessHandle();
```

```csharp
[DllImport("Kernel32"), ExactSpelling = true, SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern Boolean SetPriorityClass(
    SafeWaitHandle hprocess, ProcessBackgroundMode mode);
```

```csharp
[DllImport("Kernel32"), EntryPoint = "GetCurrentThread", ExactSpelling = true]
private static SafeWaitHandle GetCurrentWin32ThreadHandle();
```

```csharp
[DllImport("Kernel32"), ExactSpelling = true, SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern Boolean SetThreadPriority(
    SafeWaitHandle hthread, ThreadBackgroundMode mode);
```

```csharp
// http://msdn.microsoft.com/en-us/library/aa48021.aspx
[DllImport("Kernel32"), SetLastError = true, EntryPoint = "CancelSynchronousIO"]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern Boolean CancelSynchronousIO(SafeWaitHandle hThread);
```

```csharp
// 这里是使用它的代码示例：

public static void Main() {
    using (ThreadIO.BeginBackgroundProcessing()) {
        // 此处执行低优先级 I/O 请求（例如：调用 ReadAsync/WriteAsync）
    }
}
```

你通过调用 `ThreadIO.BeginBackgroundProcessing` 方法来告诉程序你希望线程启动低优先级的 I/O 请求。注意，这会降低线程的 CPU 调度优先级。你可以通过调用 `EndBackgroundProcessing` 或对 `BeginBackgroundProcessing` 返回的值调用 `Dispose`（如代码 C# 的 using 状态所示）来让线程恢复到正常优先级的 I/O 请求（以及正常的 CPU 调度优先级）。线程只能影响自己的后台处理模式；Windows 不允许线程更改另一个线程的后台处理模式。

如果你希望所有线程都执行进程低优先级的 I/O 请求并具有低 CPU 调度，你可以调用 `BeginBackgroundProcessing` 并向 `process` 参数传递 `true`。进程只能影响其自身的后台处理模式；Windows 不允许线程更改另一个进程的后台处理模式。

> **重要** 作为开发者，你有责任使用这些新的后台优先级来让前台应用程序具有更高的响应性，并注意避免*优先级反转*。在存在大量的正常优先级 I/O 的情况下，如果运行在后台优先级的线程获取了某个线程同步锁，那么正常优先级线程将等待该锁，直到低优先级 I/O 请求完成。此时你的后台优先级线程正在等待，而正常优先级线程却在等待。

# 第 29 章

## 原生线程同步结构

在本章中：

- 类库与线程安全 ................................................. 759
- 原生用户态与内核态结构 ....................................... 760
- 用户态结构 ....................................................... 762
- 内核态结构 ....................................................... 778

当线程池阻塞时，线程池会创建额外的线程，而创建、销毁和调度线程的时间与内存资源是非常昂贵的。当开发者看到程序中有线程没有做任何事情时，倾向于创建更多线程，希望新线程能做点什么。构建可扩展且响应良好的应用程序的关键是不阻塞线程，以便它们可以重用来执行其他任务。第 27 章“计算密集异步操作”和第 28 章“I/O 密集异步操作”重点讨论如何使用现有线程执行计算密集操作，以及在 I/O 密集操作时如何使用线程。

在本章中，我关注线程同步。线程同步是为了防止多个线程同时访问共享数据时发生损坏。我强调“同时”，因为线程同步完全取决于时机。如果你有一些数据被两个线程访问，但这两个线程不可能同时接触到数据，那么完全不需要线程同步。在第 28 章中，我讨论了异步函数的片段可能由不同的线程执行。在这里我们可能会有不同的线程访问变量和数据。但异步函数可以实现一种方式，使得两个线程不可能同时访问这些相同数据。因此，当异步函数内部的代码数据时，不需要线程同步。

