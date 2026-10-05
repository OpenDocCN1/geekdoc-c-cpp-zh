

1kd> dd /c 1MiSystemVaCountPeak L f

从理论上讲，如果有足够的虚拟地址空间，分配给组件的不同虚拟地址范围的大小可以任意增长。在实践中，在 32 位系统上，为了可靠性和稳定性，内核分配器对每种虚拟地址类型实施了限制。（在 64 位系统上，内核地址空间耗尽目前不是一个需要担心的问题。）尽管默认实施了这些限制，但系统管理员可以使用注册表来修改当前标记为受限的虚拟地址类型的这些限制（见表 5-8）。

如果对 `MiInSystemVa` 的当前请求超过了可用限制，则会发生失败（参见上一个实验），并且无论可用内存如何，都会请求回收操作。这应该有助于缓解内存负载，并允许在下次尝试时虚拟地址分配正常工作。然而，请记住，回收会影响系统缓存和非分页缓冲池。

# 实验：设置系统虚拟地址限制

`MiSystemVaCountL1` 包含了系统虚拟地址使用的限制，可以为每种类型设置限制。目前，管理器仅允许某些虚拟地址类型受到限制，并提供了运行时为系统动态使用未公开系统的能力。（这些限制也可以通过注册表设置，详见 http://msdn.microsoft.com/en-us/library/bb870880.aspx。）这些限制可以设置在表 5-8 标记的类型上。

你可以在 32 位系统上使用 `MemLimit` 实用（在本书的可下载资源中找到）来查询和设置这些类型的不同限制，并查看当前和峰值的虚拟地址空间使用情况。以下是如何使用 `-q` 标志查询当前值：

```
C:\Tools\MemLimit.exe -q
```

MemLimit v1.01 - 查询并设置系统 VA 空间消耗的硬限制
Copyright (C) 2008-2016 by Alex Ionescu
www.alex-ionescu.com

系统 VA 消耗：

| 类型 | 当前 | 峰值 | 限制 |
| --- | --- | --- | --- |
| 非分页池 (Non Paged Pool) | 45056 KB | 55296 KB | 0 KB |
| 分页池 (Paged Pool) | 151552 KB | 165888 KB | 0 KB |
| 系统缓存 (System Cache) | 44664 KB | 47923 KB | 0 KB |
| 系统 PTE (System PTEs) | 90112 KB | 135168 KB | 0 KB |
| 会话空间 (Session Space) | 63488 KB | 73728 KB | 0 KB |

作为一个实验，使用以下命令为分页池设置 100 MB 的限制：
memlimit.exe -p 100M

现在使用 Sysinternals 的 `TestLimit` 创建尽可能多的句柄。通常情况下，在足够的分页池的情况下，句柄数量应该是 1600 万左右。但在 100 MB 的限制下，结果为：

```
C:\Sysinternals\Testlimit.exe -h
```

Testlimit v5.24 - 测试 Windows 限制
Copyright (C) 2012-2015 Mark Russinovich
Sysinternals - www.sysinternals.com

进程 ID: 4780

创建句柄...
已创建 10727844 个句柄。最后错误: 1450

关于对象、句柄和分页池消耗的更多信息，请参见部分 2 第 8 章。

# 系统虚拟地址空间配额

上一节描述的系统虚拟地址限制允许限制内核组件的系统级虚拟地址空间使用。然而，当将其应用于整个系统时，它们仅在 32 位系统上有效。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。

作为一个实验，使用以下命令为分页池设置 100 MB 的限制：
memlimit.exe -p 100M

现在使用 Sysinternals 的 `TestLimit` 创建尽可能多的句柄。通常情况下，在足够的分页池的情况下，句柄数量应该是 1600 万左右。但在 100 MB 的限制下，结果为：

```
C:\Sysinternals\Testlimit.exe -h
```

Testlimit v5.24 - 测试 Windows 限制
Copyright (C) 2012-2015 Mark Russinovich
Sysinternals - www.sysinternals.com

进程 ID: 4780

创建句柄...
已创建 10727844 个句柄。最后错误: 1450

关于对象、句柄和分页池消耗的更多信息，请参见部分 2 第 8 章。

# 系统虚拟地址空间配额

上一节描述的系统虚拟地址限制允许限制内核组件的系统级虚拟地址空间使用。然而，当将其应用于整个系统时，它们仅在 32 位系统上有效。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。你可以在 `HKLM\System\CurrentControlSet\Control\Session Manager` 键下配置 `PagedPoolQuota`、`NonPagedPoolQuota`、`PagingFileQuota` 和 `WorkingSetPages` 值。为了解决系统管理员可能有的特定配额需求，内存管理器与进程管理器协作执行系统级或用户特定的配额。

（注：此处原文中存在大量重复段落，已按要求完成翻译并保持逻辑）

## 用户地址空间布局

正如内核中的地址空间一样，用户地址空间也是动态构建的。线程栈、进程堆以及加载的镜像（如 DLL）的地址（如果应用程序和镜像支持）通过 ASLR 机制动态计算。除了这些区域（以及某些系统结构如 TEB 和 BEB）之外，其他内存分配都是运行时相关的，结合 DEP 使得攻击更难以实现。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_382_0.png)

图 5-14 启用 ASLR 的用户地址空间布局。

# 实验：分析用户地址空间

Sysinternals 的 VMMap 实用工具可以显示你机器上任何进程使用的虚拟内存详细视图。这些信息按内存分配类型分类，总结如下：

- 镜像 (Image)：显示映射执行文件及其依赖项（如动态库）以及任何其他内存映射映像（可执行文件）的内存分配。
- 映射文件 (Mapped File)：显示映射数据文件的内存分配。
- 可共享 (Shareable)：显示标记为可共享的内存分配，通常包括共享内存（但不映射文件，后者位于 Image 或 Mapped File 下）。
- 堆 (Heap)：显示此进程拥有的堆内存分配。
- 托管堆 (Managed Heap)：显示由 .NET CLR 分配的内存。对于未使用 .NET 的进程，它不会显示任何内容。
- 栈 (Stack)：显示此进程中每个线程栈分配的内存。
- 私有数据 (Private Data)：显示除栈和堆之外标记为私有的内存分配，例如内部数据结构。

