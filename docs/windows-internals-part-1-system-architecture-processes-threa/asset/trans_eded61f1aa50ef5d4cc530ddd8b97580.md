

图 6–6 显示了一个设备节点（也称为 devnode），它包含一个创建物理设备对象（PDO）的总线驱动程序、下层过滤器、创建一个功能设备对象（FDO）的功能驱动程序以及上层过滤器。必需层是 PDO 和 FDO。各种过滤器可能存在也可能不存在。

## IRP

| | |
|---|||
| FDO | 上层过滤器驱动 3 |
| FDO | 上层过滤器驱动 2 |
| FDO | 上层过滤器驱动 1 |
| FDO | 功能驱动程序 |
| FDO | 下层过滤器驱动 2 |
| FDO | 下层过滤器驱动 1 |
| PDO | 总线驱动程序 |

**图 6–6** WDM 设备节点 (devnode)。

在 WDM 中，一个驱动程序负责控制设备设备方面。总线驱动程序负责检测总线成员的变化（设备添加或删除），协助 PnP 管理器枚举总线上的设备，访问特定总线的寄存器，并在某些情况下控制总线上设备的电源。功能驱动程序通常是唯一访问设备硬件的驱动程序。这些设备是如何被描述的，详见本章的“即插用管理器”节。

## 分层驱动程序

对单个硬件的支持被分在多个驱动程序中，提供了使设备正常工作所需的部分功能。除了 WDM 总线驱动程序、功能驱动程序和过滤驱动程序外，硬件支持可能被分配在以下组件之间：

- **类驱动程序 (Class drivers)**：它们实现特定类设备（如磁盘、键盘或 CD-ROM）的 I/O 处理，这些设备的硬件接口已经标准化，因此一个驱动程序就可以为来自各种制造商的设备提供服务。

- **微类驱动程序 (Miniclass drivers)**：它们实现针对特定类设备的 I/O 处理。例如，尽管微软有一个标准化的电池类驱动程序，但不间电源 (UPS) 和笔记本电池都具有高度特定的接口，这些接口在制造商之间差异巨大，因此需要供应商提供微类驱动。微类驱动本质上是内核模式 DLL，不直接执行 IRP 处理。相反，类驱动程序调用它们，并从类驱动程序导入函数。

- **端口驱动程序 (Port drivers)**：它们实现对类型 I/O 端口（如 SATA）的 I/O 请求的处理，并作为内核模式函数库而非实际设备驱动程序实现。端口驱动程序由微软编写，因为接口通常是标准化的，以便不同的供应商共享同一个端口驱动程序。然而，在某些情况下，第三方可能为专用硬件编写自己的程序。在某些情况下，I/O 端口也扩展到逻辑端口。例如，网络驱动接口规范 (NDIS) 就是“端口”驱动程序。

- **微端口驱动程序 (Miniport drivers)**：它们将通用的 I/O 请求映射到适配器类型，例如特定的网络适配器。微端口驱动程序是导入端口驱动程序提供的实际设备。微端口驱动程序由第三方编写，为端口驱动程序提供接口。与微类驱动程序一样，它们是内核模式 DLL，不执行 IRP 处理。

图 6-7 是为了说明目的简化示例，有助于演示设备驱动程序在高层的工作原理。你可以看到，文件系统驱动程序接收到一个写入文件特定位置的请求。它通过 I/O 管理器将此请求传递给磁盘驱动程序，在磁盘起始边界写入若干字节。磁盘驱动程序反过来将请求转换为磁盘上的物理位置，并与磁盘通信以写入数据。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_511_0.png)

图 6-7 文件系统驱动程序和驱动程序

此图说明了两个分层驱动程序之间的工作分工。I/O 管理器接收到一个相对于文件起始的写入请求。I/O 管理器将请求传递给文件系统驱动程序，将其从文件偏移量转换为磁盘位置并写入若干字节。文件系统驱动程序调用 I/O 管理器将请求传递给磁盘驱动程序，将其转换为物理位置并传输数据。

由于所有驱动程序——设备驱动程序和文件系统驱动程序——为操作系统提供了相同的框架，另一个驱动程序可以在不更改现有驱动程序的情况下轻松插入。例如，可以将多个磁盘看起来像一个巨大的单一磁盘。此驱动程序位于文件系统和磁盘驱动程序之间，如图 6-8 所示的简化架构图（对于卷管理器，请参见第 12 章“存储管理”）。

## 应用程序 / 服务

