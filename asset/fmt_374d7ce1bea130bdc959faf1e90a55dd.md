
`1kd> dt nt!epro`

```
+0000 Pcb : _KPROCESS
+02d8 ProcessLock : _EX_PUSH_LOCK
+02e0 RundProcess : _EX_RUNDOWN_REF
+02e8 UniqueProcessId : Ptr64 Void
+02f0 ActiveProcessLinks : _LIST_ENTRY
+03a8 Win32Process : Ptr64 Void
+03b0 Job : Ptr64 _EJOB
+0418 ObjectTable : Ptr64 _HANDLE_TABLE
+0420 DebugPort : Ptr64 Void
+0428 Wow64Process : Ptr64 _EWOW64PROCESS
+0758 SharedCommitCharge : UInt8b
+0760 SharedCommitLock : _EX_PUSH_LOCK
+0768 SharedCommitLinks : _LIST_ENTRY
```

```
+0778 AllowedCpuSets : Uint8B
+0780 DefaultCpuSets : Uint8B
+0778 AllowedCpuSetsIndirect : Ptr64 Uint8B
+0780 DefaultCpuSetsIndirect : Ptr64 Uint8B
```

该结构的第一个成员 (`Pcb`) 是一个 `KPROCESS` 类型的嵌入结构。这是存储调度和时间计数数据的地方。你可以像显示 `EPROCESS` 一样显示内核进程结构的格式：

```
1kd dt ntl_process
+0000 Header : _DISPATCHER_HEADER
+0018 ProfileListHead : _LIST_ENTRY
+0028 DirectoryTableBase : Uint8B
+0030 ThreadListHead : _LIST_ENTRY
+0040 ProcessLock : Uint4B
+02c6 KernelTime : Uint4B
+0270 UserTime : Uint4B
+0274 LdtFreeuserHint : Uint2B
+0276 LdtTableLength : Uint2B
+0278 LdtSystemDescriptor : _KGDDTRY64
+0288 LdtBaseAddress : Ptr64 Void
+0290 LdtProcessLock : _FAST_MUTEX
+02c8 InstrumentationCallback : Ptr64 Void
+02d0 SecurePid : Uint8B
```

`dt` 命令允许你通过在结构名称后输入字段名称来查看一个或多个字段的特定内容。对于字段，输入 `dt ntl_process UniqueProcessid` 会显示进程 ID 字段。在表示结构的字段中——例如 `EPROCESS` 的 `Pcb` 字段，它包含 `KPROCESS` 子结构——在字段名后添加句点将允许调试器显示该子结构。查看 `KPROCESS` 的另一种方法是输入 `dt process`。你可以通过添加更多字段名称（在 `KPROCESS` 内部）继续递归。最后，`dt` 命令的 `-r` 开关允许你递归遍历所有结构。在开关后添加数字可以控制命令遵循的递归深度。

早些使用的 `dt` 命令显示的是所选结构的格式，而不是该结构类型的任何特定实例的内容。要显示实际进程的实例，你可以通过 `!process 0` 命令获取系统中几乎所有 `EPROCESS` 结构的地址（系统空闲进程除外）。因为 `KPROCESS` 是 `EPROCESS` 中的第一个内容，所以 `EPROCESS` 的地址也可以通过 `dt _kprocess` 用作 `KPROCESS` 的地址来工作。

# 实验：使用内核调试器 !process 命令

内核调试器 `!process` 命令显示进程对象及其关联结构中的部分信息。每个进程的输出分为两个部分。首先，你看到有关进程的信息，如下所示。当你不指定进程地址或 ID 时，`!process` 会列出当前在 CPU 0 上运行的线程所属进程的信息，在单进程系统上这就是 WinDbg 本身（如果如果在 WinDbg 中使用了 livekd 则是）。

```
1kd> !process
PROCESS fff0011c3243c0
SessionID: 2 Cid: 0e38 Peb: 52f1lde00 ParentId: 0f08
DirBase: 38b3e000 ObjectFile: fffff00da2b22200 HandleCount: <Data Not Accessible>
Image: windbg.exe
VadPort fffff0011bada6e0 Vads 11 Clone Private 3563. 228. Locked: 1
DeviceMap fffff000984e4330
Token fffff000a13f9a0
ElapsedTime 00:00:20.77
UserTime 00:00:00.00
KernelTime 00:00:00.15
QuotaUsage[PagedPool] 299512
QuotaUsage[NonPagedPool] 16240
Working Set Sizes (now,max) 9719
PeakSetSize 209731
VirtualSize 209732
PageFaultCount 13603
MemoryPriority FOREGROUND
BasePriority 8
CommitCharge 3994
Job fffff0011b85369
```

`process` 输出之后是进程中的线程列表。这在第 4 章的“使用内核调试器 `!thread` 命令”中有详细解释。

注意输出提供了 `PEB` 的地址。由于 `PEB` 在进程中，它仅在该进程上下文中有效。要查看另一个进程的 `PEB`，你必须先将 WinDbg 切换到进程。你可以使用 `.process` 命令加上 `EPROCESS` 指针来这样做。

如果你使用的是最新的 Windows SDK，更新版本的 WinDbg 将在 `PEB` 下包含一个直观的超链接，点击它可以自动执行 `.process` 命令和 `!peb` 命令。

位于进程用户态地址空间的 `PEB` 包含了加载器、堆管理器以及需要从用户态访问它的其他 Windows 组件所需的信息；通过系统调用暴露所有信息将成本太大。`EPROCESS` 和 `KPROCESS` 结构仅从内核态访问。`PEB` 的重要字段如图 3-4 所示，并在本章后面的部分进行了详细解释。

