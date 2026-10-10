
## CreateProcess 的流程

我们已经看到了进程状态管理中的各种数据结构，以及各种工具和调试器如何检查这些信息。在本节中，我们将看到这些数据结构是如何以及何时被创建并填充的，以及进程背的创建和终止行为。正如我们所看到的，所有文档记录的进程创建函数最终都会调用 `CreateProcessInternal`，这就是我们将

创建一个进程由操作系统三个部分执行的几个阶段组成：Windows 客户端库 `Kernel32.dll`（执行 `CreateProcessInternal` 的实际工作）、Windows 执行体（Windows executive）以及 Windows 子系统进程（Csrss）。由于 Windows 的多环境子系统架构，创建一个可执行进程（其他子系统可以使用）与创建一个 Windows 子系统进程的工作是分开的。因此，尽管对 Windows `CreateProcess` 函数流程的描述很复杂，但那部分工作特定于 Windows 子系统处理的语义，而不是创建执行体对象所需的的核心工作。

以下列表总结了使用 Windows `CreateProcess` 函数创建进程的主要阶段。每个阶段执行的操作将在后续章节中详细说明。

> 注意：CreateProcess 的许多步骤与进程虚拟地址的设置有关，因此引用了第 5 章中定义的内存管理术语和结构。

- 1. 验证参数；将 Windows 子系统标志和选项转换为其原生计数器；解析、验证并转换属性列表（attribute list）为其原生对应项。
- 2. 打开要在进程内执行的映像文件 (.exe)。
- 3. 创建 Windows 执行体进程对象。
- 4. 创建初始线程（栈、上下文和 Windows 执行体线程对象）。
- 5. 执行创建后的 Windows 子系统特定的进程初始化。
- 6. 启动初始线程的执行（除非指定了 `CREATE_SUSPENDED` 标志）。
- 7. 在新进程和线程的上下文中，完成地址空间的初始化（例如加载 DLLs）并开始执行程序的入口点。

图 3-10 显示了 Windows 创建进程所遵循的阶段概述。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_146_0.png)

图 3-10 进程创建的主要阶段。

# 阶段 1：转换和验证参数及标志

在打开可执行文件运行之前，`CreateProcessInternal` 执行以下步骤：

- 1. 新进程的优先级类作为 `CreateProcess` 函数的 `CreationFlags` 参数中的独立位指定。因此，你可以为单个 `CreateProcess*` 指定多个优先级类，通过选择设置的最低优先级类来解决为进程分配哪个优先级类的问题。

定义了六种进程优先级类，每个值都映射到一个数字：

- 空闲或低级 (Idle or Low)，如任务管理器所示 (4)
- 低于正常 (Below Normal) (6)
- 正常 (Normal) (8)
- 高于正常 (Above Normal) (10)
- 高 (High) (13)
- 实时 (Real-time) (24)

优先级类被用作进程中创建的线程的基础优先级。此值不直接影响进程本身——只影响其内部的线程。进程优先级类及其对线程调度的影响描述出现在第 4 章。

- 2. 如果没有为新进程指定优先级类，则优先级类默认为正常（Normal）。如果为新进程指定实时优先级类，且调用者没有“增加调度优先级”特权（SE_INC_BASE_PRIORITY_NAME），则改为使用高（High）类。换句话说，进程创建不会因为调用者没有足够的权限在实时优先级下创建进程而失败；新进程的优先级不会像实时那么高。

- 3. 如果创建标志指定进程将被调试，`Kernel32` 将通过 `DbgConnectDebug` 发起到 `Ntdll.dll` 中原生调试代码的连接，并从当前线程的环境块（TEB）获取调试句柄。

- 4. 如果创建标志指定了，`Kernel32.dll` 将设置默认的硬错误模式（hard error mode）。

- 5. 用户指定的属性列表从 Windows 子系统格式转换为普通格式，并向其添加内部属性。可以添加到属性列表的可能属性如表 3-7 所示，包括它们记录的 Windows API 对应项（如果有）。

> 注意：传递给 `CreateProcess*` 的属性列表允许调用者访问诸如初始线程的 TEB 这样的信息。

## 表 3-7 进程属性

