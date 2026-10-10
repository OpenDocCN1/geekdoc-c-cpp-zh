
Windows 内核的可扩展性随时间不断演进。例如，Windows Server 2003 引入了具有细粒度锁的 CPU 调度队列，允许线程调度决策在多个处理器上并行发生。Windows 7 和 Windows Server 2008 消除了等待调度期间的全局调度器锁。这种锁粒度性的逐步改进也发生在其他领域，例如内存管理器、缓存管理器和对象管理器。

## 客户端版本与服务器版本的区别

Windows 同时提供客户端和服务器零售版包。Windows 10 有六个桌面客户端版本：Windows 10 家庭版、Windows 10 专业版、Windows 10 教育版、Windows 10 专业版教育版以及 Windows 10 企业版长期服务分支 (`LTSB`)。其他非桌面版本包括 Windows 10 移动版、Windows 10 企业版以及 Windows 10 IoT Core、IoT Core 企业版和 IoT Mobile版。还有更多针对具有特定需求的地区的变体，例如 N 系列。

Windows Server 2016 有六个版本：Windows Server 2016 数据中心版、Windows Server 2016 标准版、Windows Server 2016 基础版、Windows Server 2016 MultiPoint Premium Server、Windows Storage Server 2016 以及 Microsoft Hyper-V 2016。

这些版本的区别如下：

- Server 2016 数据中心版和标准版采用基于核心（而非基于插槽）的定价
- 支持的逻辑处理器数量
- 对于服务器系统，允许运行的 Hyper-V 容器数量（客户端系统仅支持基于命名空间的容器）
- 支持的物理内存量（实际上是可用于 RAM 的最高物理地址）；请参第 5 章“内存管理”获取更多关于物理内存限制的信息
- 支持的并发网络连接数（例如，文件和打印服务最多允许 10 个并发连接）
- 支持的多点触和桌面组合
- 支持 BitLocker、VHD 启动、Appocker、Hyper-V 等功能，以及 100 多个其他可配置许可值
- Windows 服务器版具备、而客户端版不具备的分层服务（例如：目录服务、Host Guardian、直接存储空间和集群）

表 2 列出了 Windows 10、Windows Server 2012 R2 和 Windows Server 2016 在内存和处理器支持方面的差异。对于 Windows Server 2012 R2 的详细对比，请参见 https://www.microsoft.com/en-us/download/details.aspx?id=41703。对于 Windows 10 和 2016 及早期版本的内存限制，请参见 https://msdn.microsoft.com/en-us/library/windows/desktop/aa36678.aspx。

尽管 Windows 有多个客户端和服务器零售版包，但它们共享一套核心系统文件，包括内核 `ntoskrnl.exe` 和 PAE 版本 `ntkernel.exe`、HAL 库、设备驱动程序以及基础系统工具和 DLL。

由于不同的 Windows 版本具有相同的内核映像，系统如何识别是哪种版本呢？通过查询 `HKLM\SYSTEM\CurrentControlSet\ProductType` 注册表值来区分是客户端还是服务器（任何变体）。这些值根据许可策略文件加载到注册表中。有效值列于表2-3。可以通过用户态的 `VersionInfo` 函数或使用内核态的 `RtlGetVersion` 和 `RtlVersionInfo` 函数进行查询，这些在 Windows 驱动包 (`WDK`) 中均记录。

### 表 2-2 Windows 版本的处理器和内存限制

| 支持的插槽数 (32 位版) | 支持的物理内存 (32 位版) | 支持的逻辑处理器/插槽数 (64 位版) | 支持的物理内存 (x64 版) |
|---|---|---|---|
| Windows 10 家庭版 | 1 | 4 GB | 1 插槽 | 128 GB |
| Windows 10 专业版 | 2 | 4 GB | 2 插槽 | 2 TB |
| Windows 10 企业版 | 2 | 4 GB | 2 插槽 | 2 TB |
| Windows Server 2012 R2 基础版 | 不可用 | 不可用 | 2 插槽 | 64 GB |
| Windows Server 2016 标准版 | 不可用 | 不可用 | 512 个逻辑处理器 | 24 TB |
| Windows Server 2016 数据中心版 | 不可用 | 不可用 | 512 个逻辑处理器 | 24 TB |

