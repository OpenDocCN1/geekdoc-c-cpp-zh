
State: `0x3` (Running) Running on processor 7

尽管流程的某些细节在架构之间有所不同（这是汇编语言程序之一，而不是 C 语言），但空闲线程的基本序列如下：

1. 空闲线程启用待处理的中断并将其禁用（在 x86 和 x64 处理器上使用 `STI` 和 `CLI` 指令）。这样做是有利的，因为空闲线程的大部分是在中断禁用的情况下执行的。
2. 在某些架构的调试构建，空闲线程检查内核调试器是否尝试中断系统。如果是，它将获得访问权限。
3. 空闲线程检查是否有待处理的 DPC（第 6 节描述）。如果 DPC 在生成时没有产生中断，它们可能处于待处理状态。如果存在 DPC，空闲循环调用 `KiRetList` 来交付它们。这还将执行定时器过期以及延迟读取；后者将在随后的“多处理器系统”中解释。`KiRetList` 必须在禁用中断的情况下进入，这就是为什么在第 I 步结束时中断仍处于禁用状态。`KiRetList` 退出时也是禁用中断状态。
4. 空闲线程检查是否请求了时间片过期。如果是，则调用 `QuantumEnd` 来处理该请求。
5. 空闲线程检查是否有线程被选择在下一个处理器上运行。如果是，则调度该线程。这可能是因为第 3 步中处理的 DPC 或定时器过期解决了等待线程的情况，或者当该线程已经在空闲循环中时，另一个处理器为该处理器选择了该线程。
6. 如果根据请求，空闲线程检查其他处理器上准备就绪的线程，并在可能的情况下在本地调度其中一个。（该操作将在随后的“空闲调度程序”中解释）
7. 空闲线程调用注册的电源管理处理器空闲例程（无论如何执行电源管理功能），该例程要么在处理器驱动程序（如 `intelppm.sys`）中，要么如果没有此类驱动则在 HAL 中。

## 线程挂起

线程可以通过 `SuspendThread` 和 `ResumeThread` API 函数显式地被挂起和恢复。每个线程都有一个挂起计数（suspend count），在挂起时加1，在恢复时减1。如果计数为 0，则该线程可以执行；否则，它将不会执行。

挂起的工作原理是通过向线程队列一个内核 APC（异步过程调用）来实现。当线程切换到执行时，会先执行该 APC。这使得线程处于等待状态，直到线程最终恢复时触发事件信号，其退出等待状态。

如果线程在挂起请求到来时处于等待状态，那么这种挂起机制有一个明显的缺点，因为这意味着线程需要被唤醒仅仅是为了再次被挂起。这（如果线程的内核栈被交换出）可能会导致内核栈缺页。Windows 8.1 和 Server 2012 R2 了一种名为“轻量级挂起”（Lightweight Suspend）的机制，允许在不使用 APC 机制的情况下挂起处于等待状态的线程，而是直接操作内存中的线程对象并将其标记为挂起。

## （深度）冻结

冻结是一种机制，进程进入一种挂起状态，该状态无法通过在线程上调用 `ResumeThread` 来改变。这在系统需要挂起 UWP 应用时非常有用。这通常发生在 Windows 应用进入后台时——例如，另一个应用进入了前台，或者该应用处于挂起模式。在这种情况下，系统会给应用程序大约五秒的时间运行，通常用于保存应用程序状态。保存状态非常重要，因为如果内存资源不足，Windows 应用可能会在不通知的情况下被杀死。如果应用被杀死，状态可以在下次启动时重新加载，用户会觉得应用从未消失。冻结进程意味着以某种方式挂起所有线程，使得 `ResumeThread` 无法唤醒它们。`KTHREAD` 结构中的一个标志位指示线程是否被冻结。要使一个线程能够执行，其挂起计数必须为 0 且 `Frozen` 标志位必须置零。

深度冻结增加了另一个限制：进程中新创建的线程无法启动得那么快。例如，如果使用 `CreateThread` 调用在深度冻结的进程中创建一个新线程，该线程将在实际启动之前被冻结。这是冻结功能的典型用法。

进程和线程冻结功能没有直接暴露给用户态。它由进程状态管理器（PSM）服务内部使用，该服务负责向内核发出释放和解冻（取消冻结）请求。

你也可以使用作业（jobs）来冻结进程。冻结和解冻作业的能力没有公开文档说明，但可以使用标准的 `SetInformationJob` 系统调用来实现。这通常用于 Windows 应用，因为所有 Windows 应用都包含在作业中。此类作业可能包含单个进程（Windows 应用本身），但也可以包含与同一 Windows 应用程序相关的后台任务托管进程，这样就可以一次性完成对该作业下所有进程的冻结或解冻。（Windows 应用请参阅第 2 部分的第 8 章。）

## 实验：深度冻结

在这个实验中，你将通过调试虚拟机来观察深度冻结的发生。

1. 以管理员权限打开 `WinDbg` 并挂载到正在运行 Windows 10 的虚拟机上。
2. 按 `Ctrl+Break` 进入虚拟机的调试模式。
3. 当深度冻结开始时，使用显示被冻结进程的命令设置断点：