| 原生属性 | 等效 Win32 属性 | 类型 | 描述 |
| :--- | :--- | :--- | :--- |
| PS_CP_PARENT_PROCESS | PROC_THREAD_ATTRIBUTE_PARENT_PROCESS | 输入 | 父进程句柄。 |
| PS_CP_DEBUG_OBJECT | N/A. 使用 DEBUG_PROCESS 时 | 输入 | 调试对象。 |
| PS_CP_PRIMARY_TOKEN | N/A. 使用 CreateProcessAsUser | 输入 | 使用了令牌的进程。 |
| PS_CP_CLIENT_ID | 返回的 PROCESS_INFORMATION | 输出 | 返回 TID 和 PID。 |
| PS_CP_TEB_ADDRESS | N/A. 内部使用 | 输出 | 初始线程的地址。 |
| PS_CP_FILENAME | CreateProcess API 中的参数 | 输入 | 要创建的进程名称。 |
| PS_CP_IMAGE_INFO | N/A. 内部使用 | 输出 | RETURNS_SECTION_INFORMATION，包含版本、标志和子系统，以及栈大小和入口点。 |
| PS_CP_MEM_RESERVE | N/A. 由 SMSS 和 CSRSS 使用 | 输入 | 在进程创建期间应进行的虚拟内存保留，因为还没有其他分配。 |
| PS_CP_PRIORITY_CLASS | N/A. 作为 CreateProcess API 的参数传递 | 输入 | 给进程的优先级类。 |
| PS_CP_ERROR_MODE | N/A. 通过 CREATE_DEFAULT_ERROR_MODE 标志传递 | 输入 | 进程的硬错误处理模式。 |
| PS_CP_STD_HANDLE_INFO | N/A. 内部无 | 输入 | 指定哪些标准句柄应该复制或创建。 |
| PS_CP_HANDLE_LIST | PROC_THREAD_ATTRIBUTE_HANDLE_LIST | 输入 | 父进程中继承的句柄列表。 |
| PS_CP_GROUP_AFFINITY | PROC_THREAD_ATTRIBUTE_GROUP_AFFINITY | 输入 | 允许线程运行的处理器组。 |
| PS_CP_PREFERRED_NODE | PROC_THREAD_ATTRIBUTE_PREFERRED_NODE | 输入 | 与进程关联的首选（理想）NUMA 节点。它影响创建初始进程堆和线程栈的节点（第 5 章）。 |
| PS_CP_IDEAL_PROCESSOR | PROC_THREAD_ATATTRIBUTE_IDEAL_PROCESSOR | 输入 | 线程应该被调度到哪个理想处理器。 |
| PS_CP_UMS_THREAD | PROC_THREAD_ATTRIBUTE_UMS_THREAD | 输入 | 包含 UMS 属性、完成列表和上下文。 |

| PS_CP_MITIGATION_OPTIONS | PROC_THREAD_MITIGATION_POLICY | 输入 | 说明 |
| :--- | :--- | :--- | :--- |
| PS_CP_MITIGATION_OPTIONS | | | 包含关于进程应启用或禁用的缓解措施（SEHOP、ATL 模拟、NX）的信息。 |
| PS_CP_PROTECTION_LEVEL | PROC_THREAD_ATTRIBUTE_PROTECTION_LEVEL | 输入 | 必须是表 3-1 中允许的进程保护值之一，或者是与父进程相同的 `PROTECT_LEVEL_SAME` 值。 |
| PS_CP_SECURE_PROCESS | 无。内部使用。 | 输入 | 表示进程是否应作为隔离用户模式 (IUM) 信任运行。更多细节请参阅第 2 部分第 8 章。 |
| PS_CP_JOB_LIST | 无。内部使用。 | 输入 | 将进程分配到作业列表中。 |
| PS_CP_CHILD_PROCESS_POLICY | PROC_THREAD_ATTRIBUTE_CHILD_PROCESS_POLICY | 输入 | 指定新进程是否允许创建子进程，无论是直接还是间接（例如通过使用 WMI）。 |
| PS_CP_ALL_APPLICATION_PACKAGES_POLICY | PROC_THREAD_ATTRIBUTE_ALL_APPLICATION_PACKAGES_POLICY | 输入 | 指定 AppContainer 令牌是否排除在包含 ALL APPLICATION 组的 ACL 检查之外。将而使用 ALL RESTRICTED APPLICATION PACKAGES 组。 |
| PS_CP_WIN32K_FILTER | PROC_THREAD_ATTRIBUTE_WIN32K_FILTER | 输入 | 表示进程的任何 GDI/USER 系统调用是否会被过滤（拦截），或者它们是否会被审计。通过使用 Microsoft Edge 浏览器来减少攻击面。 |
| PS_CP_SAFE_OPEN_PROMPT_ORIGIN_CLAIM | 无。内部使用。 | 输入 | 用于标记标记（Mark of Web）功能，以识别来自不可信源的文件。 |
| PS_CP_BNO_ISOLATION | PROC_THREAD_ATTRIBUTE_BNO_ISOLATION | 输入 | 使进程与一个隔离的 BaseNamedObjects 目录关联（有关命名对象的更多信息，请参阅第 2 部分第 8 章）。 |
| PS_CP_DESKTOP_APP_POLICY | PROC_THREAD_ATTRIBUTE_DESKTOP_APP_POLICY | 输入 | 表示现代应用是否允许启动旧版桌面应用程序，如果是，以什么方式启动。 |
| 无——内部使用 | PROC_THREAD_ATTRIBUTE_SECURITY_CAPABILITIES | 输入 | 指定指向 `SECURITY_CAPABILITIES` 结构的指针，用于在调用 `NtCreateUserProcess` 之前为进程创建 AppContainer 令牌。 |

