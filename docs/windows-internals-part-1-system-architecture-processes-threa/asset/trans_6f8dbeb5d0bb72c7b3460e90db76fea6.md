
虽然这个实验无法提供我们所描述的内部步骤的完整视图，但你将能够看到系统的几个部分运行，特别是预取（prefetch）和 Superfetch、映像文件执行选项和其他兼容性检查，以及映像加载器映射。

我们将查看一个非常简单的可执行文件——Notepad.exe，并从命令提示符窗口（Cmd.exe）启动它。重要的是，我们需要同时查看 Cmd.exe 内部的操作和 Notepad.exe 内部的操作。请记住，所有用户态的工作都是由 `CreateProcessInternal` 完成的，父进程在内核创建新进程对象之前会调用该函数。

为了正确设置，请按照以下步骤操作：

- 1. 在 Process Monitor（进程监视器）中添加两个过滤器：一个针对 Cmd.exe，一个针对 Notepad.exe。这些是你应该包含的唯一进程。确保你没有正在运行这两个进程的实例，这样你就能知道看到的是正确的事件。过滤器窗口看起来应该是这样的：

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_166_0.png)

- 2. 确保已禁用事件日志（打开 File 并选择 Capture Events），然后启动命令提示符。

- 3. 启用日志（打开 File 菜单并点击工具栏上的放大镜图标），输入 Notepad 并按回车。在典型的 Windows 系统上，你应该能看到有 500 到 3,500 个事件出现。

- 4. 停止捕获并隐藏 Sequence（序列）和 Time（时间）列，这样你就可以将注意力集中感兴趣的列上。你的窗口看起来应该与截图所示类似。

正如 CreateProcess 流程第 1 阶段所述，首先注意到的事情之一是，在进程启动和第一个线程创建之前，Cmd.exe 对 `HKLM\Microsoft\Windows NT\CurrentVersion\Image Execution Options\Notepad.exe` 进行了注册表查询。由于没有与 Notepad.exe 关联映像执行选项，该进程被创建为：

# Process Monitor - Sysinternals.www.sysinternals.com

File Edit Event Tools Options Help

| Process Name | Location | Path |
| --- | --- | --- |
| zcmd.exe | 14524 | CreateFile | C:\Users\pavei\* |
| zcmd.exe | 14524 | QueryDirectory | C:\Users\pavei\* |
| zcmd.exe | 14524 | QueryDirectory | C:\Program Files (x86)\Common Files\Microsoft Online Service\* |
| zcmd.exe | 14524 | CreateFile | C:\Program Files (x86)\Common Files\Microsoft Online Service\* |
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32\* |
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32\* |
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32.COM |
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32.EXE |
| zcmd.exe | 14524 | CreateFile | C:\Users\pavei\* |
| zcmd.exe | 14524 | RegOpenKey | HKLM\SOFTWARE\WINDOWS\NT\CURRENTUSER\* |
| zcmd.exe | 14524 | RegQueryKeyInformation | HKLM\SOFTWARE\Microsoft\Agent\Process\notepadepad.exe |
| zcmd.exe | 14524 | RegSetValue | C:\WINDOWS\system32\notepad.exe |
| zcmd.exe | 14524 | CreateProcess | |
| zcmd.exe | 14524 | TerminateProcess | |

显示 233,905 个事件中的 3,428 个 (1.4%) 虚拟内存

与 Process Monitor 中的另一个事件一样，你可以通过查看事件堆栈（stack）来判断进程创建流程的每个部分是在用户态还是内核态执行的，以及通过什么路径执行。要做到这一点，双击 RegOpenKey 事件并切换到 Stack 选项卡。下面的截图显示了 64 位 Windows 10 机器上的堆栈：

# Event Properties

