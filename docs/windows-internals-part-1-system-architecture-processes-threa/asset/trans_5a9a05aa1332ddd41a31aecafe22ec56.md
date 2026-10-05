

# 10. 找到命令处理器应用并展开其节点。你应该就能在下面的截图中看到标题 Parent（父进程）：

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_30_0.png)

11. 右键点击 Windows 命令处理器并选择“转到详细信息”。

12. 右键点击此 `cmd.exe` 进程并选择“结束进程树”。

13. 在任务管理器确认对话框中点击“结束进程树”。

第一个命令提示符将会出现，但你仍然应该看到画图窗口，因为它是你终止的命令进程的孙进程。由于中间进程（画图程序的父进程）已被终止，父进程和孙进程之间没有联系。

来自 Sysinternals 的 Explorer 显示了比其他任何可用工具更详细的进程和线程信息，这就是为什么你会在书中许多实验中看到它。以下是 Process Explorer 显示提供的一些独特功能：

- 进程安全令牌，例如组和权限列表以及虚拟化存储
- 高亮显示进程、线程和句柄列表中的变更
- 服务托管进程内部的服务列表，包括显示名称和描述
- 额外的进程属性列表，例如缓解策略及其进程保护级别
- 属于作业（job）的进程以及作业详情
- 托管 .NET 应用程序进程以及 .NET 特定细节，如 AppDomains 列表、加载的程序集和 CLR 计数计数
- 托管 Windows Runtime（嵌入式进程）的进程
- 进程和线程的启动时间
- 内存映射文件的完整列表（不仅仅是 DLL）
- 挂起进程或线程的能力
- 杀死单个线程的能力
- 轻松识别在一段时间内哪些进程消耗最多的 CPU

> **注意：** 性能监器可以显示给定进程集的 CPU 利用率，但它不会自动显示性能监控会话后创建的进程。只有二进制输出格式的手动跟踪才能做到这一点。

Process Explorer 还提供了在一个处方便访问信息的功能，例如：

- 进程树，并能够折叠树的部分
- 进程中打开的句柄，包括未命句柄
- 进程中的 DLL（以及内存映射文件）列表
- 进程内的线程活动
- 用户模式和内核模式线程栈，包括使用 Windows 调试工具自带的 Dbghelp.dll 将地址映射到名称
- 使用线程周期计算更准确的 CPU 百比——这是一种精确 CPU 活动的更好的表示方法，正如第 4 章“线程”中所解释的那样
- 完整性级别
- 内存管理器细节，例如峰提交负载以及内核内存分页和非分页池限制（其他工具仅显示当前大小）

接下来是一个使用 Process Explorer 的入门级实验。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_31_0.png)

## 实验：使用 Process Explorer 查看进程详情

从 Sysinternals 下载最新版本的 Process Explorer 并运行它。你可以使用标准用户权限运行它。或者，右键点击可执行文件并选择“以管理员身份运行”以以管理员权限运行。以管理员权限运行会使 Process Explorer 安装一个提供更多功能的驱动程序。无论你如何启动 Process Explorer，以下描述都适用。

当你第一次运行 Process Explorer 时，应该配置符号（symbols）。如果你不这样做，当你双击进程并点击“线程（Threads）”选项卡时，将收到一条“当前未配置符号”的消息提示。如果配置妥当，Process Explorer 可以访问符号信息以显示线程启动函数的符号名称以及线程调用栈上的函数。这对于识别进程内线程正在做什么非常有用。要访问符号，你必须安装了 Windows 调试工具（在本章稍后部分描述）。然后点击“选项（Options）”，配置“符号（Symbols）”，并填写调试工具文件夹中 `Dbghelp.dll` 的路径以及有效的符号路径。例如，在 64 位系统上，如果 Windows 调试工具安装在 WDK 的默认位置，则该配置是正确的。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_32_0.png)

在上述的示例中，使用了按需符号服务器来访问符号，符号文件的副本被安装在本地机器的 `C:\symbols` 文件夹中（如果你有可用空间，可以将此文件夹替换为其他文件夹，例如另一个驱动器）。有关配置使用符号服务器的更多信息，请参阅 https://msdn.microsoft.com/en-us/library/windows/desktop/ee165fd8.aspx。