### 表 2-3 ProductType 注册表值

| Windows 版本 | ProductType 值 |
|---|---|
| Windows 客户端 | w1NT |
| Windows 服务器 (域控制器) | LanmanNT |
| Windows 服务器 (仅服务器) | ServerNT |

注册表值 `ProductType` 包含 `tokens.dat` 文件的副本，用于区分 Windows 版本和许可策略启用的功能。如果核心文件对于客户端和服务器版本来说是相同的，它们在运行上又有何区别？简而言之，服务器系统默认针对系统吞吐量进行优化，而客户端版本针对交互式桌面使用的响应时间进行优化。例如，根据产品类型，资源分配决策在启动时取决于操作系统堆（或池）、内部系统工作线程的数量以及系统数据缓存的大小。此外，运行时策略（例如内存管理器权衡系统和进程内存需求）在服务器版和客户端版之间存在不同的默认行为（时间片或量子；见第4章）。如果两个产品存在显著的操作差异，将在书中相关章节突出显示。除非另有说明，书中所有内容适用于客户端和服务器版本。

## 实验：确定许可策略启用的功能

如所述，Windows 支持通过许可机制启用100多种不同的功能。这些策略设置不仅决定了客户端和服务器之间的各种差异，还决定了 Windows 各版本（SKU）之间的差异，例如 BitLocker 支持（Windows 服务器以及 Windows 客户端专业版和企业版可用）。可以使用书中提供的 `SLPolicy` 工具显示许多此类策略值。

策略设置按设施（facility）组织，每个设施代表策略应用所属的模块。你可以通过带有 `-f` 参数运行 `Slpolicy.exe` 来显示工具识别的所有设施列表：

```
C:\SLPolicy.exe -f
Software License Policy Viewer Version 1.0 (C)2016 by Pavel Yosovich
Desktop Windows Manager
Explorer
Fax
Kernel
IIS
```

你可以在开关后添加任何设施名称以显示该设施的策略值。例如，查看 CPU 和可用内存的限制，请使用 Kernel 设施。以下是运行 Windows 10 专业版的机器上预期的输出：

```
C:\SLPolicy.exe -f Kernel
Software License Policy Viewer Version 1.0 (C)2016 by Pavel Yosovich
Kernel
------
Maximum allowed processor sockets: 2
Maximum allowed memory in MB (x86): 4096
Maximum allowed memory in MB (x64): 2097152
Maximum allowed memory in MB (ARM64): 2097152
Maximum physical page in bytes: 4096
Device Family ID: 3
Native VHD boot: Yes
Dynamic Partitioning supported: No
Virtual Partitioning supported: No
Memory Mirroring supported: No
Persist defective memory list: No
```

作为另一个示例，Windows Server 2012 R2 数据中心版的内核 设施输出看起来如下：

```
Kernel
Maximum allowed processor sockets: 6
Maximum allowed memory in MB (x86): 4096
Maximum allowed memory in MB (x64): 4194304
Add physical memory allowed: Yes
Add VM memory allowed: Yes
Maximum physical page in bytes: 0
Native VHD boot: Yes
Dynamic Partitioning supported: Yes
Virtual Partitioning supported: Yes
Memory Mirroring supported: Yes
Persistent device memory list: Yes
```

## 检查版 (Checked build)

Windows 有一种特殊的调试版本称为检查版（外部仅适用于 Windows 8.1 及更早版本，且需要 MSD 订阅）。它是使用 Windows 源代码带有 `DBG` 编译标志进行重新编译的结果，这包含了编译时、调试和跟踪代码。此外，为了便于理解机器码，不会对二进制文件进行以提高执行速度的后期处理（请参见 Windows 调试工具帮助文件中的“调试优化代码”）。

检查版的主要目的是辅助驱动开发人员，因为它对设备驱动程序或系统代码调用的内核态函数执行更严格的检查。例如，如果一个驱动

没有内置工具可以显示你运行的是内核的检查版还是零售版（称为免费版）。然而，此信息可以通过 Windows 管理规范 (WMI) `win32_OperatingSystem` 类的 `Debug` 属性获取。