| Frame | Module | Location | Address | Path |
| --- | --- | --- | --- | --- |
| K 0 | ntdll.dll | | 0x77ff000084f08640 | C:\WINDOWS\system32\ntdll.dll |
| K 1 | kernel32.dll | | 0x77ff000042f04238 | C:\WINDOWS\system32\kernel32.dll |
| K 2 | ntdll.dll | OpenaseKey = +0x17 | 0x77ff000031f0316 | C:\WINDOWS\system32\ntdll.dll |
| K 3 | kernel32.dll | NtCreateKey = +0x1ec | 0x77ff000031f037c | C:\WINDOWS\system32\kernel32.dll |
| K 4 | ntdll.dll | NtOpenKey = +0x2a6 | 0x77ff000031f03ae | C:\WINDOWS\system32\ntdll.dll |
| K 5 | ntdll.dll | | 0x77ff000031f0394 | C:\WINDOWS\system32\ntdll.dll |
| K 6 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| K 7 | ntdll.dll | ServiceLink | 0x77ff000031f0360 | C:\WINDOWS\system32\ntdll.dll |
| K 8 | ntdll.dll | RegSetValue = +0x41 | 0x77ff000031f03a6 | C:\WINDOWS\system32\ntdll.dll |
| K 9 | ntdll.dll | NtCloseFile = +0x4e | 0x77ff000031f03b1 | C:\WINDOWS\system32\ntdll.dll |
| K 10 | ntdll.dll | NtCreateFile = +0x1c | 0x77ff000031f03de | C:\WINDOWS\system32\ntdll.dll |
| K 11 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| U 12 | rtdll.dll | | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |
| U 13 | kernel32.dll | CreateFile = +0x217 | 0x77ff000031f03c6 | C:\WINDOWS\system32\kernel32.dll |
| U 14 | kernel32.dll | CreateProcess = +0x22 | 0x77ff000031f03e8 | C:\WINDOWS\system32\kernel32.dll |
| U 15 | kernel32.dll | CreateProcessW = +0x53 | 0x77ff000031f03d5 | C:\WINDOWS\system32\kernel32.dll |
| U 16 | ntdll.dll | | 0x77ff000031f035c | C:\WINDOWS\system32\ntdll.dll |
| U 17 | ntdll.dll | | 0x77ff000031f05b4 | C:\WINDOWS\system32\ntdll.dll |
| U 18 | ntdll.dll | WorkItemThread = +0x36d | 0x77ff000031f0d6d | C:\WINDOWS\system32\ntdll.dll |
| U 19 | ntdll.dll | DispatchPath = +0x95 | 0x77ff000031f0af45 | C:\WINDOWS\system32\ntdll.dll |
| U 20 | ntdll.dll | CreatePath = +0x95 | 0x77ff003b031f094 | C:\WINDOWS\system32\ntdll.dll |
| U 21 | ntdll.dll | | 0x77ff000031f03c | C:\WINDOWS\system32\ntdll.dll |
| U 22 | kernel32.dll | BaseThreadThread = +0x2d | 0x77ff006b8102 | C CWINDOWS\system32kernel32.dll |
| U 23 | rtdll.dll | UserThreadStart = +0x34 | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |

# Event Properties

| Frame | Module | Location | Address | Path |
| --- | --- | --- | --- | --- |
| K 0 | ntdll.dll | | 0x77ff000084f08640 | C:\WINDOWS\system32\ntdll.dll |
| K 1 | kernel32.dll | | 0x77ff000042f04238 | C:\WINDOWS\system32\kernel32.dll |
| K 2 | ntdll.dll | OpenaseKey = +0x17 | 0x77ff000031f0316 | C:\WINDOWS\system32\ntdll.dll |
| K 3 | kernel32.dll | NtCreateKey = +0x1ec | 0x77ff000031f037c | C:\WINDOWS\system32\kernel32.dll |
| K 4 | ntdll.dll | NtOpenKey = +0x2a6 | 0x77ff000031f03ae | C:\WINDOWS\system32\ntdll.dll |
| K 5 | ntdll.dll | | 0x77ff000031f0394 | C:\WINDOWS\system32\ntdll.dll |
| K 6 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| K 7 | ntdll.dll | ServiceLink | 0x77ff000031f0360 | C:\WINDOWS\system32\ntdll.dll |
| K 8 | ntdll.dll | RegSetValue = +0x41 | 0x77ff000031f03a6 | C:\WINDOWS\system32\ntdll.dll |
| K 9 | ntdll.dll | NtCloseFile = +0x4e | 0x77ff000031f03b1 | C:\WINDOWS\system32\ntdll.dll |
| K 10 | ntdll.dll | NtCreateFile = +0x1c | 0x77ff000031f03de | C:\WINDOWS\system32\ntdll.dll |
| K 11 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| U 12 | rtdll.dll | | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |
| U 13 | kernel32.dll | CreateFile = +0x217 | 0x77ff000031f03c6 | C:\WINDOWS\system32\kernel32.dll |
| U 14 | kernel32.dll | CreateProcess = +0x22 | 0x77ff000031f03e8 | C:\WINDOWS\system32\kernel32.dll |
| U 15 | kernel32.dll | CreateProcessW = +0x53 | 0x77ff000031f03d5 | C:\WINDOWS\system32\kernel32.dll |
| U 16 | ntdll.dll | | 0x77ff000031f035c | C:\WINDOWS\system32\ntdll.dll |
| U 17 | ntdll.dll | | 0x77ff000031f05b4 | C:\WINDOWS\system32\ntdll.dll |
| U 18 | ntdll.dll | WorkItemThread = +0x36d | 0x77ff000031f0d6d | C:\WINDOWS\system32\ntdll.dll |
| U 19 | ntdll.dll | DispatchPath = +0x95 | 0x77ff000031f0af45 | C:\WINDOWS\system32\ntdll.dll |
| U 20 | ntdll.dll | CreatePath = +0x95 | 0x77ff003b031f094 | C:\WINDOWS\system32\ntdll.dll |
| U 21 | ntdll.dll | | 0x77ff000031f03c | C:\WINDOWS\system32\ntdll.dll |
| U 22 | kernel32.dll | BaseThreadThread = +0x2d | 0x77ff006b8102 | C CWINDOWS\system32kernel32.dll |
| U 23 | rtdll.dll | UserThreadStart = +0x34 | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |

