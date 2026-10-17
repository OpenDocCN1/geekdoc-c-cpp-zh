
+00cc DriverExtension : 0x8a557c8 _

+00d0 DriverName : _UNICODE_STRING "kbdclass"

+00d4 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"

+00d8 FastIo : (null)

+00de DriverInit : 0x30

+00e0 MajorFunction : 7

+00e4 DriverUnload : (null)

+00e8 SectionName : (null)

+00ec SharedData : (null)

+00f0 DeviceType : (null)

+00f4 DeviceType : (null)

+00f8 FileObjectType : (null)

+00fc FileObjectType : (null)

+0100 Type : 4

+0102 Size : 0x168

+0104 DeviceObject : 0x9f509648 _DEVICE_OBJECT

+0108 Flags : 0x412

+01c0 DriverStart : 0xc30000 Void

+0110 DriverSize : 0x000

+0114 DriverSection : 0x8a557c8 _DRIVER_EXTENSION

+0118 DriverExtension : 0x8a557c8 _

+011c DriverName : _UNICODE_STRING "kbdclass"

+0124 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"

+0128 FastIo : (null)

+012c DriverInit : 0x30

+0130 MajorFunction : 7

+0134 DriverUnload : (null)

+0138 SectionName : (null)

+013c SharedData : (null)

+0140 DeviceType : (null)

+0144 DeviceType : (null)

+0148 FileObjectType : (null)

+014c FileObjectType : (null)

+0150 DeviceObject : (null)

+0154 DeviceFlags : 0

+01158 DeviceExtension : (null)

+015bc DriverName : (null)

+0160 DriverStart : 0xc30000 Void

+0164 DriverSize : 0x000

+0168 DriverSection : 0x8a557c8 _DRIVER_EXTENSION

+016cc DriverExtension : 0x8a557c8 _

+0170 DriverName : _UNICODE_STRING "kbdclass"

+0174 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"

+0178 FastIo : (null)

+017c DriverInit : 0x30

+0180 MajorFunction : 7

+0184 DriverUnload : (null)

+0188 SectionName : (null)

+018c SharedData : (null)

+0190 DeviceType : (null)

+0194 DeviceType : (null)

+0198 FileObjectType : (null)

+019c FileObjectType : (null)

+01a0 DeviceObject : (null)

+01a4 DeviceFlags : 0

+01a8 DeviceExtension : (null)

```
分发例程被清晰地显示，将在下一节中讨论。请注意，驱动程序不支持的操作将传递给 I/O 管理器的例程。`!devobj` 命令的地址对应一个 `DRIVER_OBJECT`，而 `!devobj` 命令的地址对应一个 `DEVICE_OBJECT`。你可以直接使用调试器查看这些结构。
```

为了对使用文件对象的驱动代码保持某种程度的透明度，并允许在不扩大文件功能的情况下进行扩展，该结构还包含一个扩展字段，允许最多六种不同的附加属性，见表 6-2。

## 打开设备

文件对象是表示设备句柄的内核态数据结构。文件对象符合对象的标准：它们可以被多个进程共享；它们具有名称；受对象安全保护；并且支持同步。文件对象提供了可以读取或写入的表示。表 6-1 列出了文件对象的属性。

| 属性 | 目的 |
| :--- | :--- |
| 文件名 | 文件对象指向的文件，通过 `CreateFile` 或 `CreateFile2` 传递 |
| 当前字节偏移量 | 它在文件中的位置（仅用于同步 I/O） |
| 共享模式 | 这些指示当当前调用者使用时，其他调用者是否可以读取、写入或删除 |
| 打开模式 | 这些指示 I/O 是同步还是异步、缓存还是非顺序等 |
| 指向设备对象 | 标识文件所在的设备类型 |
| 指向卷块 (VPB) | 标识文件所在的卷或分区（文件系统情况下） |
| 指向节对象指针 | 这是一个描述映射/缓存文件的根结构。该结构还包含缓存映射，标识文件的哪些部分被缓存管理器缓存，以及它们在缓存中的位置 |
| 指向私有缓存映射 | 用于存储此句柄的页缓存信息或进程页优先级。参见第 5 节“内存管理”有关页优先级的信息 |
| I/O 请求包 (IRP) 列表 | 如果是线程 I/O（在本章后面的“线程异步 I/O”部分描述）且文件对象与完成部分相关（在“I/O 完成端口”部分描述），则这是与该文件相关的所有操作列表 |
| I/O 完成上下文 | 这是当前 I/O 完成部分的上下文信息（如果存在） |
| 文件对象扩展 | 存储文件的 I/O 优先级（在本章稍后解释）以及是否对文件对象执行共享访问检查，并包含存储特定上下文的可选文件扩展 |