6. 如果进程是作业对象（job object）的一部分，则请求虚拟桌面机 (VDM) 的进程标志将被忽略。

7. 传递 `CreateProcess` 函数的进程和初始线程的安全属性会被转换为它们的内部表示（`OBJECT_ATTRIBUTES` 结构，记录在 WDK 中）。

8. `CreateProcessInternal` 检查进程是否应以现代方式创建。如果通过属性（`PROC_THREAD_ATTRIBUTE_PACKAGE_FULL_NAME`）指定了完整包名，或者创建者本身是现代的（且没有通过 `PROC_THREAD_ATTRIBUTE_PARENT_PROCESS` 属性显式指定父进程），则进程将以现代方式创建。如果是这样，将调用内部 `BaseAppExtension` 以通过一个名为 `APX_PROCESS_CONTEXT` 的结构收集有关该现代应用的更多上下文信息。此上下文持有诸如包名（内部称为 package moniker）、与应用相关的权限、进程的当前目录以及该应用是否应具有完全信任等信息。创建完全信任现代应用的选项并未公开，而是为具有现代外观和体验且需要执行操作的应用程序保留的。一个典型的例子是 Windows 10 中的设置应用 (SystemSettings.exe)。

9. 如果要创建现代进程，安全能力（由 `PROC_THREAD_ATTRIBUTE_CAPABILITIES` 提供）将由内部 `BaseCreatebox` 函数记录，用于初始令牌的创建。`LowBox` 术语指的是执行进程所属的沙箱（AppContainer）。请注意，虽然不支持通过直接调用 `CreateProcess` 创建现代进程（而应使用此处描述的 COM 接口），但 Windows SDK 和 MSDN 提供了通过传递此属性创建 AppContainer 遗留应用程序的能力。

10. 如果要创建一个现代进程，则向内核设置标志以跳过清单检测。现代进程绝不应该嵌入式清单（manifest），因为这根本不需要。（现代应用有它自己的清单，与此处引用的嵌入式清单无关。）

11. 如果指定了调试标志（`DEBUG_PROCESS`），则可执行文件在映像文件执行选项键（在下一节讨论）下的调试器值将被标记为跳过。否则，调试器将永远无法创建其调试器进程，因为创建过程将进入无限循环（反复尝试创建调试器进程）。

12. 所有窗口都与桌面（工作区的图形化表示）相关。如果 `STARTUPINFO` 结构中未指定桌面，则进程将与调用者的当前桌面关联。

> 注意：Windows 10 的虚拟桌面功能不使用多个桌面对象（内核对象中）。仍然只有一个桌面，但根据需要显示和隐藏窗口。这与 Sysinternals 的 `desktops.exe` 工具形成对比，后者实际上创建了多四个桌面对象。在将窗口从一个桌面移动到另一个桌面时可以感觉到这种差异。在 `desktops.exe` 的情况下，无法这样做，因为 Windows 不支持此类操作。相反，Windows 10 的虚拟桌面允许这样做，因为没有这种限制。