> **提示：** 你可以通过设置名为 `_NT_SYMBOL_PATH` 的环境变量为图形所示的值来配置 Microsoft 符号服务器。各种工具会自动使用此变量，例如 Process Explorer、Windows 调试工具包含的调试器、Visual Studio 等。这将帮助你避免为每个工具都单独配置。

当 Process Explorer 启动时，它默认显示进程树。你可以展开下窗格以显示打开的句柄或映射的 DLL 和内存映射文件（这些内容将在第 5 章“内存管理”和第二部分的第 8 章中探讨）。它还显示进程命令行和路径的工具提示，当将鼠标悬停在进程名称上时，该提示变得可见。对于某些类型的进程，工具提示还会显示额外信息，包括：

- 服务托管进程内部的服务（例如 `svchost.exe`）
- 任务托管进程内部的任务（例如 `TaskHost.exe`）
- cmd 托管进程的目标（也称为默认代理）
- 在 `dllhost.exe` 进程内托管时的类信息
- Windows 仪表程序程序 (WMI) 托管进程，如 `WmiPrSE.exe`（在本章的“Windows 运行时”部分中简要讨论）

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_33_0.png)

| Name | PID | CPU | Start Time | Private Bytes | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| services | 510 | 0 | 00:01 13:17:18-09 | 7,248 | 12,956 & Services Controller |
| svchost.exe | 512 | 0 | 00:01 13:17:18-06 | 4,488 | 54,485 & Service |
| svchost.exe | 514 | 0 | 00:01 13:14:05-09 | 38,100 | 83,290 & Shell |
| svchost.exe | 516 | 0 | 00:01 13:14:05-16 | 2,936 | 3,192 & LocalService |
| svchost.exe | 518 | 0 | 00:01 13:53:02-16 | 5,568 | 1,312 & RWorker |
| svchost.exe | 520 | 0 | 00:01 13:53:02-16 | 3,192 | 10,240 & LocalService |
| svchost.exe | 522 | 0 | 00:01 13:53:02-16 | 3,065 | 3,065 & LocalService |
| svchost.exe | 524 | 0 | 00:01 13:53:02-16 | 11,184 | 11,764 & LocalService |
| svchost.exe | 526 | 0 | 00:01 13:53:02-16 | 10,950 | 91,628 & LocalService |
| svchost.exe | 528 | 0 | 00:01 13:53:02-16 | 10,000 | 116,100 & LocalService |
| svchost.exe | 530 | 0 | 00:01 13:53:02-16 | 10,000 | 37,768 & Windows Manager |
| svchost.exe | 532 | 0 | 00:01 14:52:09-09 | 21,936 | 34,024 & Service Tool |
| svchost.exe | 534 | 0 | 00:01 13:21:03-16 | 13,024 | 25,424 & Service Subsystem |
| svchost.exe | 536 | 0 | 00:01 13:21:03-16 | 13,024 | 13,608 & Runtime (UI) Shell Controller |
| svchost.exe | 538 | 0 | 00:01 15:56:04-16 | 6,456 | 23,998 & LocalService Host |
| svchost.exe | 540 | 0 | 00:01 13:53:02-16 | 13,024 | 23,996 & Host for Windows Services |
| svchost.exe | 542 | 0 | 00:01 13:53:02-16 | 226,754 | 264,620 & Host for Windows Services |
| svchost.exe | 544 | 0 | 00:01 13:53:02-16 | 226,108 | 344,000 & Host for Windows Services |
| svchost.exe | 546 | 0 | 00:01 13:53:02-16 | 10,972 | 10,972 & Host for Windows Services |
| svchost.exe | 548 | 0 | 00:01 13:53:02-16 | 10,972 | 10,972 & Host for Windows Services |
| svchost.exe | 550 | 0 | 00:01 13:53:02-16 | 3,298 | 3,298 & Host for Windows Services |
| svchost.exe | 552 | 0 | 00:01 13:53:02-16 | 20,452 | 36,296 & Host for Windows Services |
| svchost.exe | 554 | 0 | 00:01 13:53:02-16 | 4,508 | 11,548 & Host for Windows Services |
| svchost.exe | 556 | 0 | 00:01 13:53:02-16 | 7,876 | 7,876 & Host for Windows Services |
| svchost.exe | 558 | 0 | 00:01 13:53:02-16 | 21,528 | 21,528 & Host for Windows Services |
| svchost.exe | 560 | 0 | 00:01 13:53:02-16 | 17,768 | 38,244 & Host for Windows Services |

