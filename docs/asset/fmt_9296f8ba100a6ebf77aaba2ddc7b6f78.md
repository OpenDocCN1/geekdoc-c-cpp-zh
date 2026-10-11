
对于每个进程，内存管理器维护一组描述进程地址空间状态的 `VADs`。`VAD` 组织在一个自平衡的 `AVL` 树中（以其发明者 Adelson-Velsky 和 Landis 命名，任何节点的两个子子树的高度差最多为 1；这使得插入、查找和删除变得非常快）。平均而言，在搜索与虚拟地址对应的 `VAD` 时，比较次数最少。对于每个具有所有相同特征（预留与已提交映射、内存访问保护等）的连续非虚拟地址范围，每个范围都有一个 `VAD`。图 5-29 显示了 `VAD` 树的图。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_418_0.png)

**图 5-29** `VADs`。

当进程引用地址空间或映射节视图时，内存管理器创建一个 `VAD` 来存储分配请求提供的任何信息，例如被预留的地址范围、该范围是共享还是私有的、子进程是否可以继承该范围的内容，以及应用于范围内页面的页保护。

当线程首次访问某个地址时，内存管理器必须为该页面创建一个 `PTE`。为了做到这一点，它找到包含该地址的 `VAD` 并使用其信息填充 `PTE`。如果地址落在 `VAD` 覆盖的范围之外，或者处于已预留未提交的地址范围内，内存管理器知道线程在尝试使用它之前没有分配内存，从而产生访问冲突。

## 实验：查看 VAD

你可以使用内核调试器 `!vad` 命令查看给定进程的 `VADs`。首先，使用 `!process` 命令找到 `VAD` 树的根地址。然后将该地址传递给 `!vad` 命令，如下所示的 `explorer.exe` 的 `VAD` 树。

```
kd> !process 0 explorer.exe
PROCESS fffc8069382e80
SessionId: 1 Cid: 43e0 Peb: 0 ParentId: 338
Base: 55ab700 ObjectTable: fffda86281d80 HandleCount: 823.
image: explorer.exe
VadRoot fffc80691237f0 Vads 505 Clone 0 Private 5088. Modified: 2146. Locked: 0.
```

```
kd> !vad fffc8069a470 End VAD Level Start
ffff809bc52b0 9 640 64f 0 Mapped READWRITE
Pagefile section, shared commit 0x10
ffff809be6900 8 650 0 Mapped READONLY
Pagefile section, shared commit 0x2
ffff809bc4290 9 660 675 0 Mapped READONLY
Pagefile section, shared commit 0x16
ffff809ae1f320 7 680 0 32 Private READWRITE
ffff809b292b0 9 700 2 701 READWRITE
ffff809dda470 8 710 2 Private READWRITE
ffff809279570 6 720 0 23 Mapped READONLY
Pagefile section, shared commit 0x4
ffff80985670 10 730 0 31 Mapped READONLY
Pagefile section, shared commit 0x2
ffff809bd9d90 9 740 2 41 Private READWRITE
ffff809d5a7b0 8 750 0 Mapped READONLY
\Windows\explorer.exe
Total VADs: 574, average level: 8, maximum depth: 10
Total private commit: 0x3420 pages (53376 KB)
Total shared commit: 0x478 pages (4576 KB)
```

## 旋转 VAD

视频驱动程序通常必须从用户态内存（包括显卡内存和 `AGP` 端口）复制数据。为了快速将这些内存视图映射到进程并支持这些缓存属性，内存管理器实现了旋转 `VAD`，允许视频驱动程序通过 `GPU` 直接传输数据，并按需将不需要的内存调入进程页面。图 5-30 显示了相同地址如何在显存和虚拟内存之间旋转的示例。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_419_0.png)

图 5-30。

