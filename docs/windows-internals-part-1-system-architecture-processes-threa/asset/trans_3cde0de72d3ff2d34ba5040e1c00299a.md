
以前不需要担心这个问题，因为系统会直接崩溃。然而，由于低内存状态可能会临时发生，而且今天的移动设备性能不如大型机器，因此让设备驱动程序妥善处理指示内核内存耗尽的分配失败至关重要。

被调用时可能随机失败的驱动程序包括：`ExAllocatePool*`、`MmProbeAndLockPagesSpec`、`MmMapIoCache`、`MmAllocateContiguous-Memory`、`MmAllocatePagesForId`、`IoAllocateInt`、`IoAllocateMd`、`IoAllocateWorkItem`、`IoAllocateErrorLogEntry`、`IoSetCompleteRoutineEx` 以及其他从池分配的 R API。Verifier 会验证内核 GDI 函数管理的分配（完整列表请参见 WDK 文档）。此外，你还可以指定以下内容：

- **分配失败的概率**：默认为 6%。

- **哪些应用程序应接受模拟**：默认为所有应用程序。

- **哪些池标记应受影响**：默认为所有。

- **启动故障注入前应使用多长的延迟**：默认是系统启动后 7 分钟，这足以跳过关键初始化阶段，在该阶段低内存状态可能会阻止设备驱动程序的加载。

你可以通过 `verifier.exe` 的命令行选项更改这些自定义设置。

在该阶段结束后，Driver Verifier 会对其验证的设备驱动程序开始随机导致分配调用失败。如果驱动程序没有正确处理分配失败，这可能会表现为系统崩溃。

## 系统性低资源模拟

与低资源模拟类似，此选项会对内核和 `Ndis.Sys`（针对网络驱动程序）的某些调用执行失败，但它是以系统的方式进行的，通过检查故障注入点的调用栈。如果驱动程序正确处理了失败，则该调用栈将不再被注入。这允许驱动程序以系统的方式发现问题、修复报告的问题并继续处理下一个。检查所有调用栈是一项开销较大的操作，不建议使用此功能一次验证多个驱动程序。

## 杂项检查

Driver Verifier 用的某些杂项检查允许它检测池中处于活动状态的系统结构被释放。例如，Driver Verifier 会检查：

- **空闲内存中的活动工作项**：驱动程序调用 `ExFreePool` 释放池块时，仍存在通过 `IoQueueWorkItem` 队列的一个或多个工作项。

- **空闲内存中的活动资源**：驱动程序在调用 `ExDelete-Resource` 销毁 `ERSOURCE` 对象之前调用了 `ExFreePool`。

- **空闲内存中的活动旁路列表**：驱动程序在调用 `ExDelete-PagedLookasideList` 或 `ExDeletePagedLookasideList` 删除旁路列表之前调用了 `ExFreePool`。

最后，启用验证后，Driver Verifier 会执行某些无法单独启用或禁用的自动检查。这些包括：

- 在具有错误标志的 MDL 上调用 `MmProbeAndLockPages` 或 `MmProbeAndLockProcessPages`。例如，对未映射的 MDL 调用 `MmProbeAndLockPages` 是错误的。

- 在具有错误标志的 MDL 上调用 `MmMapIoCache`。例如，对未映射的 MDL 调用 `MmMapIoCache` 是错误的。

- 在未映射的 MDL 上调用 `MmFreePoolPages`。

- 在未映射的 MDL 上调用 `MmFreeIoCache`。

Driver Verifier 是系统极有价值的补充，并参与了系统的设置、升级和迁移。

## 即插即用

PnP 管理器是 Windows 中适应不断变化的硬件的主要组件。例如，它允许系统在无需人工干预的情况下检测、配置和删除设备。PnP 管理器提供以下功能：

- 设备枚举。

- 资源分配。

- 设备状态管理。

- 硬件更改通知。

Windows 旨在对即插即用提供完全支持，但可能的程度取决于连接的设备；如果单个设备或驱动程序不支持即插即用，系统的支持范围可能会受到影响。表 6-6 显示了支持和不支持即插即用的设备与驱动程序组合的结果。

6-6 设备与即插即用能力

| 设备类型 | 即插即用驱动程序 | 非即插即用驱动程序 |
|---|---|---|
| 即插即用 | 完全即插即用 | 不即插即用 |
| 非即插即用 | 部分即插即用 | 不即插即用 |

不支持即插即用的设备是指不支持自动检测的设备，例如旧声卡。由于操作系统不知道硬件物理上是否存在，某些操作（如笔记本电脑拔坞和睡眠）是不被允许的。然而，如果为设备手动安装了即插即用驱动程序，该驱动程序可以实现由 PnP 管理器引导的设备资源分配。

旧式