## 表 3-8 CreateProcess 第一1阶段的决策树

| 如果镜像... | 创建状态代码 | 此镜像将运行... | 以及将发生的情况 |
|---|---|---|---|
| 是具有 .exe、.com 或 .pif 扩展的 MS-DOS 程序 | PsCreateFailOnSectionCreate | Ntvdm.exe | CreateProcessInternal 重启阶段 1。 |
| 是 Win16 应用程序 | PsCreateFailOnSectionCreate | Ntvdm.exe | CreateProcessInternal 重启阶段 1。 |
| 在 32 位系统上的 Win64 程序（或 PPC、MIPS 或 Alpha 二进制文件） | PsCreateFailMismatch | N/A | CreateProcess 将失败。 |
| 具有另一个名称的调试 值 | PsCreateFailName | Debug 值中指定的名称 | CreateProcessInternal 重启阶段 1。 |
| 是无效或损坏的 Windows 扩展名 | PsCreateFailExeFormat | N/A | CreateProcess 将失败。 |
| 无法打开 | PsCreateFailOnFileOpen | N/A | CreateProcess 将失败。 |
| 是具有 .bat 或 .cmd 扩展的命令过程 | PsCreateFailOnSectionCreate | Cmd.exe | CreateProcessInternal 重启阶段 1。 |

具体而言，CreateProcessInternal 遍历镜像的决策树如下：

- 如果是 x86 32 位 Windows，且镜像是具有 .exe、.com 或 .pif 扩展的 MS-DOS 程序，则会向 Windows 子系统发送消息，检查是否已为此会话创建了 MS-DOS 支持端口（在 HKLM\SYSTEM\CurrentControlSet\Control\WOW\registry 值中指定的 Ntvdm.exe）。如果已创建了支持进程，则使用其来运行虚拟 DOS 机器（VDM）进程以运行新镜像。然后 CreateProcessInternal 重启。如果尚未创建支持进程，则镜像将作为 Ntvdm.exe 运行，且 CreateProcessInternal 重启。
- 如果文件运行 .bat 或 .cmd 扩展名，则要运行的镜像将变为 Cmd.exe（Windows 命令行提示符），CreateProcessInternal 在阶段 1 重启。（批处理文件名将在 / 关后作为第二个参数传递给 Cmd.exe）。
- 对于 x86 Windows 系统，如果镜像是 Win16（Windows 3.1）可执行文件，CreateProcessInternal 必须决定是创建一个新的 VDM 进程来运行，还是使用默认的会话级 VDM 进程（该进程可能尚未创建）。CreateProcess  CREATE_SEPARATE_wOW_VDM 和 CREATE_SHARED_wOW_VDM 控制此决策。如果未设置这些标志，则由 HKLM\SYSTEM\CurrentControlSet\Control\WOW\DefaultSeparateVDM 值决定此行为。如果在独立的 VDM 中运行应用程序，运行消息将变为 Ntdvm.exe，后跟某些配置参数和 16 位进程名称，然后 CreateProcessInternal 在阶段 1 重启。否则，Windows 子系统将发送消息检查共享 VDM 进程是否存在并可以可以使用。（如果 VDM 运行在不同的桌面上，或未在与调用者相同的安全级别下运行，则无法使用，必须创建一个新的 VDM 进程。）如果使用了共享 VDM 进程，Windows 子系统将向其发送消息以运行新镜像，CreateProcess 返回。如果尚未创建 VDM 进程（或无法使用），则要运行的镜像将变为 VDM 支持镜像，CreateProcessInternal 在阶段 1 重启。

# 阶段 3：创建 Windows 内核进程对象

此时，NtCreateProcess 已经打开了一个有效的可执行文件并创建了一个对象将其映射到新的进程地址空间。接下来，它通过调用内部系统函数 PspAllocateProcess 创建一个 Windows 内核进程对象。创建内核进程对象（由创建它的线程完成）涉及以下子阶段：

- **3A.** 设置 EPROCESS 对象
- **3B.** 创建初始进程地址空间
- **3C.** 初始化内核进程结构 (KPROCESS)
- **3D.** 完成进程地址空间的设置
- **3E.** 设置 PEB
- **3F.** 完成内核进程对象的设置