以下 PowerShell 脚本显示属性。（你可以通过打开 PowerShell 宿主机来尝试。）

```
PS C:\Users\pavely> Get-WmiObject win32_operatingsystem | select debug
debug
-----
False
```

此系统未运行检查生成（checked build），因为显示的 `Debug` 属性为 `False`。

检查生成二进制文件中大量的额外代码是源于 `ASSERT` 和/或 `NT_ASSERT` 宏，这些宏定义在 WDK 头文件 `Wdm.h` 中，并在 WDK 文档中了他的记录。这些宏用于测试条件，例如数据结构或参数的有效性。如果表达式求值为 `FALSE`，宏要么调用内核态函数 `RtAssert`，要么调用 `DbgPrint` 将调试消息文本发送到消息缓冲区，要么发出断言中断（assertion interrupt），该中断在 x64 和 x86 系统上触发中断 0xB。如果挂载了内核调试器并加载了适当的样本，将会自动显示此消息，并提示用户是否怀疑断言失败（断点、忽略、终止进程或终止）。如果系统启动时没有使用内核调试器（使用启动配置数据库中的 debug 选项），且当前没有挂载内核调试器，则断言测试失败将导致系统崩溃（bug-crash）。关于某些内核支持例程执行的断言检查的小列表，请参阅 WDK 文档中的“Checked Built ASSERTs”部分（尽管该列表已不再维护且过时）。

