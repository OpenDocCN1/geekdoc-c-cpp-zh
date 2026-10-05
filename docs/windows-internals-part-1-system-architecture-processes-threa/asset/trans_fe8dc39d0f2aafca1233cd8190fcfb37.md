

# I/O 类型

应用程序对其发出的 I/O 请求有多种选项。此外，I/O 管理器为驱动程序提供了实现快捷 I/O 接口的选择，这通常可以减少用于 I/O 处理的 IRP 分配。在本节中，我们将解释这些 I/O 请求的选项。

# 同步和异步 I/O

应用程序发出的大多数 I/O 操作都是同步的（这是默认值）。这意味着，应用程序线程会等待设备执行数据操作，并在 I/O 完成时返回状态码。然后，程序可以继续执行并立即访问传输的数据。当以简单形式使用时，Windows 的 ReadFile 和 WriteFile 函数是以同步方式执行的。它们在将控制权返回给调用者之前完成 I/O 操作。

> 异步 I/O 允许应用程序发出多个 I/O 请求，并在设备执行 I/O 操作时继续执行。这种类型的 I/O 可以提高应用程序的吞吐量，因为它允许应用程序继续进行其他工作。要使用异步 I/O，在使用 Windows CreateFile 或 CreateFile2 函数时必须指定 `FILE_FLAG_OVERLAPPED` 标志。当然，在发出异步 I/O 操作后，线程必须小心在设备驱动程序完成数据操作之前访问 I/O 操作的任何数据。线程必须通过监控同步对象的句柄（无论是事件、I/O 完成端口还是文件对象本身，该句柄会在 I/O 完成时发出信号），将其执行情况与 I/O 请求的完成同步。

无论 I/O 请求的类型如何，发送给驱动程序的 I/O 操作都是异步行为的。这意味着，一旦启动了 I/O 请求，设备驱动程序必须尽快返回 I/O 系统。I/O 是否立即返回取决于句柄是以同步还是异步 I/O 打开的。图 6-3 描述了启动读操作时的控制流。请注意，如果存在等待（取决于文件对象中的重叠标志），它是由 `NtReadFile` 在内核模式下完成的。

你可以使用 Windows `OverlappedIoCompletion` 宏测试挂挂的异步 I/O 操作状态，或使用 `GetOverlappedResult(Ex)` 函数获取更多细节。如果你正在使用 I/O 完成端口（在本章稍后的章节“I/O 完成端口”中描述），可以使用 `GetQueuedCompletionStatus(Ex)` 函数。

# 快速 I/O

快速 I/O 是一种特殊机制，允许 I/O 系统跳过 IRP 的生成，直接进入驱动堆栈来完成 I/O 请求。此机制用于优化某些 I/O 路径，这些路径在使用 IRP 时速度较慢。快速 I/O 在第二部分的第 13 章和第 14 章中有详细描述。驱动程序通过在其驱动对象中输入一个指向 `PFAST_IO_DISPATCH` 指针的结构体来注册其快速 I/O 入口。

# 实验：查看驱动注册的 I/O 例程

`ldobj` 内核调试器命令可以列出驱动程序在其驱动对象中注册的快速 I/O 例程。通常，只有文件系统驱动程序需要 I/O 例程——尽管存在例外，例如网络协议驱动程序和总线过滤器。输出显示了 NTFS 文件系统程序的快速 I/O 表：

```
lkd> dr0 \filesystemntfs 2
Driver object (fffc404b2bf8f10) is for:
\FileSystemNTFS
DriverEntry:       ffff80e5663a030
DriverStartIo:    00000000
DriverUnload:     00000000
AddDevice:        00000000
```

调度例程：