> 注意： 只有在系统初始化期间（当创建 System 进程时）才不会有父进程。从该时间点之后，始终需要一个父进程为新进程提供安全上下文。

## 阶段 3A：设置 EPROCESS 对象

此子阶段涉及以下步骤：

- 1. 继承父进程的亲和性，除非在进程创建期间（通过属性列表）显式设置过。
- 2. 如果属性列表中指定了，则选择属性列表中指定的理想 NUMA 节点。
- 3. 继承父进程的 I/O 和页优先级。如果没有父进程，则使用默认页优先级 (S) 和 I/O 优先级 (Normal)。
- 4. 将新进程的退出状态设置为 STATUS_PENDING。
- 5. 选择由属性列表选定的硬错误处理模式。如果没有提供，则继承父进程的处理模式。如果不存在父进程，则使用默认处理模式，即显示所有错误。
- 6. 将父进程的 ID 存储在新进程对象的 InheritedFromUniqueProcessID 字段中。
- 7. 查询镜像执行选项 (IEO) 键值，以检查进程是否应使用大页映射（IEO 键中的 UseLargePages 值），除非进程在 Wow64 下运行，在这种情况下不使用大页。还查询该键检查 NTDLL 是否已列为在该进程内应使用大页映射的 DLL。
- 8. 查询 IEO 中的性能选项键（PerfOptions，如果存在），它可能包含以下任何值：IoPriority、PagePriority、CpuPriorityClass 和 WorkingLimitKB。
- 9. 如果进程将在 Wow64 下运行，则分配 Wow64 辅助结构 (WOW64) 并将其设置在 EPROCESS 成员中。
- 10. 如果进程在 AppContainer 内创建（绝大多数情况下为 LowBox），则验证为 LowBox 创建的令牌。
- 11. 尝试获取创建进程的所有权限。选择实时进程类、为新进程分配令牌、使用大页映射进程以及在新会话中创建进程，这些操作都需要适当的权限。

## 阶段 3C：创建内核进程结构

`PspAllocateProcess` 的下一个阶段是初始化 `KPROCESS` 结构（即 `EPROCESS` 中的 `Pcb` 成员）。这项工作由 `KeInitializeProcess` 完成，它执行了以下操作：

- 1. 初始化连接进程所有部分的双向链表（初始为空）。
- 2. 将进程默认量子时间片（在“线程调度”部分中有更详细描述）的初始值（或重置值）硬编码为 6，直到后续由 `(PspQuantumAndPriority)` 初始化。
- 3. 根据阶段 3A 阶段计算的结果设置进程的基础优先级。
- 4. 设置进程中线程的默认处理器亲和力，同样设置了组亲和力。组亲和力是在阶段 3A 阶段计算的或从父进程继承的。
- 5. 将进程交换状态设置为驻留（resident）。
- 6. 线程种子基于内核为此进程选择的理想处理器（这基于之前创建的进程的理想处理器，实际上是按轮询方式对其进行修改）。创建新进程将更新 `KeNodeBlock` 中的种子，以便新进程能够获得不同的理想处理器种子。
- 7. 如果该进程是安全进程（Windows 10 和 Server 2016），则现在通过调用 `HvCreateSecureProcess` 创建其安全 ID。

## 阶段 3D：完成进程地址空间的设置

为新进程设置地址空间相当复杂，让我们一步步查看涉及的内容。为了充分利用本节内容，你应该熟悉第 5 章描述的 Windows 内存管理器区间。

负责设置地址空间大部分工作的例程是 `MmInitializeProcess-AddressSpace`。它还支持从另一个进程克隆地址空间。这种能力在实现 POSIX `fork` 系统调用时非常有用。未来可能还会被用于支持 Unix 风格的 `fork`（这是 Redstone 1 中 Windows 子系统 for Linux 实现 fork 的方式）。以下步骤没有描述地址空间功能，而是关注于正常的进程地址初始化。