Windows 的每个版本都对内存管理器进行了改进，以更好地利用非统一内存架构 `NUMA` 设备，例如大型服务器系统以及 Intel 和 AMD 工作站。内存管理器中的 `NUMA` 支持增加了对节点信息（如位置、拓扑和访问成本）的智能感知，允许应用程序和驱动程序利用 `NUMA` 能力，同时抽象底层硬件细节。

内存管理器初始化时，调用 `MiComputeMemoryCosts` 在不同节点上执行各种页面和缓存操作。然后计算操作完成所需的时间。根据这些信息，它构建了一个访问成本图（节点与系统中节点之间的距离）。当系统为特定操作需要页面时，它查询图表以选择最佳节点（即最近的节点）。如果该节点没有可用内存，它将选择最近的节点，依此类推。

尽管内存管理器确保尽可能让内存分配来自执行分配的线程的处理器节点（理想节点），但它也提供了函数允许应用程序选择自己的节点，例如 `VirtualAllocEx`、`CreateFileMapping`、`MapViewOfFileEx` 和 `AllocateUserPages` `API`。

理想节点不仅用于应用程序分配内存，还用于内核操作和页错误。例如，运行在非理想处理器上的线程发生页错误时，内存管理器不会使用当前节点。相反，它将从线程的理想节点分配内存。虽然这在线程仍在该 CPU 上运行时可能会导致访问时间变慢，但随着线程迁移回其理想节点，内存访问将得到优化。在任何情况下，如果理想节点资源耗尽，将选择离理想节点节点，而不是随机的其他节点。然而，就像用户态应用程序一样，驱动程序在使用 `MmAllocatePagesForEx` 或 `MmAllocateMemoryCache` 等 `API` 时也可以指定自己的节点。

各种内存管理器池和数据结构也针对 `NUMA` 节点进行了优化。内存管理器尝试均匀使用系统中所有节点的物理内存来处理非分页池。进行分配时，内存管理器使用理想节点作为索引，在非分页池内部选择一个响应该节点物理内存的虚拟地址。此外，还创建了 `NUMA` 节点空闲列表以有效利用此类内存配置。除了非分页池，系统缓存和系统 `PTE` 也同样分配在所有节点上，以及内存管理器的旁列表中。

最后，当系统需要清零页面时，它通过创建与物理内存所在节点对应的 `NUMA` 亲和线程，在不同节点上并行执行。本地预取器和 `SuperFetch`（在“主动内存管理[SuperFetch]”节中描述）在预取期间也会使用目标进程的理想节点，而软错误会导致页面迁移到发生错误线程的理想节点。

# 节对象 (Section objects)

正如本章之前“共享内存和映射文件”节中所提到的，节对象（Windows 子系统称为*文件映射对象*，`file mapping object`）代表两个或多个进程可以共享的内存块。节对象可以映射到分页文件或磁盘上的另一个文件。

执行体使用节对象将可执行文件加载到内存中，缓存管理器则使用它们来访问缓存文件中的数据（有关缓存管理器如何使用节对象的更多信息，请参阅第 2 部分第 14 章）。你还可以使用节对象将文件映射到进程地址空间。然后，可以通过映射节对象的不同视图并对内存进行读写而不是文件，从而作为大数组来访问文件——这种活动被称为映射文件 `I/O`（`mapped file I/O`）。当程序访问无效页（不在物理内存中的页）时，会发生页错误，内存管理器会自动从映射文件或分页文件中将该页调入内存。如果应用程序修改了页，内存管理器会在正常操作期间更改写回文件。或者，应用程序可以使用 Windows 的 `FlushFile()` 函数显式地刷新文件。

像其他对象一样，节对象由对象管理器分配和释放。对象管理器创建并初始化对象头，并用它来管理对象；内存管理器定义节对象体（有关对象管理器的更多信息请参见第 2 部分第 8 章）。内存管理器还实现了用户态线程可以检索并更改存储在节对象主体中的属性的服务。节对象的结构如图 5-31 所示。表 5-14 总结了存储在节对象中的唯一属性。

