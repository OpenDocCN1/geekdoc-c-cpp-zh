

接下来的章节将讨论 KMDF 和 UMDF，无论它们运行在哪个操作系统上，其行为本质上是一致的。

# 内核模式驱动框架

我们在第 2 章中已经讨论了 Windows 驱动程序框架（WDF）的一些细节。在本节中，我们将更深入地查看框架内核模式部分 KMDF 提供的组件和功能。请注意，本节将仅简要介绍 KMDF 的部分核心架构。欲需关于该主题更全面的概述，请参考 Windows 驱动程序包（Windows Driver Kit）文档。

> 本节中介绍的大部分细节与 UMDF 2.x 相同，但下一节讨论的例外除外。

# KMDF 驱动程序的结构和操作

首先，让我们看看 KMDF 支持哪些类型的驱动程序或设备。通常，只要驱动程序执行标准的 I/O 处理和 IRP 操作，KMDF 就应该支持符合 WDM 的驱动程序。KMDF 不适用于那些不直接使用 Windows 内核 API 而通过库调用进入现有端口和类驱动程序（port and class drivers）的驱动程序。这些类型的驱动程序无法使用 KMDF，因为它们只为执行 I/O 处理的实际 WDM 驱动程序提供回调。此外，如果驱动程序提供自己的分发函数而不是依赖端口或类驱动程序，IEEE 1394、ISA、PCI、PCMCIA 和 SD 客户端（用于安全数字存储设备）驱动程序也可以使用 KMDF。

尽管 KMDF 在 WDM 之上提供了抽象，但之前所示的基本驱动程序结构通常适用于 KMDF 驱动程序。在其核心，KMDF 驱动程序必须具有以下函数：

- **初始化例程 (Initialization routine)**：像任何其他驱动程序一样，KMDF 驱动程序有一个初始化驱动程序的 `DriverEntry` 函数。KMDF 驱动程序在此启动框架，并执行属于驱动程序部分或描述框架部分的配置和初始化步骤。对于非即插（Plug and Play）驱动程序，这里应该是创建第一个设备的地方。
- **添加设备例程 (Add-device routine)**：KMDF 驱动程序的操作基于事件和回调（稍后将描述），`EvtDriverDeviceAdd` 回调对于 PnP 设备最重要的，因为当内核中的 PnP 管理器枚举驱动程序的某个设备时，它会接收到通知。
- **一个或多个 EvtIo 例程 (One or more EvtIo routines)**：类似于 WDM 驱动程序的分发例程，这些回调处理来自特定设备队列的特定类型 I/O 请求。驱动程序通常创建一个或多个队列，KMDF 在这些队列中为驱动程序的设备放置 I/O 请求。这些队列可以根据请求类型和分发类型进行配置。

最简单的 KMDF 驱动程序可能只需要初始化和去激活例程，因为框架将提供大多数类型 I/O 处理所需的默认通用功能，包括电源和即插即用（Play）事件。在 KMDF 模型中，事件指的是驱动程序可以响应或期间参与的运行状态（run-states）。这些事件与同步无关（同步将在第 2 部分第 8 章讨论），而是框架内部的。

对于对驱动程序运行至关重要或需要特殊处理的事件，驱动程序注册一个回调例程来处理该事件。在其他情况下，驱动程序可以允许 KMDF 执行默认的通用操作。例如，在事件（`EvtDeviceEject`）之后，驱动程序可以选择提供弹出回调，或者退回到默认的 KMDF 代码，该代码将告诉用户设备不支持弹出。然而，并非所有事件都有默认行为，必须由驱动程序提供回调。一个显著的例子是上述描述的 `EvDriverDeviceAdd` 事件，它是任何即插即用驱动程序的核心。

# 实验：显示 KMDF 和 UMDF 2 驱动程序

随 Windows 调试工具包分发的 `Wdfkd.dll` 扩展提供了许多可以用于调试和分析 KMDF 驱动程序的命令（而不是使用内置的 WDM 调试扩展，后者可能无法提供同样的 WDF 特有信息）。你可以使用 `!wdfkd.wdf1dr` 命令安装 KMDF 驱动程序。在下面的示例中，显示了来自 Windows 10 32 位 Hyper-V 虚拟机的输出，展示了已安装的内置程序。

```
1kd> !wdfkd.wdf1dr
```

| KMDF 驱动程序 | | |
| :--- | :--- |
| LoadedModuleList | 0x8626aa8d |
| LIBRARY_MODULE | v1.19 |
| Service | \Registry\Machine\System\CurrentControlSet\Services\Wdf01000 |
| ImageName | Wdf01000.sys |
| ImageAddress | 0x87000000 |
| ImageSize | 0x08f0000 |
| Associated Clients: 25 | |

