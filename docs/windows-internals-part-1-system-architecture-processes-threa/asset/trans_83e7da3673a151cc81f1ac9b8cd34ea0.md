

# 识别安全进程的实验

安全进程除了通过名称识别外，可以在内核调试器中通过两种方式进行识别。首先，每个安全进程都有一个安全的 PID，它代表该进程在安全内核（Secure Kernel）句柄表中的句柄。普通内核（VTL）在进程中创建线程或请求终止进程时会使用该 PID。其次，线程本身关联有一个线程饼干（thread cookie），它代表它们在安全内核线程表中的索引。

你可以在内核调试器中尝试以下操作：

```
!d>for_each_process .if @@((nt!EPROCESS)$){@Process})->Pcb.SecurePid) {
    !print "Trustlet: %s\n", ((nt!EPROCESS)$){@Process})->ImageFileName,
@Process
}
Trustlet: SecurePid (ffffb9b0d8c79080)
Trustlet: Lsa.exe (ffffb9b09e2ba9640)
Trustlet: Biso.exe (ffffb9b09e6c16460)
!d> nt_EPROCESS ffffb9b0d8c79080 Pcb.SecurePid
+0x00 Pcb
  +0x2d SecurePid : 0000000140000004
!d> nt_EPROCESS ffffb9b09e2ba9640 Pcb.SecurePid
+0x00 Pcb
  +0x2d SecurePid : 0000000140000030
!d> nt_EPROCESS ffffb9b09e6c16460 Pcb.SecurePid
+0x00 Pcb
  +0x2d SecurePid : 0000000140000080
!d> process ffffb9b09e2ba9640 4
SessionId: 0 Cid: 0338 Peb: 63cdc62b000 ParentId: 0328
DirBase: 2f25400 ObjectTable: fffc07b5b91040 HandleCount: 44.\Image: Lsa.exe
THREAD ffffb9b09e2ba2080 Cid 0338. Teb: 0000000cdc62c200 Win32Thread:
0000000000000000 WAIT
!d> nt_THREAD ffffb9b09e2ba2080 Tcb.SecureCookie
+0x00 Tcb
  +0x31c SecureCookie : 9
```

# CreateProcess 的流程

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

# 表 3-7 进程属性

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