| | 节 (Section) |
| :--- | :--- |
| 对象主体属性 | 最大大小 (Maximum Size)、页保护 (Page Protection)、是否基于分页文件或映射 |
| 服务 | 创建节 (Create Section)、打开节 (Open Section)、扩展节 (Extend Section)、映射/取消映射视图 (Map/Unmap View)、查询节 (Query Section) |

**图 5-31** 一个节对象。

**表 5-14** 节对象主体属性

| 属性 | 目的 |
| :--- | :--- |
| 最大大小 | 这是节可以增长的最大字节数。如果映射文件，则为文件的最大大小。 |
| 页保护 | 这是创建节时分配给节中所有页的基于页的内存保护。 |
| 分页文件或映射文件 | 这表示节是创建为空的（由分页文件支持——如前所述，文件支持的节仅在页需要写入磁盘时才使用分页文件资源）还是由文件支持（由映射文件支持）。 |
| 基于或不基于 | 这表示节是否为基于节（based section，它在所有进程中必须以相同的虚拟地址出现）或非基于节（non-based section，不同进程可以在不同的虚拟地址访问它）。 |

## 实验：查看节对象

你可以使用 Sysinternals 的 Process Explorer 查看进程映射的文件。按照以下步骤操作：

- 1. 打开视图（View）菜单，选择下窗格视图（Lower Pane View），并选择 DLLs。
- 2. 打开视图（View）菜单，选择选择列（Select Columns）、DLL，并启用映射类型（Mapping Type）列。
- 3. 注意映射（Mapping）列中被标记为 Data（数据）的文件。这些是映射文件，而不是 DLL 或映像加载器作为模块加载的文件。由分页文件支持的节对象在名称（Name）列中显示为 `<Pagefile Backed>`。否则，此处将显示文件名。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_422_0.png)

另一种查看对象的方法是寻找类型为 Section（节）对象的句柄（打开视图 View 菜单，选择下窗格视图 Lower Pane View，并选择句柄 Handles）。在下面的截图中，显示了对象名称（如果存在）。这不是支持该节的文件名（如果有）；它是在对象管理器命名空间中赋予节的名称。（有关对象管理器请参见第 2 部分第 8 章）。双击条目可以显示有关对象的更多信息，例如句柄数及其安全性。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_423_0.png)

内存管理器维护的描述映射节的结构结构如图 5-32 所示。这些结构确保了无论访问类型如何（打开文件、映射文件等），来自映射文件的数据都是一致的。对于每个打开的文件（由文件对象表示），都有一个节对象指针结构。该结构是维护所有访问类型一致性以及提供缓存的关键。节对象指针结构指向一个或两个控制区域。一个控制区域用于在文件作为数据文件访问时映射文件，另一个用于在文件作为可执行文件运行时映射文件。控制区域反过来指向节结构，该结构描述了文件的文件每个节（只读、读写等）的映射信息。控制区域还指向分配在分页页池（page pool）中的段结构（segment structure），段结构又指向原型 `PTE`（prototype `PTEs`），这些 `PTE` 用于映射到节对象映射的实际页。正如本章早些时候描述的，进程页表指向这些原型 `PTE`，指向正在处理的页。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_423_1.png)

图 5-32 内部节结构。

尽管 Windows 确保任何访问（读或写）文件的进程始终能看到相同的数据，但有一种情况，相同数据的副本可能存在于物理内存中。当文件作为数据文件（读或写）然后作为可执行文件运行时，这种重复就会发生。例如，当文件作为数据文件访问（读或写）然后作为可执行文件运行时，这种重复就会发生。当文件被映射为映像时，内部执行了以下操作：

- 1. 如果使用文件映射 `API` 或缓存管理器创建节，会创建一个数据控制区域表示数据页。
- 2. 当运行并创建节以映射映像时，内存管理器发现节对象指针指向数据控制区域并刷新节。为了确保在访问映像之前将修改的页写入磁盘。
- 3. 内存管理器为映像创建一个控制区域。
- 4. 当映像开始执行时，其（只读）页从映像文件调入，如果数据存在则直接从文件复制。

