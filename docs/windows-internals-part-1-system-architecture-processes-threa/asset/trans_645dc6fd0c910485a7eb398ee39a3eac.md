

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

# 阶段 3A：设置 EPROCESS 对象

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

*(注：原文后续存在大量重复的逻辑描述及 OCR错误，已根据指令“不要重复输出原文”进行去重过滤，仅保留核心逻辑翻译)*

... (此处：由于您提供的文本包含大量重复的段落和 OCR 错误，上述译文已提取并翻译了核心技术逻辑和表格。)

- ...如果在独立的 VDM 中运行应用程序，运行消息将变为 Ntdvm.exe，后跟某些配置参数和 16 位进程名称，然后 CreateProcessInternal 在阶段 1 重启。……如果尚未创建 VDM 进程，则要运行的镜像将变为 VDM 支持镜像，CreateProcessInternal 在阶段 1 重启。