# Event Properties

| Frame | Module | Location | Address | Path |
| --- | --- | --- | --- | --- |
| K 0 | ntdll.dll | | 0x77ff000084f08640 | C:\WINDOWS\system32\ntdll.dll |
| K 1 | kernel32.dll | | 0x77ff000042f04238 | C:\WINDOWS\system32\kernel32.dll |
| K 2 | ntdll.dll | OpenaseKey = +0x17 | 0x77ff000031f0316 | C:\WINDOWS\system32\ntdll.dll |
| K 3 | kernel32.dll | NtCreateKey = +0x1ec | 0x77ff000031f037c | C:\WINDOWS\system32\kernel32.dll |
| K 4 | ntdll.dll | NtOpenKey = +0x2a6 | 0x77ff000031f03ae | C:\WINDOWS\system32\ntdll.dll |
| K 5 | ntdll.dll | | 0x77ff000031f0394 | C:\WINDOWS\system32\ntdll.dll |
| K 6 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| K 7 | ntdll.dll | ServiceLink | 0x77ff000031f0360 | C:\WINDOWS\system32\ntdll.dll |
| K 8 | ntdll.dll | RegSetValue = +0x41 | 0x77ff000031f03a6 | C:\WINDOWS\system32\ntdll.dll |
| K 9 | ntdll.dll | NtCloseFile = +0x4e | 0x77ff000031f03b1 | C:\WINDOWS\system32\ntdll.dll |
| K 10 | ntdll.dll | NtCreateFile = +0x1c | 0x77ff000031f03de | C:\WINDOWS\system32\ntdll.dll |
| K 11 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| U 12 | rtdll.dll | | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |
| U 13 | kernel32.dll | CreateFile = +0x217 | 0x77ff000031f03c6 | C:\WINDOWS\system32\kernel32.dll |
| U 14 | kernel32.dll | CreateProcess = +0x22 | 0x77ff000031f03e8 | C:\WINDOWS\system32\kernel32.dll |
| U 15 | kernel32.dll | CreateProcessW = +0x53 | 0x77ff000031f03d5 | C:\WINDOWS\system32\kernel32.dll |
| U 16 | ntdll.dll | | 0x77ff000031f035c | C:\WINDOWS\system32\ntdll.dll |
| U 17 | ntdll.dll | | 0x77ff000031f05b4 | C:\WINDOWS\system32\ntdll.dll |
| U 18 | ntdll.dll | WorkItemThread = +0x36d | 0x77ff000031f0d6d | C:\WINDOWS\system32\ntdll.dll |
| U 19 | ntdll.dll | DispatchPath = +0x95 | 0x77ff000031f0af45 | C:\WINDOWS\system32\ntdll.dll |
| U 20 | ntdll.dll | CreatePath = +0x95 | 0x77ff003b031f094 | C:\WINDOWS\system32\ntdll.dll |
| U 21 | ntdll.dll | | 0x77ff000031f03c | C:\WINDOWS\system32\ntdll.dll |
| U 22 | kernel32.dll | BaseThreadThread = +0x2d | 0x77ff006b8102 | C CWINDOWS\system32kernel32.dll |
| U 23 | rtdll.dll | UserThreadStart = +0x34 | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |

# Event Properties

