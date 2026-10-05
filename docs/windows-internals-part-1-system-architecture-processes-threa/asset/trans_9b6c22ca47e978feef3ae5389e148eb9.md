

```
+0x040 ThreadLock : Uint8B
+0x048 CycleTime : Uint8B
+0x050 RuntimeError : Uint4B
...
+0x5a0 ReadOperationCount : Int8B
+0x5a8 WriteOperationCount : Int8B
+0x5b0 OtherOperationCount : Int8B
+0x5b8 ReadTransferCount : Int8B
+0x5c0 WriteTransferCount : Int8B
+0x5c8 OtherTransferCount : Int8B
+0x5d0 QueuedScb : Ptr64_KSCB
```

## 实验：使用内核调试器 !thread 命令

内核调试器 `!thread` 命令会转储线程数据结构中的部分信息。内核调试器显示的某些关键元素无法通过任何工具显示，包括以下信息：

- 内部结构地址
- 优先级详情
- 挂起 I/O 请求列表
- 对于处于等待状态的线程，该线程正在等待的对象列表

要显示线程信息，可以使用 `!process` 命令（在显示进程信息后显示该进程的所有线程）或 `!thread` 命令（通过显示线程对象的地址来显示特定线程）。

让我们找到 `explorer.exe` 的所有实例：

```
1kd> !process 0 explorer.exe
PROCESS fffe0001f3fe7c0
SessionId: 1 Cid: 0b7c Peb: 0221900 ParentCid: 03c4
DirBase: 19b264000 ObjectTable: fffff0007268cc0 HandleCount: 2248.
Image: explorer.exe
```

```
PROCESS fffe0001b8c17c0
SessionId: 1 Cid: 23b0 Peb: 02256000 ParentCid: 03f0
DirBase: 2d4010000 ObjectTable: fffff0001aef0480 HandleCount: 2208.
Image: explorer.exe
```

我们将选择其中一个实例并显示它的线程：

```
1kd> !process fffe0001b8c17c0 2
PROCESS fffe0001b8c17c0
SessionId: 1 Cid: 23b0 Peb: 02256000 ParentCid: 03f0
DirBase: 2d4010000 ObjectTable: fffff0001aef0480 HandleCount: 2232.
Image: explorer.exe
```

THREAD fffe0001ac30c80 Cid 23b0.2b88 Teb 000000002570000 Win32Thread:
fffe000157ca200 WAIT: (UserRequest) UserMode Non-Alertable
fffe0001b6eb470 SynchronizationEvent

THREAD fffe0001af10800 Cid 23b0.2f40 Teb: 00000000265000 Win32Thread:
fffe000156688a0 WAIT: (UserRequest) UserMode Non-Alertable
fffe000172ad4f0 SynchronizationEvent
fffe0001c26420 SynchronizationEvent

THREAD fffe0001b69a080 Cid 23b0.2fac Teb: 00000000267000 Win32Thread:
fffe000192c5d350 WAIT: (UserRequest) UserMode Non-Alertable
fffe000188d3c00 SynchronizationEvent
fffe0001552ff440 SynchronizationEvent

...

THREAD fffe000223422080 Cid 23b0.3d8c Teb: 0000000003cf00 Win32Thread:
fffe0001eccd790 WAIT: (WaitForQueue) UserMode Alertable
fffe0001aec9080 QueueObject

THREAD fffe000232f30880 Cid 23b0.3a8f Teb: 0000000003d100 Win32Thread:
00000000000000000 WAIT: (WaitForQueue) UserMode Alertable
fffe0001aec9080 QueueObject

THREAD fffe000232b0f80 Cid 23b0.2d6c Teb: 0000000003d300 Win32Thread:
00000000000000000 WAIT: (WaitForQueue) UserMode Alertable
fffe0001aec9080 QueueObject

THREAD fffe0001f0b5800 Cid 23b0.3398 Teb: 0000000003e300 Win32Thread:
00000000000000000 WAIT: (UserRequest) UserMode Alertable
fffe0001d1ad970 SynchronizationEvent
fffe0002b42660 Synchronization

为了节省空间，线程列表被截断了。每个线程的地址 (ETH) 可以传递给线程；其进程 ID (cid) 和线程 ID（前面的线程都是该进程的一部分）；环境块 (TEB)，以及线程状态（必须处于等待状态）。下一行可能显示正在等待的对象列表。

要获取特定线程的更多信息，请将其地址传递给线程：

```
1kd> thread fffe0001d45d800
THREAD fffe0001d45d800 Cid 23b0.45c2 Teb: 0000000026d000 Win32Thread:
fffe0001aace630 WAIT: (UserRequest) UserMode Non-Alertable
fffe00013678350 NotificationEvent
fffe000222ab370 Limit 0xffff
fffe000222564b0 SynchronizationEvent
Owning Process ffffc0004f7ddb0 Image: explorer.exe
fffe00018c17c00 198 Threads
Attached Process N/A Image: N/A
WaitCount 7233205 Ticks: 00:00:04.218 Count 6570 Processor: 7
UserTime: 00:00:00.078
KernelTime: 00:00:00.046
Win32 Start Address ffff000271d4c90 ffff0000271d3f
Stack In ffff000271d5000 Limit ffff0000271c00 Call 000000000000000
Priority 9 Degree 0 Priority 5
GetContext failed, 0x804001
unable to get current state, HRESULT 0x804001
Child-SP ffff000271d3fc0 ffff00f3f086ca 000000000000000000001
0000000000000000000000 : ntKiSwapContext+0x16
fffff000271d4100 ffff000271b08519 ffff000271d5a8d ffff0003b88039
fffff0001eac9080 00000000000000f : ntKiSwapThread+0x15
fffff000271d41b60 ffff00f3f086ce 000000000000000000000000
fffff000271d419cf 000000000000000 : ntKiCommitThread+0x19
fffff000271d42a40 ffff0003bf2aad ffff000271d3c0
000000000000000 : ntKiWaitForObjects+0xbd
fffff000271d4300 ffff00f3bf2a2a6 ffff0083bf1a40 ffff000271d488
fffff000271d4858 ffff0003bf1e6e8 ntKiWaitForObjects+0x24
fffff000271d4810 ffff00f3bf3defaa ffff000fa0 ffff0083bf2ef0ad
fffff0001e4d5d800 000000000 16e2f1d98 ntKiWaitForObjects+0x66
fffff000271d49a0 000077ffe-4b5c24 000000000000000
0000000000000000 : 00
```

关于线程有大量信息，例如其优先级、堆栈详情和内核时间等。你将在本章以及第 5 章“内存管理”和第 6 章“I/O 系统”中查看这些许多细节。

## 实验：使用 list 查看线程信息

以下输出是使用 Windows 调试工具中的 `list` 命令对进程进行的详细显示。（请确保你从 "fitness" 作为目标进程运行 `list`。）请注意，线程显示了 `Win32StartAddr`。这是应用程序传递给 `CreateThread` 函数的地址。所有工具（Process Explorer 除外）都会显示线程起始地址：实际起始地址（`Ntdll.dll` 中的一个函数）或应用程序特定的起始地址。

以下是正在运行 `list` 的输出：

```
