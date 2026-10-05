

[19] IRP_MJ_QUERY_QUOTA fffff80e565275f0 ntoskr!NfsFsdDispatchWait
[1a] IRP_MJ_SET_QUOTA fffff80e565275f0 ntoskr!NfsFsdDispatchWait
[1b] IRP_MJ_PNP fffff80e56566230 ntoskr!NfsFsdPnp

快速 I/O 例程序：
...

在激活状态下，每个 IRP 通常位于与请求 I/O 的线程相关的 IRP 列表中（否则，在执行与线程无关的 I/O 时，它将被存储在文件对象中，这在本文章的“线程无关的 I/O”节中有所描述）。这使得 I/O 系统能够在线程因带有未完成的 I/O 请求而终止时，找到并取消任何待处理的 IRP。此外，分页 I/O IRP 也与缺页线程相关联（尽管它们是不可取消的）。这允许 Windows 使用线程无关的 I/O 优化——当当前线程是发起线程时，不使用异步过程调用（APC）来完成 I/O。这些页错误会在内联发生，不需要 APC 递送。

## 实验：查看线程的待处理 IRP

`thread` 命令打印与该线程相关的所有 IRP。如果需要，`!process` 命令可以很好地做到这一点。使用本地实时调试运行内核调试器，并列出 explorer 进程的线程：

```
kd> process 0 7 explorer.exe
PROCESS fffffc04b63c7370
SessionId: 1 Cid: 0b0 Peb: 0ccb000 ParentId: 103
DiBase:8895f000 ObjectTable:ffff689011b71c0 HandleCount:<Data Not Accessible:
Image: explorer.exe
nVadRoot fffffc04b6c2b980 Vads 569 Clone 0 Private 7260. Modified 36527. Loaded. 784.
DeviceMap fffffc688fd7a5d30
```

Token fffff689000024920
18:48:28.375
UserTime 00:00:17.500
KernelTime 00:00:13.484
...

MemoryPriority BACKGROUND
BasePriority 8
CommitCharge 10789
Job Cid 0cb0.10b4 fffffc04b6075060

```
THREAD fffffc04b673a080 Cid 103c.15a8 Teb: 0000000000cbc000 Win32Thread:
ffffc04b66e709a0 WAIT: (UserRequest) UserMode Non-Alertable
ffffc04b66706740 SynchronizationEvent
Not impersonating
...
```

```
THREAD fffffc04b631c7c0 Cid 153c.15a8 Teb: 00000000006a3000 Win32Thread:
ffffc04b6a83a917 WAIT: (UserRequest) UserMode Non-Alertable
```

518 第 6 章 I/O 系统

## SynchronizationEvent
同步事件

IRP 列表：
ffffc04b69ad920: (0006,02c8) Flags: 00060800 Mdl: 00000000

你可能会看到许多线程，其中大多数线程在线程信息的 IRP 列表中都报告了 IRP（调试器仅对具有超过 17 个待处理 I/O 请求的线程显示前 17 个 IRP）。选择一个 IRP 并使用 `!irp` 命令对其检查：

```
lkd!irp fffffc04b69ad920
IRP is active with 2 stacks 1 is current = 0xffffc404b69ad9f0
No Mdl: No System Buffer: Thread fffffc04b13c3c7c0: Irp stack trace.
cmd lg Device File Completion-Next
[_IRP_FILE_SYSTEM_CONTROL(d, N/O)]

5 el fffff04b253c90 pending fffffc04b568b5620 ffffff8e00s572ed0-ffffc404b63c0e00
Success Error Code pending

\\FileSystem\Nps
Args: FLTMGR!FltPassThroughCompletion 000000000 00110008 00000000

[IRP_FILE_SYSTEM_CONTROL(d, N/O)]
5 0ffffc04b3cdca000 fffffc04b568b5620 00000000-00000000
\FileSystem\FltMgr
Args: 00000000 00000000 00110008 000000000

该 IRP 有两个位置，并目标指向命名管道系统 (NPFS) 驱动程序拥有的设备。（NPFS 在第 2 部分第 10 节“网络”中描述)。

## IRP 流程

IRP 通常由 I/O 管理器创建，然后发送到目标设备节点上的第一个设备。图 6-13 显示了基于硬件的设备驱动典型 IRP 流程。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_535_0.png)

图 6-13 IRP 流程

I/O 管理器是创建 IRP 的唯一实体。即插拔管理器和管理器也负责创建具有功能代码 IRP_MJ_PNP 和 IRP_MJ_ 的 IRP。

图 6-13 显示了一个带有六层设备的设备节点：两个过滤器、FDO 和 PDO。这意味着该设备被创建了 I/O 堆栈位置——每个层一个。IRP 始终被递送给最高层设备，即使打开的是堆栈中较低的命名设备。

接收 IRP 的驱动程序可以执行以下操作之一：

-   直接并调用 `IoCompleteRequest` 完成 IRP。这可能是因为 IRP 具有无效参数（例如，缓冲区大小不足或 I/O 代码错误），因为操作很快并可以立即完成，例如从设备获取状态或从注册表中读取值。驱动程序调用 `IoGetIrpStackLocation` 获取其应该引用的堆栈位置指针。

-   在进行某些处理后将 IRP 转发到下一个。例如，上层过滤器可以对操作进行某些记录并将 IRP 向下发送执行。在发送请求之前，驱动程序必须为行中的下一个驱动程序准备下一个 I/O 堆栈位置。如果它不想进行更改，可以使用 `IoSkipIrpStackLocation` 宏，或者可以使用 `IoCopyIrpStackLocationNext` 创建一个副本并进行相应的更改。一旦下一个 I/O 堆栈位置准备就绪，驱动程序调用 `IoCallDriver`。
-   作为扩展，驱动程序还可以通过调用 `IoSetCompletionRoutine` 注册完成。

IRP 流程继续由各种驱动程序在 IRP 向堆栈向下移动时进行处理。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_536_0.png)

537

## 实验：查看设备堆栈

`!device` 命令显示与设备相关的设备。`!devstack` 命令显示与类相关的设备堆栈。输出高亮了类的条目。该行之上的条目位于上方，之下的条目位于下方。

## 实验：检查 IRP

在此实验中，你将在系统中找到一个 IRP，并确定 IRP 类型、其目标地、发布它的驱动程序以及属于哪个进程。这最好在本地调试时进行，因为 IRP 可能会不稳定。