| 映像基地址 | `PEB_LDR_DATA` |
|---|---|
| 加载数据库 | |
| 线程本地存储数据 | |
| 进程标志位 | `RTL_USER_PROCESS_PARAMETERS` |
| 进程创建参数 | |
| 进程堆 (指针) | 进程堆 |
| NT 全局标志 | |
| GDI 共享句柄表 (指针) | GDI 共享句柄表 |
| 处理器数量 | |
| 进程堆信息 | |
| 加载锁 | `RTL_CRITICAL_SECTION` |
| OS 版本信息 | |
| AppCompat 数据 | |
| Shim 数据 | |
| 会话 ID | |
| 纤本地存储数据 | |
| 程序集和激活上下文 | |
| CSRSS 共享内存 (指针) | |
| 线程池信息 | |

**图 3-4** 进程环境块 (`PEB`) 的重要字段。

## 实验：检查 PEB

你可以使用内核调试器中的 `!peb` 命令转储 `PEB` 结构，它会显示当前在 CPU 0 上运行的线程所属进程的 `PEB`。通过使用上一个实验的信息，你也可以将 `PEB` 指针作为命令的参数。

```dbg
lkd>.process /P fffff001c3243c0 ; !peb 5f2f1de00
PEB at 000003561454000
InheritedAddressSpace: No
ReadImageFileExecutions: No
BeingDebugged: No
ImageBaseAddress: 00007ff64fa70000
Ldr: 00007ffdf5f2s200
Ldr.Initialized: Yes
Ldr.InInitializationModuleList: 000001d3d3d2b630 . 000001d3d6cddb60
Ldr.InOrderModuleList: 000001d3d3d23790 . 000001d3d6cddb40
Ldr.InMemoryOrderModuleList: 000001d3d3d2b37a0 . 000001d3d6cddb50
BaseStamp Module
7ff6f4fa70000 56ccafadd Feb 23 21:15:41 2016 C:\windows\windbg.exe
7ffdf5f1b0000 56bf9dd Feb 23 18:09:06 2019 C:\windows\system32\ntdll.dll
7ffd2fc10000 56d2d5aa Oct 30 04:27:54 2015 C:\windows\system32\KERNEL.DLL
```

`CSR_PROCESS` 结构包含了特定于 Windows 子系统（`csrss`）的进程信息。因此，只有 Windows 应用程序会与 `CSR_PROCESS` 结构相关联（例如，`Smss` 则没有）。此外，每个会话都有自己的 Windows 子系统实例；`CSR_PROCESS` 结构由每个独立会话中的 `Csrs` 进程维护。`CSR_PROCESS` 的基本结构如图 3-5 所示，并在本章稍后的部分进行详细解释。

| 客户端 ID | `CSR_PROCESS` |
|---|---|
| 进程链接 | |
| 线程列表头 | `CSR_THREAD` |
| 客户端端口句柄 | |
| 进程句柄 | |
| 客户端视图数据 | |
| 会话数据 | `CSR_NT_SESSION` |
| 进程标志 | |
| 引用计数 | |
| 消息数据 | 每个 `CSR_SERVER_DLL` 一个 |
| 关机级别 | |
| 标志 | |
| 进程组数据 | |
| 服务端数据 | |

图 3-5 `CSR` 进程结构体的字段。

## 实验：检查 CSR_PROCESS

`Csrs` 进程受到保护的（有关受保护进程的更多信息，请参阅本章稍后部分），因此无法向 `Csrs` 进程挂载用户调试器（即使具有特权权限或采用非侵入性方式）。相反，我们使用内核调试器。

首先，列出所有存在的 0 号 `Csrs` 进程：

```dbg
lkd> process 0 csrs.exe
PROCESS fffe00077ddf080
SessionId: 0 Cid: 02c0 Peb: c4e3fc0000 ParentId: 026c
DirBase: ObjectTable: ffff0004d15d040 HandleCount: 543.
Image: csrs.exe
```

```dbg
PROCESS fffe0007896080
SessionId: 1 Cid: 0338 Peb: d4b4db4000 ParentId: 0330
DirBase: ObjectTable: ffff0004dff0040 HandleCount: 514.
Image: csrs.exe
```

接下来，取其中任意一个进程，并将调试器上下文切换到指向其用户模块可见的特定进程：

```dbg
lkd> .process /r / fffe0007896080
Implicit process is now fffe0007896080
Loading User Symbols
```

`/p` 参数将调试器的进程上下文更改为提供的进程对象（`EPROCESS`，主要在行调试时需要），而 `/r` 请求加载用户符号。现在你可以使用 `Lm` 命令查看模块本身，或者查看 `CSR_PROCESS` 结构：

```dbg
lkd> dt csrss!_csr_process
+0000 ClientId : _CLIENT_ID
+0010 ListLink : _LIST_ENTRY
+0020 ThreadList : _LIST_ENTRY
+0030 NtSession : Ptr64 _CSR_NT_SESSION
+0038 ClientPort : Ptr64 Void
+0040 ClientBase : Ptr64 Char
+0048 ClientBounds : Ptr64 Char
+0050 ProcessHandle : Ptr64 Void
+0058 SequenceNumber : Uint48
+005c Flags : Uint48
+0060 DebugFlags : Uint48
+0064 ReferenceCount : Int34
+0068 ProcessGroupId : Uint48
+006c ProcessGroupSequence : Uint48
+0070 LastMessageSequence : Uint48
+0074 OutstandingMessages : Uint48
+0078 ShutdownLevel : Uint48
+007c ShutdownFlags : Uint48
+0080 Luid : _UUID
+0088 ServerDllPerProcessData : [1] Ptr64 Void
```
