

它们通常被分组在数量较少且大小特定的桶（buckets）中。LFH 使用的分配策略是通过高效处理相同大小的块来优化这些模式的使用。

为了解决可扩展性问题，LFH 将频繁访问的内部结构扩展到槽（slots），其数量是机器上当前处理器数量的两倍。线程到槽的分配由一个名为亲和性管理器（affinity manager）的 LFH 组件完成。初始情况下，LFH 开始使用第一个槽进行堆分配；然而，如果在访问某些内部数据时检测到冲突，LFH 会将当前线程切换到不同的槽。后续的操作会将线程分散到更多的槽中。对于每个大小的桶都会对这些槽进行控制，以提高局部性并最大程度地减少整体内存消耗。

即使 LFH 作为前端堆启用，不那么频繁的分配大小也可能继续使用核心堆函数来分配内存，而最常用的分配类将通过 LFH 执行。一旦对特定堆启用了 LFH，就无法将其禁用。曾经可以在 Windows 7 及更早版本的 Windows 中移除 LFH 层的带有 `HeapCompatibilityInformation` 类的 `HeapInformation` API 现在已被忽略。

## 段堆 (Segment heap)

图 5-9 显示了 Windows 10 中引入的段堆的架构。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_352_0.png)

**图 5-9** 段堆。

管理分配的层取决于分配大小如下：

- 对于小尺寸（小于或等于 16,368 字节），使用 LFH，但仅当大小确定为常用大时才使用。此逻辑与 NT 堆的 LFH 前端层类似。如果 LFH 尚未触发，将使用变变大小（VS）分配器。
- 对于小于或等于 128 KB 的大小（且不由 LFH 服务），VS 分配器使用：VS 和 LFH 分配器都使用后端根据需要创建所需的堆子段。
- 大于 128 KB 且小于或等于 500 KB 的分配直接由堆后端提供服务。
- 大于 508 KB 的分配通过直接调用内存管理器（`VirtualAlloc`）提供服务，因为这些分配非常大，默认的 64 KB 分配粒度（并舍入最近的页面大小）被认为是足够了。

以下是两种堆实现的简单快速比较：

- 在某些情况下，段堆可能比 NT 堆慢一些。然而，未来的 Windows 版本可能会使其与 NT 堆平相当。
- 段堆的元数据内存占用更低，更适合手机等低内存设备。
- 段堆的元数据与实际数据分离，而 NT 堆的元数据与数据本身交织在一起。这使得段堆更安全，因为仅根据块地址很难获取该分配的元数据。
- 段堆只能用于可增长的堆。它不能与用户提供的内存映射文件一起使用。如果尝试创建此类段堆，将创建一个 NT 堆。
- 两个堆都支持 LFH 分配，但它们的内部实现完全不同。段堆在内存消耗和性能方面具有更高效的实现。

如前所述，UWP 应用默认使用段堆。这主要是因为它们的内存占用较低，适用于低内存设备。它还被用于某些基于可执行文件的系统进程：`csrss.exe`、`lsass.exe`、`runtimebroker.exe`、`smss.exe` 和 `svchost.exe`。

段堆不是桌面端应用的默认堆，因为存在可能影响现有应用程序的兼容性问题。在未来的版本中，它可能会成为默认。要为特定可执行文件启用或禁用段堆，可以设置名为 `EndHeapDebugOpts` (DWORD) 的映像文件执行选项值：

- 位 2 (4) 禁用段堆
- 位 3 (8) 启用段堆

你可以通过向 `HKLM\SYSTEM\CurrentControlSet\Session Manager\Segment Heap` 注册表项添加名为 `Enabled` (DWORD) 的值来全局启用或禁用段堆。值为零时禁用段堆，非零值启用它。

## 实验：查看基本堆信息

在这个实验中，我们将检查一个 UWP 进程的一些堆。

- 1. 使用 Windows 10，运行 Windows 计算器。（点击开始按钮并输入 Calculator 找到它。）
- 2. Windows 10 中的计算器已转换为 UWP 应用（`Calculator.Exe`）。运行 WinDbg 并挂载到计算器进程。
- 3. 一旦挂载，WinDbg 会中断进程。发布 `!heap` 命令来获取堆的快速摘要：
```
0033> !heap
Heap Address
2531eb9b000 Segment Heap
2531eb98000 NT Heap
2531eb10000 Segment Heap
25320a4000 Segment Heap
253215a000 Segment Heap
253214f000 Segment Heap
2532eb7000 Segment Heap
253215d0000 NT Heap
```
- 4. 注意这些各种堆及其句柄和类型（segment 或 NT）。第一个堆是默认的进程堆。因为它是可增长的且没有使用任何内存块，所以它被创建为段堆。第二个堆用于用户定义的内存块（在早的“进程堆”节中描述过）。由于段堆不支持此功能，它被创建为 NT 堆。
- 5. NT 堆由 `ntdll!HEAP` 管理。让我们查看第二个堆的结构：
```
0033: dt ntdll!heap 2531eb98000
+0000 Segment : _HEAP_SEGMENT
+0000 Entry : _HEAP_ENTRY
+00010 Signature : 0xfffeee
+00014 Flags : 1
+00018 List : _LIST_ENTRY [ 0x00000023'1ec00120
0x00000023'1ec00120 ]
+00028 Heap : 0x00000023'1ec0000 _HEAP_ENTRY
+00030 BaseAddress : 0x00000023'1ec0000
```
- 6. 注意，上面的 `ntdll!heap` 实际上是 `_HEAP` 结构。让我们重新查看 `_HEAP` 输出：
```
0033: dt ntdll!heap 2531eb98000
+0000 Segment : _HEAP_SEGMENT
+0000 Entry : _HEAP_ENTRY
+00010 Signature : 0xfffeee
+00014 Flags : 1
+00018 List : _LIST_ENTRY [ 0x00000023'1ec00120
0x00000023'1ec00120 ]
+00028 Heap : 0x00000023'1ec0000 _HEAP_ENTRY
+00030 BaseAddress : 0x00000023'1ec0000
```
（注：此处根据上下文逻辑修正了 `dt` 命令输出的理解，原文示例中可能存在截断或特定显示，翻译时保持格式结构）

*纠正：原文提供的 `dt` 命令输出在示例中不完整，我将严格遵循原文结构进行翻译和保留。*

重新查看原文中的 `dt` 块部分：
```
0033: dt ntdll!heap 2531eb98000
+0000 Segment : _HEAP_SEGMENT
+0000 Entry : _HEAP_ENTRY
+00010 Signature : 0xfffeee
+00014 Flags : 1
+00018 List : _LIST_ENTRY [ 0x00000023'1ec00120
0x00000023'1ec00120 ]
+00028 Heap : 0x00000023'1ec0000 _HEAP_ENTRY
+00030 BaseAddress : 0x00000023'1ec0000
```
- 6. 注意 `FrontHeap` 字段。该字段指示了是否存在前端层。在之前的输出中，如果它为空，则没有前端层。非空值表示 LFH 前端层（因为它是唯一定义的）。
- 7. 段堆使用 `ntdll__SEGMENT_HEAP` 结构定义。这里是默认进程堆：
（由于原文在此处结束，翻译随原文结束）