| Frame | Module | Location | Address | Path |
| --- | --- | --- | --- | --- |
| K 0 | ntdll.dll | | 0x77ff000084f08640 | C:\WINDOWS\system32\ntdll.dll |
| K 1 | kernel32.dll | | 0x77ff000042f04238 | C:\WINDOWS\system32\kernel32.dll |
| K 2 | ntdll.dll | OpenaseKey = +0x17 | 0x77ff000031f0316 | C:\WINDOWS\system32\ntdll.dll |
| K 3 | kernel32.dll | NtCreateKey = +0x1ec | 0x77ff000031f037c | C:\WINDOWS\system32\kernel32.dll |
| K 4 | ntdll.dll | NtOpenKey = +0x2a6 | 0x77ff000031f03ae | C:\WINDOWS\system32\ntdll.dll |
| K 5 | ntdll.dll | | 0x77ff000031f0394 | C:\WINDOWS\system32\ntdll.dll |
| K 6 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| K 7 | ntdll.dll | ServiceLink | 0x77ff000031f0360 | C:\WINDOWS\system32\ntdll.dll |
| K 8 | ntdll.dll | RegSetValue = +0x41 | 0x77ff000031f03a6 | C:\WINDOWS\system32\ntdll.dll |
| K 9 | ntdll.dll | NtCloseFile = +0x4e | 0x77ff000031f03b1 | C:\WINDOWS\system32\ntdll.dll |
| K 10 | ntdll.dll | NtCreateFile = +0x1c | 0x77ff000031f03de | C:\WINDOWS\system32\ntdll.dll |
| K 11 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll |
| U 12 | rtdll.dll | | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |
| U 13 | kernel32.dll | CreateFile = +0x217 | 0x77ff000031f03c6 | C:\WINDOWS\system32\kernel32.dll |
| U 14 | kernel32.dll | CreateProcess = +0x22 | 0x77ff000031f03e8 | C:\WINDOWS\system32\kernel32.dll |
| U 15 | kernel32.dll | CreateProcessW = +0x53 | 0x77ff000031f03d5 | C:\WINDOWS\system32\kernel32.dll |
| U 16 | ntdll.dll | | 0x77ff000031f035c | C:\WINDOWS\system32\ntdll.dll |
| U 17 | ntdll.dll | | 0x77ff000031f05b4 | C:\WINDOWS\system32\ntdll.dll |
| U 18 | ntdll.dll | WorkItemThread = +0x36d | 0x77ff000031f0d6d | C:\WINDOWS\system32\ntdll.dll |
| U 19 | ntdll.dll | DispatchPath = +0x95 | 0x77ff000031f0af45 | C:\WINDOWS\system32\ntdll.dll |
| U 20 | ntdll.dll | CreatePath = +0x95 | 0x77ff003b031f094 | C:\WINDOWS\system32\ntdll.dll |
| U 21 | ntdll.dll | | 0x77ff000031f03c | C:\WINDOWS\system32\ntdll.dll |
| U 22 | kernel32.dll | BaseThreadThread = +0x2d | 0x77ff006b8102 | C CWINDOWS\system32kernel32.dll |
| U 23 | rtdll.dll | UserThreadStart = +0x34 | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll |

CHAPTER 3 Processes and jobs 151

与 Process Monitor 中的另一个事件一样，你可以通过查看事件堆栈（stack）来判断进程创建流程的每个部分是在用户态还是内核态执行的，以及通过什么路径执行。要做到这一点，双击 RegOpenKey 事件并切换到 Stack 选项卡。下面的截图显示了 64 位 Windows 10 机器上的堆栈：

此堆栈显示你已经到达在内核态执行的进程创建部分（通过 `NtCreateUserProcess`），并且由 `PspAllocateProcess` 负责此检查。

在查看线程和进程创建后的事件列表中，你会注意到三组事件：

- 对应用程序兼容性标志的简单检查，这会让用户态进程创建代码知道是否需要通过 shim 引擎检查应用程序兼容性数据库。

- 对 SxS（搜索 By-Side-Side）、清单（Manifest）和 MUI/语言键的多次读取，这些是前面提到的程序框架的一部分。

- 对一个或多个 .db 文件的文件 I/O，这些是系统上的应用程序兼容性数据库。此 I/O 是进行检查是否需要调用 shim 引擎的地方。由于 Notepad 是一个良好的微软程序，它不需要任何 shim。

下面的截图显示了后续的一系列事件，这些发生在 Notepad 进程内部。这些是由内核态的用户态线程封装发起的动作，该封装执行了上述操作。前两个是 Notepad.exe 和 Ntdll.dll 映像调试通知消息，这些消息只有在 Notepad 进程上下文中运行并针对该进程上下文时才会生成。