在文件的指定偏移处写入数据
- 将文件偏移量转换为卷偏移量并调用下一个驱动程序（通过 I/O 管理器）
- 调用驱动程序在卷偏移量处写入数据
- 将卷偏移量转换为数量和偏移量，并调用下一个驱动程序（通过 I/O 管理器）
- 调用下一个驱动程序在磁盘偏移量处写入数据
- 将磁盘偏移量转换为磁盘上的物理位置并传输数据

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_512_0.png)

**图 6–8** 添加驱动程序。

## 实验：查看加载列表

你可以通过运行对话框执行 `Msinfo32.exe` 查看已注册驱动程序的列表。选择**软件**下的**系统**条目以查看系统配置的驱动程序列表。已加载的“启动”列显示为是，如下所示：

## 系统摘要

| 名称 | 描述 | 路径 | 已启动 | 模式 | 状态 |
|---|---|---|---|---|---|
| Inware | 合规... | c:\windows\system32\drivers\inware.sys | 内核 | 否 | 已停止 |
| Compware | | c:\windows\system32\drivers\compware.sys | 内核 | 否 | 已停止 |
| PreEnv | | c:\windows\system32\drivers\prenv.sys | 内核 | 否 | 已停止 |
| Environment variables | 环境变量 | c:\windows\system32\drivers\envvars.sys | 内核 | 否 | 已停止 |
| acdev | ACPI 设备 | c:\windows\system32\drivers\acdev.sys | 内核 | 否 | 已停止 |
| aspdev | | c:\windows\system32\drivers\aspdev.sys | 内核 | 否 | 已停止 |
| Network Connections | 网络连接 | c:\windows\system32\drivers\netconn.sys | 内核 | 否 | 已停止 |
| Runtime | ACPI 报警驱动程序 | c:\windows\system32\drivers\rtalarm.sys | 内核 | 否 | 已停止 |
| Loaded Modules | 加载的模块 | c:\windows\system32\drivers\loadmod.sys | 内核 | 否 | 已停止 |
| Program Groups | 应用程序处理... | c:\windows\system32\drivers\progrp.sys | 内核 | 是 | 正常 |
| Starting Programs | 启动程序 | c:\windows\system32\drivers\startpr.sys | 内核 | 是 | 正常 |
| Old Registration | 处理器控制器 | c:\windows\system32\drivers\oldreg.sys | 内核 | 否 | 已停止 |
| Windows Error Reporting | Windows 错误报告 | c:\windows\system32\drivers\werfault.sys | 内核 | 否 | 已停止 |
| amndata | | c:\windows\system32\drivers\amndata.sys | 内核 | 否 | 已停止 |
| amndata | | c:\windows\system32\drivers\amndata.sys | 内核 | 否 | 已停止 |

来自 `HKLM\System\CurrentControlSet\Services` 注册表项的驱动程序列表位于驱动程序和服务的之间。它由服务管理器 (SCM) 启动。区分驱动程序和服务的方法是查看 Type 值。小值（1, 2, 4, 8）表示驱动程序，而值 16 (0x10) 和 32 (0x20) 表示 Windows 服务。有关驱动程序的更多信息，请参阅第 2 章。

你也可以通过 Process Explorer 查看内核模式驱动程序列表。运行 Process Explorer，选择 System 进程，并在下视图 View 条目中选择 DLL：

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_513_0.png)

| PID | 映像 | CPU | 内存 | 工作集 | 线程 | 公司名称 | 基地址 |
|---|---|---|---|---|---|---|
| 4 | System | 0.0 | 28448 | 28448 | 4 | Microsoft Corporation | 0x000000000000000 |
| 512 | smss.exe | 0.0 | 800 | 800 | 1 | Microsoft Corporation | 0x000000000000000 |
| 640 | services.exe | 0.0 | 12400 | 12400 | 3 | Microsoft Corporation | 0x000000000000000 |
| 1244 | explorer.exe | 0.0 | 15120 | 15120 | 12 | Microsoft Corporation | 0x000000000000000 |
| 2500 | svchost.exe | 0.0 | 4500 | 4500 | 8 | Microsoft Corporation | 0x000000000000000 |
| 3200 | lsass.exe | 0.0 | 9200 | 9200 | 2 | Microsoft Corporation | 0x000000000000000 |
| 4100 | wininit.exe | 0.0 | 2100 | 2100 | 1 | Microsoft Corporation | 0x000000000000000 |
| 5000 | csrss.exe | 0.0 | 3300 | 3300 | 4 | Microsoft Corporation | 0x000000000000000 |