```
bp nt!PsFreezeProcess "process -1 0; g"
```
4. 输入 `g`（go）命令或按 F5。你应该能看到许多深度冻结的发生。
5. 从任务栏启动 UI，然后关闭 UI。大约 5 秒后，你将看到如下内容：

```
PROCESS 8F518500 SessionId: 2 Cid: 12c8 Peb: 03945000 ParentCid: 02ac

DirBase: 054007e0 Object: b0a8a040 HandleCount: 988.

Image: SearchUi.exe
```
6. 现在退出调试器并显示该进程的更多信息：

```
kd> !process 8F518500 1

PROCESS 8F518500 SessionId: 2 Cid: 12c8 Peb: 03945000 ParentCid: 02ac

DeepFreeze

DirBase: 054007e0 Object: b0a8a040 HandleCount: 988.

Image: SearchUi.exe

VadRoot 9c1fffd8 Vads 405 Clone 0 Priority 7682. Modified 2024. Locked 0nDeviceDevice a12509c0

Token b0a65bd0

ElapsedTime 04:02:33.518

UserTime 00:00:06.937

KernelTime 00:00:00.703

QuotaPoolUsage[PagedPool] 562688

QuotaPoolUsage[NonPagedPool] 34392

Working Sets (now,min,max) (20470, 50, 345) (81880KB, 200KB, 13880KB)

PeakWorkingSetSize 25878

VirtualSize 367 Mb

PeakVirtualSize 400 Mb

PageFaultCount 307764

MemoryPriority BACKGROUND

BasePriority 8

CommitCharge 8908

Job
```
7. 退出调试器查看作业，注意作业是否处于冻结状态。使用作业命令查看更多信息：

```
kd> !job
```
8. 停止深度冻结，然后启动 UI 观察其解冻过程。

# 多处理器系统

在单处理器系统上，调度相对简单：想要运行的优先级最高的线程始终运行。在多处理器系统上，情况要复杂得多。这是因为 Windows 会尝试将线程调度到对该线程最优的处理器上，并考虑了线程的偏好处理器、之前运行过的处理器，以及多处理器系统的配置。因此，尽管 Windows 尝试在所有 CPU 上调度最高优先的可运行线程，但它仅保证在某个某处运行其中一个最高优先的线程。通过共享队列（对于那些没有设置节点亲和性限制的线程），这种保证会更强。每个共享的处理器组都至少在运行一个最高优先的线程。

在描述用于选择哪些线程运行以及何时运行的特定算法之前，让我们先检查 Windows 在多处理器系统中为了跟踪线程和处理器状态而维护的额外信息，以及 Windows 支持的三种不同类型的多处理器系统（SMT、多核和 NUMA）。

## 组与 SMT 组

Windows 在处理逻辑处理器拓扑结构时，使用 `KPRCB` 中的五个字段来确定正确的调度方案。第一个字段 `CorePhysicalProcessor`（核心物理处理器）确定其逻辑处理器是否是多路封装包的一部分。它是根据处理器返回的 `CPUID` 计算并四舍五入到 2 的幂的。第二个字段 `LogicalProcessorsCore`（逻辑处理器核心）确定逻辑处理器是否是 SMT 组的一部分（例如在带有线程线程的 Intel 处理器上），它也通过 `CPUID` 查询并进行四舍五入。这两个数字相乘得到每个封装包的逻辑处理器数量，或者是适合插槽的实际物理处理器数量。通过这些数字，每个 `PRCB` 都可以填充其 `PackageValueSet`（封装包值集）。该亲和性掩码描述了该组内的其他哪些逻辑处理器（因为封装包被限制在一个组内）属于同一个物理处理器。类似地，`CoreProcessorSet`（核心处理器集）将其他逻辑处理器连接到同一个核心，此外 `GroupSetMember` 值定义了当前处理器组内的哪个位掩码，当前处理器组的 `GroupSetMember` 值为 8（等于 2 的 3 次方）。

## 实验：查看逻辑处理器信息

你可以使用内核调试器中的 `!smt` 命令检查 Windows 为 SMT 处理器维护的信息。以下输出来自一个带有 SMT（八个逻辑处理器）的四核 Intel i7 系统：

```
1kd> !smt

SM Summary:
```

```
KeActiveProcessors:

........ (000000000000000ff)

IdleSummary:

........ (0000000000000009e)
```

| 编号 | PRCB | SMT | APIC Id |
|---|---|---|---|
| 0 | fffffba03d7546180 | -- | (0000000000000003) 0x0000000 |
| 1 | fffffba01cb33180 | -- | (0000000000000003) 0x0000001 |
| 2 | fffffba01cb3dd180 | -- | (0000000000000003) 0x0000002 |
| 3 | fffffba01cb22180 | -- | (000000000000000c) 0x0000003 |
| 4 | fffffba01cb266180 | -- | (0000000000000000) 0x0000004 |
| 5 | fffffba01cabd6180 | -- | (0000000000000030) 0x0000005 |
| 6 | fffffba01cb491180 | -- | (000000000000000c) 0x0000006 |
| 7 | fffffba01cb5d4180 | -- | (000000000000000c) 0x0000007 |