- 1. 虚拟内存管理器将进程的最后修剪（last trim）值设置为当前时间。工作管理器（在平衡集管理器线程的上下文中运行）使用此值来决定何时启动集合修剪。
- 2. 内存管理器初始化进程的工作集列表。现在可以处理页错误了。
- 3. 节（在打开映像文件时创建）现在映射到新进程的地址空间中，并将进程节基设置为映像的基地址。
- 4. 创建并初始化进程环境块（PEB）（见阶段 3E 节）。
- 5. 将 `Ntdll.dll` 映射到进程中。如果这是一个 Wow64 进程，也会映射 32 位的 `Ntdll.dll`。
- 6. 如果请求，则为进程创建一个新会话。这个特殊步骤仅是为了会话管理器（Smss）在初始化新会话时的便利。
- 7. 设置进程的默认句柄，同样设置组亲和力。

## 阶段 3E：设置 PEB

`NtCreateProcess` 调用 `MiCreatePeb`，将系统级语言支持（NLS）表映射到进程地址空间。它为 PEB 分配一个页面并初始化许多字段，这些字段是通过注册表配置的。某些字段可以被映像头中的设置覆盖。

如果映像头部特征设置了 `IMAGE_FILE_SYS_ONLY` 标志（指示映像只能在单处理器系统上运行，将为所有线程选择一个 `CmpRtlProcessorNumber`）。选择过程通过简单循环可用处理器完成。每次运行这种类型的映像时，都会使用下一个处理器。

## 阶段 3F：完成执行对象的设置

在返回进程句柄之前，必须完成一些设置步骤，这些步骤由 `PsInsertProcess` 及其辅助函数完成：

- 如果启用了系统级进程审核（由于本地策略设置或域控制器组策略），将进程创建写入安全日志。
- 如果父进程包含作业，则从父进程级别恢复作业并绑定到新创建进程的会话。最后，将新进程加入作业。
- 将新进程插入到 Windows 活动进程列表（`PsActiveProcessHead`）的末尾。现在可以通过 `EnumProcesses` 和 `OpenProcess` 等函数访问该进程。
- 将父进程的调试标志复制到新进程，除非设置了 `NoDebugFlag`（创建进程时请求）。如果指定了调试端口，则将其附加到新进程。

# 第 4 阶段：创建初始线程及其栈和上下文

此时，Windows 内内核进程对象已完全建立。然而，它还没有线程，因此目前还无法执行任何操作。现在是开始这项工作了。通常情况下，`PspThread` 例程负责线程创建的所有方面，并在创建新线程时由 `NtCreateThread` 调用。然而，由于初始线程是由内核通过用户态输入内部创建的，`PspThread` 依赖的两个辅助函数变为：`PspAllocateThread` 和 `PspInsertThread`。`PspAllocateThread` 处理内核对象本身的实际创建和初始化，而 `PspInsertThread` 则处理线程和安全属性的创建，并调用 `KeStartThread` 将内核对象转换为系统中可调度的线程。尽管如此，线程还不会做任何事情。它是以挂起状态创建的，直到进程完全初始化（如第 4 阶段）后才会被恢复。

`PspAllocateThread` 执行以下步骤：

- 1. 防止在 Wow64 进程中创建用户态调度（UMS）线程，并防止用户态调用者在系统进程中创建线程。
- 2. 创建并初始化内核线程对象。
- 3. 如果系统启用了能量估计（XBOX 始终禁用），则为内核对象中分配并初始化一个 `Thread_ENERGY_VALUE` 结构。
- 4. 初始化 LPC、I/O 管理和内核使用的各种列表。
- 5. 设置线程创建时间，并创建其线程 ID (TID)。
- 6. 在线程执行之前，它需要一个栈和一个运行所需的上下文，因此会设置这些内容。初始线程的栈大小从镜像中获取；无法指定其他大小。如果是 Wow64 进程，还将初始化 Wow64 线程上下文。
- 7. 为新线程分配线程环境块 (TEB)。
- 8. 将用户态线程起始地址存储在 `THREAD`（在 `StartAddress` 字段）中。这是 `Ntdll.dll` 中系统提供的线程启动函数（`LtlUserStart`）。用户的 Windows 起始地址存储在 `THREAD` 的另一个位置（`Win32StartAddress` 字段），以便像 Process Explorer 这样的调试工具显示这些信息。
- 9. 调用 `KeInitThread` 设置 `KTHREAD` 结构。初始线程的当前优先级设置为进程优先级，其亲和性设置为进程亲和性。`KeInitThread` 随后为线程分配内核栈，并初始化线程的机器硬件上下文，包括上下文、陷阱和异常帧。
- 设置线程上下文，以便线程将在 `KiThreadStartup` 中以内核模式启动。最后，`KeInitThread` 将线程状态设置为 `Initialized`（已初始化）并返回到 `PspAllocateThread`。