由于数据控制区域映射的页可能仍在空闲列表中，这就是相同数据的副本位于不同页中的情况。这种重复不会导致数据一致性问题。这是因为如提到的，数据控制区域已经刷新，因此从映像读取的页是最新的（且这些页不会写回磁盘）。

## 实验：查看控制区域

要找到文件的控制区域地址，必须首先获取文件对象的地址。你可以通过内核调试器转储进程表获取此地址，并记录文件对象的地址。虽然内核调试器的 `if1` 命令显示了文件对象的基本信息，但它没有显示指向节对象指针的指针。然后使用 `dt` 命令格式化文件对象以获取节对象指针的地址。该结构由三个指针组成：指向数据控制区域的指针、指向共享缓存映射（第 2 部分第 14 章解释）的指针以及指向映像区域的指针。通过节对象指针，可以获取文件控制区域的地址（如果存在）。）。

例如，如果你打开 PowerPoint 文件并使用 `!handle` 显示该进程的句柄表，你会发现一个打开 PowerPoint 文件的句柄（你可以进行搜索）。

```
1kd>!process 0 powerprnt.exe
PROCESS: fffc806813e80
```

```
SessionId: 1 Cid: 2b64 Peb: 0124000 ParentCid: 1d38
DirBase: 2525000 ObjectTable: fffda8f4926c40 HandleCount: 1915.
Image: POWERNT.EXE.
```

```
1kd>.process /p ffffc8068913e80
Implicit result is now ffffc806*8913e80
1kd>handle
```

```
0c08: Object: ffffc806f856ea60 GrantedAccess: 00120089 Entry: fda8f491d0020
Object: ffffc806f856ea60 Type: (ffffc806285625c00) File
ObjectHeader: ffffc806f856aa00 (new version)
HandleCount: 1 PointerCount: 30839
Directory Object: 0000000 Name: \WindowsInternals\7Edition\Chapter05\diagrams.pptx (HarddiskVolume2)
```

获取对象地址 (`FFFFC806F856A60`) 并使用 `dt` 进行格式化，结果如下：

```
1kd dt _nt_file_object ffffc806f856ea60
+0000 Type : 0n
+0002 Size : 0n16
+0008 DeviceObject : 0ffffc06*8408cb40 _DEVICE_OBJECT
+0010 Vpb : 0ffffc06*82feba00_Vpb
+0018 FsContext : 0ffffda8f*5137cd00 Void
+0020 FsContext2 : 0ffffda8f*43c63d590 Void
+0028 SectionObjectPointer : 0ffffc06*8ec0cc58 _SECTION_POINTERS
```

获取节对象指针地址 `0ffffc806*8ec0cc58` 并使用 `dt` 进行格式化，结果如下：

```
1kd dt _nt_section_object 0ffffc806*8ec0cc58
+0000 DataSectionObject 0ffffc806*8e83c10 Void
+0008 SharedCacheMap : 0ffffc08*8d967bd0 Void
+0010 ImageSectionObject : (null)
```

最后，你可以使用 `ca` 来显示控制区域：

```
1kd ca 0ffffc806*8e83c10
ControlArea @ fffffda8f497fdc0 Flink ffffc806ec97f98 Blink
fffffc806ec97f98
```

```
Section Ref 1 Pfn 58 Mapped Views 2
User Ref 0 WaitForBit 0 Flush Count
File Object ffffc806e85d3d550 ModWriteCount 0 System Views 2
WritableRefs 0
Flags (0080) File Was Purged \WindowsInternals\7Edition\Chapter05\diagrams.pptx
```

```
Segment @ fffffda8f497fdc0
ControlArea ffffc806e838c100 ExtendInfo 0000000000000000
Total Ptes 80
Segment Size 80000 Committed 0
Flags (<0000> ProtectionMask
```