每个物理处理器的最大核心数：8
每个核心的逻辑处理器数量：2

## NUMA 系统

Windows 支持另一种类型的多处理器系统是具有非均匀内存架构（NUMA）的系统。在 NUMA 系统中，处理器被分组在较小的节点中。每个节点都有自己的处理器和内存，并通过缓存一致性互连连接到更大的系统。这些系统是非均匀的，因为每个节点都有自己的本地速度内存。

内核在数据结构 `KNODE` 中维护 NUMA 系统中每个节点的信息。内核变量是一个指向每个节点的 `KNODE` 指针的数组。你可以使用内核调试器中的 `dt` 命令查看 `KNODE` 的格式，所示：

```
kd> dt nt!KNODE

+0000 IdleParkedSet : Uint8

+0008 IdleMemSet : Uint8

+0010 IdleCpuSet : Uint8

+0040 DeepIdleSet : Uint8

+0048 ConstrainedSet : Uint8

+0050 NonParkedSet : Uint8

+0058 ParkLock : Int44

+005c Seed : Uint8

+0080 SiblingMask : Uint8

+0088 Affinity : _GROUP_AFFINITY

+0088 AffinityFill : [10] UChar

+0092 NodeNumber : Uint2B

+0094 NodeNumber : Uint2B

+0096 Stride : Uint8

+0097 Spare : Uint8

+0098 SharedQueue : Uint8

+00a0 ProximityId : Uint8

+00a4 Lowest : Uint8

+00a8 Highest : Uint8

+00ac MaximumProcessors : Uint8

+00ad Flags : Uint8

+00b0 SharedSets : UChar
```

## 实验：查看 NUMA 信息

你可以使用内核调试器中的 `!numa` 命令检查 Windows 为 SMT 处理器维护的信息。对于非 NUMA 系统，该命令将没有可用的信息。以下是来自一个带有 SMT（八个逻辑处理器）的四核 Intel i7 系统的输出（注，此处示例逻辑应为 NUMA 示例）：

要在 NUMA 系统中检查 Windows 为每个节点维护的信息，可以按照以下步骤：

1. 在内核调试器中使用 `!smt` 命令检查 SMT 处理器信息（此处示例应为 `!numa`）。
2. 在 NUMA 系统中，可以使用 `!numa` 命令检查 Windows 为每个节点维护的信息。对于非 NUMA 系统，该命令将没有可用的信息。以下是来自配置了 NUMA 的系统输出：

```
1kd> !smt

NUMA Summary:
```

```
KeActiveProcessors:

........ (000000000000000ff)

IdleSummary:

........ (0000000000000009e)
```

| 编号 | PRCB | SMT | APIC Id |
|---|---|---|---|
| 0 | fffffba03d7546180 | -- | (0000000000000003) 0x0000000 |
| 1 | fffffba01cb33180 | -- | (0000000000000003) 0x0000001 |
| 2 | fffffba01cb3dd180 | -- | (0000000000000003) 0x0000002 |
| 3 | fffffba01cb22180 | -- | (000000000000000c) 0x0000003 |
| 4 | fffffba01cb266180 | -- | (0000000000000000) 0x0000004 |
| 5 | fffffba01cabd6180 | -- | (0000000000000030) 0x0000005 |
| 6 | fffffba01cb491180 | -- | (000000000000000c) 0x0000006 |
| 7 | fffffba01cb5d4180 | -- | (000000000000000c) 0x0000007 |

每个物理处理器的最大核心数：8
每个核心的逻辑处理器数量：2

## NUMA 系统

Windows 支持的另一种类型的多处理器系统是具有非均匀架构（NUMA）的系统。在 NUMA 系统中，处理器被分组在较小的节点中。每个节点都有自己的处理器和内存，并通过缓存一致性互连连接到更大的系统。这些系统是非均匀的，因为每个节点都有自己的本地速度内存。

内核在数据结构 `KNODE` 中维护 NUMA 系统中每个节点的信息。内核变量是一个指向每个节点的 `KNODE` 指针的数组。你可以使用内核调试器中的 `dt` 命令查看 `KNODE` 的格式，如下所示：

```
kd> dt nt!KNODE

+0000 IdleParkedSet : Uint8

+0008 IdleMemSet : Uint8

+0010 IdleCpuSet : Uint8

+0040 DeepIdleSet : Uint8

+0048 ConstrainedSet : Uint8

+0050 NonParkedSet : Uint8

+0058 ParkLock : Int44

+005c Seed : Uint8

+0080 SiblingMask : Uint8

+0088 Affinity : _GROUP_AFFINITY

+0088 AffinityFill : [10] UChar

+0092 NodeNumber : Uint2B

+0094 NodeNumber : Uint2B

+0096 Stride : Uint8

+0097 Spare : Uint8

+0098 SharedQueue : Uint8

+00a0 ProximityId : Uint8

+00a4 Lowest : Uint8

+00a8 Highest : Uint8

+00ac MaximumProcessors : Uint8

+00ad Flags : Uint8

+00b0 SharedSets : UChar
```