检查生成对于系统管理员也很有用，因为可以为组件启用额外的详细信息跟踪。（有关详细说明，请参阅微软知识库文章编号 31473，标题为“HOWTO：在驱动程序和子系统中启用详细调试”）。此输出通过上述的 `DbgPrintEx` 函数发送到内部调试消息缓冲区。要查看调试消息，你可以在执行本地内核调试时使用 `!dbg` 为目标系统挂载内核调试器（这需要以调试模式启动目标系统），或者使用来自 Sysinternals 的 `DebugView.exe` 工具。然而，最新版本的 Windows 已经放弃了这种类型的调试，而是结合使用 Windows 预处理器 (`WPP`) 跟踪或 TraceLogging 技术，这两种技术都是构建在 Windows 事件跟踪 (`ETW`) 之上的。这些新日志机制的优势在于它们不再局限于组件的检查版本（特别是现在已经无法提供完整的检查生成版本，这非常有用），并且可以使用如 Windows Performance Analyzer (`WPA`, 原名为 `XPerf` 或 Windows Performance Toolkit）、TraceView（来自 WDK）或内核调试器中的 `!wmi print` 扩展等工具查看。

最后，检查生成对于测试用户态代码也很有用，仅因为系统是不同的。（这是因为内核内部发生了额外的检查，并且组件是在没有经过优化的情况下进行编译的）。通常，多线程同步 bug 会缩小到特定的时机条件。通过在运行检查生成的系统（至少是内核和 HAL）上运行你的测试，整个系统时机的不同这一可能会导致潜在的 bug 显现，而这些 bug 在普通的零售系统中是不会发生的。

## 基于虚拟化的安全架构概述

正如你在第 1 章和本章中看到的，用户态和内核态之间的隔离为操作系统免受来自用户态代码（无论是否恶意）的保护。然而，如果一段不受的内核态代码进入系统（通过某些未修补的内核或驱动程序漏洞，或者由于用户被欺骗安装了恶意或有漏洞的驱动程序），系统将完全被破坏，因为所有内核态代码都有访问整个系统的权限。第 1 章中概述的技术利用虚拟机程序提供额外的攻击防护保障，构成了一组基于虚拟化的安全 (`VBS`) 能力，通过引入虚拟信任级别 (`VTLs`) 扩展了处理器的原生基于权限的分离。`VTL` 不仅仅简单地引入了新的正交方式来隔离内存、硬件和处理器资源，还需要新的代码和组件来管理信任级别。运行在 `VTL 0` 中的常规内核和驱动程序不能被允许控制和定义 `VTL 1` 资源；这将会违背初衷。

图 2-3 显示了 VBS 激活时 Windows 10 企业版和 Server 2016 的架构。（你有时会看到安全模式或 `VSM` 的术语。）从 Windows 1607 和 Server 2016 版本开始，如果硬件支持，它始终是默认激活。对于旧版本的 Windows 10，你可以通过策略或“添加功能”对话框（选择“隔离用户模式”）来激活它。

| VTL 0 | VTL 1 |
|---|---|
| 用户模式 | 隔离用户模式 (IUM) |
| 内核模式 | 安全内核 |
| Hyper-V 虚拟机程序 | |
| SLAT | 硬件 | I/O MMU |

图 2-3 Windows 10 和 Server 2016 VBS 架构。

如图 2-3 所示，之前讨论的用户/内核代码运行在 Hyper-V 虚拟机程序之上，就像图 2-1 所示。区别在于，启用 VBS 后，现在存在一个 `VTL` 为 1 的级别，它包含自己的运行在特权处理器模式下（即 x86/x64 ring 0）的安全内核。同样，现在存在一个名为隔离用户模式 (`IUM`) 的运行时用户环境模式，它运行在非特权模式下（即 ring 3）。

在此架构中，安全内核是其自有的二进制执行文件，在磁盘上以 `securekernel.exe` 的名称找到。它既是一个限制普通用户态 DLL 可以调用的允许系统调用的环境（从而限制了可以进行哪些系统调用），也是在 `VTL 1` 下运行的内核环境。这些系统调用通过名为 `secure.dll` 的内部库暴露在内核调试器中（`ntdll.dll` 的 `VTL 1` 版本）以及一个名为 `win32.dll` 的框架中（在 `VTL 1` 下执行）。这些系统调用通过名为 `secure.dll` 的内部库暴露在内核调试器中（`ntdll.dll` 的 `VTL 1` 版本）以及一个名为 `win32.dll` 的框架中（在 `VTL 1` 下执行）。这种实现允许 `VTL 0` 应用程序访问某些内存（我们在第 5 章中将学习更多关于写复制（copy-on-write）机制的知识，防止 `VTL 0` 应用程序更改这些内存。由于利用了 CPU 支持的二级地址翻译 (`SLAT`)，这种机制实际上有效地限制了 `VTL 0` 应用程序访问内存属于 `VTL 1` 的内核态代码。

启用 VBS 后，常规内核规则仍然适用，但通过 `VTL 1` 的考虑进行了增强。换句话之，运行在 `VTL 0` 的内核态代码无法触及 `VTL 1`，因为 `VTL 1` 更高的特权。然而，运行在 `VTL 1` 的用户态代码可以触及 `VTL 0`。实现此点的简单方法如下：权限级别（用户与内核）强制执行权限；而 `VTL` 反之强制执行隔离。尽管 `VTL 1` 用户态应用程序并不比 `VTL 0` 驱动程序强大，但它们被隔离了。事实上，在某些情况下它们的权限更小。由于安全内核没有实现完整的系统调用范围，它会将系统调用转发给 `VTL 0` 内核。（安全内核的另一个名称是代理内核）。任何类型的 I/O、文件、网络和注册表操作都是完全禁止的。例如图形也是如此。

然而，安全内核通过运行在 `VTL 1` 并处于内核态，对 `VTL 0` 的内存和资源具有完全访问权限。它可以利用虚拟机程序限制 `VTL 0` OS 访问某些内存位置。`SLAT` 是 Credentials Guard 技术的基础，该技术可以将密钥存储在这些位置。同样，安全内核可以使用 `SLAT` 拦截并控制内存位置的执行，这是 Device Guard 的关键。

为了防止普通驱动程序利用硬件设备直接访问内存，系统使用了另一种名为 I/O 内存管理单元 (`MMU`) 的硬件，它有效地为设备虚拟化了内存访问。这可以用于防止驱动程序通过直接内存访问 (`DMA`) 直接访问虚拟机程序或安全内核的物理内存区域。这将绕过 `SLAT`，因为不涉及内存。

由于虚拟机程序是引导引导加载程序加载的第一个系统，它可以根据意愿授予 `SLAT` 和 I/O `MMU`，从而定义 `VTL 0` 和 1 的执行环境。然后，在 `VTL 1` 下，加载器运行并加载安全内核，内核可以根据需要进一步配置系统。