# 第 5 阶段：执行 Windows 子系统特定的初始化

一旦 `CreateUserProcess` 返回成功代码，必要的内核进程和线程对象已经创建。`CreateProcessInternal` 执行与 Windows 子系统特定操作相关的各种操作以完成进程初始化。

- 检查 Windows 是否允许运行可执行文件。这些检查包括验证头中的镜像版本，并检查 Windows 是否通过组策略阻止了该进程。
- 如果适用限制策略，将为新进程创建一个受限令牌。之后，查询应用程序兼容性数据库以查看注册表或系统应用程序数据库中是否存在该进程的项。此时不会应用兼容性 shim；信息将存储在初始线程开始执行的 PEB 中（第 6 阶段）。

# 第 6 阶段：启动初始线程的执行

此时，进程环境已经确定，线程资源已分配，进程已拥有一个线程，并且 Windows 子系统已获知新进程。除非调用者指定了 `CREATE_SUSPENDED` 标志，否则初始线程现在将恢复，以便它可以开始并在新进程上下文中执行剩余的进程初始化工作（第 7 阶段）。

# 第 7 阶段：在新进程上下文中执行进程初始化

新线程开始运行内核态线程例程 KiStartThread。KiStartThread 将 IRQL 从延迟过程调用 (DPC) 降低到 APC 级别，然后调用系统初始线程例程 PspUserThreadStartup。将用户指定的线程起始地址作为参数传递给此例程。PspUserThreadStartup 执行以下操作：

- 它在 x86 架构上安装异常链。
- 它将 IRQL 降低到 PASSIVE_LEVEL（这是用户代码允许运行的唯一 IRQL）。
- 它禁用运行时交换进程上下文的能力。
- 如果线程在启动时被杀死（无论出于什么原因），将被终止且不再采取后续操作。
- 它根据内核态数据结构中的信息在 TEB 中设置区域设置 ID 和理想处理器，然后检查线程创建是否真的失败。
- 它调用 DbgCreateThread，该函数会检查是否向新进程发送了通知。

# 终止进程

进程可以通过调用 `ExitProcess` 函数优雅地退出。对于许多进程来说——第一个线程的启动代码在从其主函数返回时会代表该进程调用 `ExitProcess`。*优雅*一词意味着加载到进程中的 DLL有机会执行工作，其方法是通过调用它们的 `DMain` 函数并传递 `DLL_PROCESS_DETACH` 来通知进程正在退出。

`ExitProcess` 只能由进程本身请求退出时被调用。使用 `TerminateProcess` 函数可以对进程进行非优雅终止，该函数可以从进程外部调用。

## 映像加载器

我们刚刚看到，当系统启动启动进程时，内核创建一个对象来表示它并执行各种内核相关的初始化任务。然而，这些任务并没有导致应用程序的执行，仅仅是准备它的上下文和环境。事实上，与内核态代码驱动程序不同，应用程序在用户态下执行。大部分实际初始化工作是在内核之外完成的。这项工作由*映像加载器*（image loader）执行，内部称为 `Ldr`。

映像加载器位于用户态系统库 *Ntdll.dll* 中，而不是内核库中。因此，它的行为就像是作为 DLL 一部分的标准代码，并受到内存访问和安全权限的限制。

## 实验：观察映像加载器

在实验中，我们使用全局标志启用一项名为加载器快照（loader snaps）的调试功能。这允许你通过启动调试对加载器输出进行调试。

1. 从安装 WinDbg 的目录启动 Gflags ，然后点击 Image File 选项卡。
2. 在 Image 字段中输入 Notepad.exe，然后按 Tab 键。这应该启用各种选项。选择 Loader Snaps 选项，然后点击 OK 或 Apply。
3. 现在启动 WinDbg，选择 File 菜单，选择 Open Executable，导航到 c:\windows\system32\notepad.exe 并启动它。你应该在这里看到几屏幕调试信息：