| ImageName | WdfGlobals | FxGlobals | ImageAddress | ImageSize |
| :--- | :--- | :--- | :--- | :--- |
| uppass.sys | v1.5 | 0xa5e53f8 | 0xa5e2f58 | 0xe9e5f000 | 0x00008008 |
| peauth.sys | v1.7 | 0x95e79d8 | 0x95e79d7 | 0x9e400090 | 0x0000ba00 |
| msldp.sys | v1.5 | 0xa9aed1b5 | 0xa9aed150 | 0x8e30000 | 0x0001140 |
| vmgid.sys | v1.5 | 0xd97f02d8 | 0xd97f02d7 | 0x08e2fc08 | 0x00008080 |
| monitor.sys | v1.5 | 0xa97cfe18 | 0xa97cfe1d | 0x8e250000 | 0x0000c00 |
| tsusbhub.sys | v1.5 | 0xa97cb3108 | 0xa97cb3108 | 0x8e4b0000 | 0x0001b00 |
| NdisVirtualBus.sys | v1.5 | 0x8d0fc2b0 | 0x8d0fc1b0 | 0x87a09000 | 0x00009900 |
| vmgencounter.sys | v1.5 | 0xd8d0fefe0 | 0xd8d0fefe0 | 0x87a84000 | 0x00008000 |
| intppm.sys | v1.5 | 0xd8d0f4c70 | 0xd8d0f4b80 | 0x87a55000 | 0x00021000 |
| vms3cap.sys | v1.15 | 0xd8df05218 | 0xd8df05318 | 0x87a04000 | 0x00008000 |
| netvsc.sys | v1.15 | 0xd8d011ded0 | 0xd8d011dd0 | 0x87a00000 | 0x00009000 |
| hyperkbd.sys | v1.15 | 0xd8d011448 | 0xd8d011438 | 0x87a00000 | 0x00011000 |
| dmvcs.sys | v1.15 | 0xd8d002db28 | 0xd8d002da8 | 0x87a99000 | 0x0000c00 |
| umbus.sys | v1.15 | 0xb8b066fd0 | 0xb8b066fe0 | 0x87f40000 | 0x0001100 |
| CompositeBus.sys | v1.15 | 0xb8b066919 | 0xb8b066918 | 0x87f00000 | 0x0000d000 |
| cdrom.sys | v1.15 | 0xb8b066320 | 0xb8b066320 | 0x87f40000 | 0x00024000 |
| vmstorfl.sys | v1.15 | 0xb2b029108 | 0xb2b029108 | 0x87c00000 | 0x00000000 |
| EhStorClass.sys | v1.15 | 0xa9d0acfb8 | 0xa9d0adf7 | 0x87d00000 | 0x00015000 |
| umbus.sys | v1.15 | 0xa9b088c70 | 0xa9b088c60 | 0x87e00000 | 0x00018000 |
| vdroot.sys | v1.15 | 0xa9b070728 | 0xa9b070728 | 0x87620000 | 0x00005000 |
| misadriv.sys | v1.15 | 0xa9a056d98 | 0xa9a056d90 | 0x87c03000 | 0x00008000 |
| WindowsRTProxy.sys | v1.15 | 0xa810f1fc10 | 0xa810f1c40 | 0x87b04000 | 0x00004000 |
| WindowsRTDT.sys | v1.15 | 0xa810f1fd0 | 0xa810f1ed0 | 0x87220000 | 0x00017000 |
| intelp.sys | v1.15 | 0xa9a05ef690 | 0xa9a05ef590 | 0x87221000 | 0x00000000 |
| aciex.sys | v1.15 | 0xd8d06287d0 | 0xd8d06287e0 | 0xa8000000 |

表 6-11 列出了 KMDF 支持的对象类型：

| 对象 | 类型 | 描述 |
| :--- | :--- | :--- |
| 列表 | WDFLIST | 这是与 KM  相关列表。 |
| 集合 | WDFCOL | 它是驱动程序的一个集合。 |
| 延迟过程调用 | WDFPC | 这是一个内核调度事件对象。 |
| 设备 | WDFDEVICE | 这是一个实例。 |
| DMA 通用缓冲区 | WDFCOMMONBUFFER | 驱动程序的 DMA 区域。 |
| DMA 启用 | WDFENABLE | 为驱动启用 DMA。 |
| DMA 事务 | WDFTRANSACTION | 这是一个 DMA 事务实例。 |
| 驱动程序 | WDFDRIVER | 描述驱动程序及其参数、回调以及其他项。 |
| 文件 | WDFFILE | | 与驱动程序程序通信的文件实例。 |
| 通用对象 | WDFOBJECT | 允许在框架内部定义自定义数据。 |
| 中断 | WDFINTERRUPT |驱动程序必须处理的中断实例。 |
| I/O 队列 | WDFQUEUE | 代表给定的 I/O 队列。 |
| I/O 请求 | WDFREQUEST | WDFQUEUE 上的请求。 |
| I/O 目标 | WDFTARGET | WDFREQUEST 指向的设备栈。 |
| 侧边列表 | WDFLOOKIDE | 侧边列表（参见第 5 章）。 |
| 内存 | WDFMEMORY | 分页或非分页池区域。 |
| 注册键 | WDFKEY | 注册项。 |
| 资源列表 | WDFIORESLIST | 分配给 WDFDEVICE 的硬件资源。 |
| 资源范围列表 | WDFIORESLIST | WDFDEVICE 一个可能的硬件资源范围。 |
| 资源需求列表 | WDFIORESQLIST | 包含描述 WDFDEVICE 所有可能资源范围的 WDFIORES 对象数组。 |