为了对使用文件对象的驱动代码保持某种程度的透明度，并允许在不扩大文件功能的情况下进行扩展，该结构还包含一个扩展字段，允许最多六种不同的附加属性，见表 6-2。

## 表 6-2 文件扩展名

| 扩展名 | 目的 |
| --- | --- |
| 事务参数 | 包含事务参数块，其中包含事务文件操作的信息。由 `IoGetTransactionBlock` 返回。 |
| 设备对象提示 | 标识此文件应关联的过滤驱动程序的设备对象。通过 `IoCreateFileEx` 或 `IoFileSpecifyDeviceToObject` 设置。 |
| I/O 状态块范围 | 允许将用户缓冲区锁定到内核模式内存中执行异步 I/O。通过 `IoFileIoOverlappedRange` 设置。 |
| 通用 | 包含过滤驱动程序特定的信息，以及调用者创建的扩展创建参数 (ECPs)。通过 `IoCreateFileEx` 设置。 |
| 计划文件 I/O | 存储文件的带宽预留信息，存储系统利用其优化并保证多媒体应用程序的吞吐量。（参见本章稍后的的“带宽预留计划 I/O”节）。通过 `SetFileBandwidthReservation` 设置。 |
| 符号链接 | 在遍历挂载点或目录联接点（或过滤程序显式解析路径）时，添加到文件对象的创建中。它存储了调用者提供的路径，包括任何中间联接点，因此如果遇到相对符号链接，它可以通过联接点回溯。有关 NTFS 符号链接、挂载点和目录的更多信息，请参见第 2 部分第 13 章。 |

当调用者打开文件或设备时，I/O 管理器返回一个指向文件对象的句柄。在此之前，会询问负责该设备的驱动程序的创建分发例程（`IRP_MJ_CREATE`）是否允许打开设备，并且如果请求需要成功，则允许驱动程序执行任何初始化请求。

> 注意：文件对象代表文件的打开实例，而不是文件本身。与使用 inode 的 UNIX 系统不同，Windows 并没有定义文件的表示方式；Windows 文件系统驱动程序定义了自身的表示方式。

为了执行对象，文件受包含访问控制列表 (ACL) 的安全描述符的保护。I/O 管理器查询安全子系统，以确定文件的 ACL 是否允许进程按照请求的方式访问文件。如果允许，对象管理器将授予访问，并将授予的访问与其返回的句柄关联。如果此线程或另一个进程需要执行原始请求中未指定的附加操作，则线程必须使用不同的请求重新打开文件（或使用所需的访问权限复制句柄）以获取另一个句柄，这将触发另一个安全检查。（有关对象保护的更多信息请参见第 7 章）。

## 实验：查看设备句柄

任何拥有设备打开句柄的进程都有与打开实例对应的文件对象。你可以通过 Process Explorer 查看这些句柄：选择一个进程并在“视图”菜单的“下窗视图”子菜单中勾选“句柄”。按“类型”列排序并向下滚动查看表示文件对象的句柄，它们被标记为 File。

## Process Explorer - Sysinternals: www.sysinternals.com/sysinternals/ProcEx.html

| 进程 | CPU | 字节 | 工作集 | PID | 描述 | 公司名称 | 对象地址 | 访问权限 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| \<System>CSHOST_CLIENT.EXE | <0.01 | 17,174 | 3,875 | 602 | 客户端运行时进程 | Microsoft Corporation | | | |
| svchost.exe | <0.01 | 14,316 | 4,538 | 603 | 服务运行时进程 | Microsoft Corporation | | | |
| svchost.exe | 0.00 | 4,664 | 10,718 | 604 | CDM | Microsoft Corporation | | | |
| dwwm.exe | 0.07 | 36,528 | 62,972 | 452 | Windows 管理器 | | | |

在此示例中，桌面窗口管理器 (`dwm.exe`) 进程有一个指向内核服务驱动程序 (`kbd.sys`) 创建的设备的打开句柄。你可以通过首先识别对象的地址，在内核调试器中查看特定的文件对象。以下命令报告了上述截图中高亮句柄（句柄值 `0xD4`）的信息，该句柄位于进程 ID 为 452 的 `dwm.exe` 进程中。

```
1kd> !handle 452
```

```
PROCESS ffffc404b62fb780

SessionID: 1 Cid: 01c4 Peb: b4c3db0000 ParentCid: 0364

DirBase: 7xe6070000 ObjectTable: fffff8fd1dc38c0 HandleCount: <Data Not Accessible>

Image: dwm.exe
```