- 快速 I/O 例程:
- FastIOCheckIfPossible fffff80e565d670
- NTFSFastIOCheckIfPossible fffff80e56526430
- FastIORead fffff80e56523310
- FastIOWrite fffff80e56523140
- FastIOQueryBasicInfo fffff80e565342d0
- NTFSFastIOQueryBasicInfo fffff80e5651e610
- FastIOLock fffff80e5651e3c0
- FastIOUnlockSingle fffff80e5653d9e0
- FastIOUnlockALL fffff80e5653dc0
- NTFSFastUnlockAll fffff80e5644f9d0
- ReleaseFileForCreate fffff80e56537750
- FastIOQueryNetwork fffff80e5653a220
- AcquireForMode fffff80e56543ec0
- NTFSquireForMode fffff80e5651e950
- MdRead fffff80d2dc6d844
- fs!RtWriteDev fffff80e5654a10
- PrepareMdlWrite
- MdlWriteComplete fffff80d2dc76e48
- fs!RtWriteComplete
- FastIOQueryOpen fffff80e5653a520
- NTFSInfsOpenCamera
- ReleaseForMode fffff80e5644ca60
- AcquireForCcFlush
- NTFSInfsAcquireFileCcFlush
- ReleaseForCcFlush fffff80e56450cf0
- NTFSInfsReleaseFileCcFlush
- NTFS!DriverEntry
- NTFS!FastCopyRead
- NTFS!FastCopyWrite
- NTFS!FastIOQueryStdInfo
- NTFS!FastIOLock
- NTFS!IOUnlockSingle
- NTFS!FastUnlockAll
- NTFS!ReleaseForCreate
- NTFS!FastIOQueryNetwork
- NTFS!MdlRead
- NTFS!PrepareMdlWrite

```

输出显示 NTFS 已已将其 `CopyRead` 例程注册为 I/O 表的 `FastIoRead`。正如此快速 I/O 入口的名称所示，如果文件被缓存，I/O 管理器在发布读 I/O 时调用此函数。如果调用失败，则选择标准的 IRP 路径。

# 映射文件 I/O 和文件缓存

映射文件 I/O 是 I/O 系统的一项重要功能——由 I/O 系统和内存管理器共同产生。（有关映射文件如何实现的细节，请参阅第 5 章）。M-file I/O 指的是将磁盘上的文件视为进程虚拟内存一部分的能力。Mapped-file I/O 允许以内存方式访问磁盘上的文件。如果 I/O 是在内存中的，内存管理器将通过分页机制来处理映射文件 I/O。映射文件 I/O 允许通过 `CreateFile`、`MapViewOfFile` 等函数在内存中进行。映射文件 I/O 允许 I/O 系统跳过 IRP 的生成，直接进入驱动堆栈来完成 I/O 请求。此机制用于优化某些 I/O 路径，这些路径在使用 IRP 时速度较慢。快速 I/O 在第二部分的第 13 章和第 14 章中有详细描述。驱动程序通过在其驱动对象中输入一个指向 `PFAST_IO_DISPATCH` 指针的结构体来注册其快速 I/O 入口。

# 散聚集 I/O (Scatter/gather I/O)

Windows 支持一种特殊的高性能 I/O，称为散聚集，通过 `ReadScatter` 和 `WriteGather` 函数可用。这些函数允许应用程序从多个缓冲区读取磁盘上的一个连续区域，而不是为每个缓冲区发送单独 I/O。要使用散聚集 I/O，文件必须以异步 I/O 打开，用户缓冲区必须是页对齐。此外，如果 I/O 指向质存储设备，I/O 必须在扇区边界上对齐。

# I/O 请求包 (IRP)

I/O 请求包 (IRP) 是存储 I/O 请求信息的地方。当线程调用 API 时，I/O 管理器构造一个 IRP 以表示其在 I/O 系统中的进度。如果可能，I/O 管理器从每个处理器的非分页侧边列表中分配 IRP：

- 小型 IRP 侧边列表存储具有一个栈位置的 IRP（栈位置将在后文描述）。
- 中型 IRP 侧边列表包含四个栈位置的 IRP（适用于需要两个或三个的 IRP）。
- 大型 IRP 侧边列表包含超过四个栈位置的 IRP。

这些列表也有全局侧边列表的支持，允许高效的跨 CPU 流。如果 IRP 需要的栈位置超过大型 IRP 侧边列表包含的数量，I/O 管理器将从非分页池分配 IRP。I/O 管理器使用 `IoAllocateIrp` 函数分配 IRP，该函数也供驱动程序开发者使用，因为在某些情况下驱动程序可能通过创建和初始化自己的 IRP 来直接初始化 I/O 请求。在分配并初始化 IRP 后，I/O 管理器会将调用文件对象的指针存储在 IRP 中。

> 注意 如果定义了，HKLM\System\ControlSet\SessionManager\O System 键中的 DWORD注册表值 `LargeIrpStackLocations` 指定了存储在大型 IRP 侧边列表中的 IRP 包含的栈位置。同样，相同键中的 `MediumIrpStackLocations` 可用于更改中型 IRP 侧边列表中栈位置的大小。

6-11 显示了 IRP 结构的一些重要成员。它始终伴随着一个或多个 `IO_STACK_LOCATION` 对象（在下一节描述）。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_530_0.png)