Handle Error reading count.

```
0348: Object: ffffc404b6406ef0 GrantedAccess: 00100003 (Audit) Entry: fffff8fd396d20

Object: ffffc404b6406ef0 Type: (ffffc404b189bf20) File

ObjectHeader: ffffc404b6406ec0 (new version)

HandleCount: 1 Pointer: 32767
```

因为它是文件对象，你可以使用 `!fileobj` 命令获取它的信息（它也是 Process Explorer 中显示的对象地址）：

```
1kd> !fileobj ffffc404b6406ef0
```

## I/O 处理

在我们已经涵盖了驱动程序的结构、类型以及支持它们的数据结构之后，让我们来看看 I/O 请求如何在系统中流转。I/O 请求通过几个可预测的阶段阶段。这些阶段取决于请求目标是单层驱动程序操作的设备，还是通过多层驱动程序到达的设备。处理方式进一步取决于调用者指定的是同步还是异步 I/O，因此我们将从这两种类型开始对 I/O 类型进行讨论，然后讨论其他类型。

## I/O 类型

应用程序对其发出的 I/O 请求有多种选项。此外，I/O 管理器为驱动程序提供了实现快捷 I/O 接口的选择，这通常可以减少用于 I/O 处理的 IRP 分配。在本节中，我们将解释这些 I/O 请求的选项。

## 同步和异步 I/O

应用程序发出的大多数 I/O 操作都是同步的（这是默认值）。这意味着，应用程序线程会等待设备执行数据操作，并在 I/O 完成时返回状态码。然后，程序可以继续执行并立即访问传输的数据。当以简单形式使用时，Windows 的 `ReadFile` 和 `WriteFile` 函数是以同步方式执行的。它们在将控制权返回给调用者之前完成 I/O 操作。

> 异步 I/O 允许应用程序发出多个 I/O 请求，并在设备执行 I/O 操作时继续执行。这种类型的 I/O 可以提高应用程序的吞吐量，因为它允许应用程序继续进行其他工作。要使用异步 I/O，在使用 Windows `CreateFile` 或 `CreateFile2` 函数时必须指定 `FILE_FLAG_OVERLAPPED` 标志。当然，在发出异步 I/O 操作后，线程必须小心在设备驱动程序完成数据操作之前访问 I/O 操作的任何数据。线程必须通过监控同步对象的句柄（无论是事件、I/O 完成端口还是文件对象本身，该句柄会在 I/O 完成时发出信号），将其执行情况与 I/O 请求的完成同步。

无论 I/O 请求的类型如何，发送给驱动程序的 I/O 操作都是异步行为的。这意味着，一旦启动了 I/O 请求，设备驱动程序必须尽快返回 I/O 系统。I/O 是否立即返回取决于句柄是以同步还是异步 I/O 打开的。图 6-3 描述了启动读操作时的控制流。请注意，如果存在等待（取决于文件对象中的重叠标志），它是由 `NtReadFile` 在内核模式下完成的。

你可以使用 Windows `OverlappedIoCompletion` 宏测试挂挂的异步 I/O 操作状态，或使用 `GetOverlappedResult(Ex)` 函数获取更多细节。如果你正在使用 I/O 完成端口（在本章稍后的章节“I/O 完成端口”中描述），可以使用 `GetQueuedCompletionStatus(Ex)` 函数。

## 快速 I/O

快速 I/O 是一种特殊机制，允许 I/O 系统跳过 IRP 的生成，直接进入驱动堆栈来完成 I/O 请求。此机制用于优化某些 I/O 路径，这些路径在使用 IRP 时速度较慢。快速 I/O 在第二部分的第 13 章和第 14 章中有详细描述。驱动程序通过在其驱动对象中输入一个指向 `PFAST_IO_DISPATCH` 指针的结构体来注册其快速 I/O 入口。

## 实验：查看驱动注册的 I/O 例程

`ldobj` 内核调试器命令可以列出驱动程序在其驱动对象中注册的快速 I/O 例程。通常，只有文件系统驱动程序需要 I/O 例程——尽管存在例外，例如网络协议驱动程序和总线过滤器。输出显示了 NTFS 文件系统程序的快速 I/O 表：

```
lkd> dr0 \filesystemntfs 2
```

Driver object (`fffc404b2bf8f10`) is for:

`\FileSystemNTFS`

DriverEntry:       ffff80e5663a030

DriverStartIo:    00000000

DriverUnload:     00000000

AddDevice:        00000000
