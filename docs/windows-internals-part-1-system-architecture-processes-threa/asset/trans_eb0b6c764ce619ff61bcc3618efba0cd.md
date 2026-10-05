
如图 4-3 所示，TEB 是本节解释的数据结构之一，它存在于进程地址空间中（而不是系统空间中）。在内部，它由一个称为线程信息块（TIB）的头部组成，该头部主要为了为了兼容 OS/2 和 Win9x 应用。它还允许在创建新线程时通过使用初始 TIB，将异常和堆栈信息存储在较小的结构中。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_217_0.png)

图 4-3 线程环境块的重要字段。

TEB 存储了映像加载器和各种 Windows DLL 的上下文信息。由于这些组件运行在用户模式下，我们需要一个可以从用户模式写入的数据结构。这就是为什么它存在于进程地址空间而不是系统空间的原因，在系统空间中，它只能从内核模式进行写。你可以使用内核调试器的 `thread` 命令来找到 TEB 的地址。

## 实验：检查 TEB

你可以在内核或用户模式调试器中使用 `tb` 命令转储 TEB 结构。该命令可以单独使用以转储调试器当前线程的 TEB，也可以配合 `tb` 地址来获取任意线程的 TEB。在内核调试器中，在对 TEB 地址发出命令之前，必须设置当前进程，以便使用正确的进程上下文。

要使用用户模式调试器查看 TEB，请按照以下步骤操作。（你将在下一个实验中学习如何使用内核调试器查看 TEB。）

- 1. 打开 WinDbg。
- 2. 打开“文件”（File）菜单并选择“运行执行”（Run Executable）。
- 3. 导航到 `c:\windows\system32\Notepad.exe`。调试器应该会在初始断点处中断。
- 4. 执行 `!peb` 命令查看当前唯一线程的 TEB（示例来自 64 位 Windows）：

```
0:000-> !peb
TEB at 000000ef125c1000
ExceptionList: 0000000000000000
StackBase: 000000ef12290000
StackLimit: 000000ef1227f000
SubSystemTIB: 0000000000000000
FiberData: 00000000000001e0
ArbitraryUserPointer: 0000000000000000
Self: 000000ef125c1000
EnvironmentPointer: 0000000000000000
ClientId: 000000000000021bc . 00000000000001b74
RpcHandle: 0000000000000000
TLS Storage: 0000026e572b600
PEB Address: 000000ef125c0000
LastError: 0
LastStatusValue: 0
Counted Owned Locks: 0
HardError: 0
```

- 5. 输入 `g` 命令或按 F5 继续运行记事本。
- 6. 在记事本中，打开“文件”（File）菜单并选择“打开”（Open）。然后点击“取消”（Cancel）关闭打开对话框。
- 7. 按 Ctrl-Break 或打开“调试”（Debug）菜单并选择“中断”（Break）以强制中断进程。
- 8. 输入 `~`（波号）命令显示进程中的线程。你会看到类似的内容：

```
0:005->~
0 Id: 21bc.1b74 Suspend: 1 Teb: 000000ef125c1000
1 Id: 21bc.6450 Suspend: 1 Teb: 000000ef125e3000
2 Id: 21bc.1a98 Suspend: 1 Teb: 000000ef125e5000
3 Id: 21bc.8860 Suspend: 1 Teb: 000000ef125e7000
4 Id: 21bc.28e0 Suspend: 1 Teb: 000000ef125c9000
5 Id: 21bc.23e0 Suspend: 1 Teb: 000000ef124a0000
6 Id: 21bc.244c Suspend: 1 Teb: 000000ef125eb0000
7 Id: 21bc.168c Suspend: 1 Teb: 000000ef125ed0000
8 Id: 21bc.c90 Suspend: 1 Teb: 000000ef125ef0000
9 Id: 21bc.1558 Suspend: 1 Teb: 000000ef125f1000
10 Id: 21bc.a64 Suspend: 1 Teb: 000000ef125f3000
11 Id: 21bc.20c4 Suspend: 1 Teb: 000000ef125f5000
12 Id: 21bc.a254 Suspend: 1 Teb: 000000ef125f7000
13 Id: 21bc.f7d8 Suspend: 1 Teb: 000000ef125f9000
14 Id: 21bc.f4b Suspend: 1 Teb: 000000ef125fb000
15 Id: 21bc.17cb Suspend: 1 Teb: 000000ef125fd000
```

- 9. 每个线程都显示其 TEB 地址。你可以通过向 `tb` 命令指定 TEB 地址来检查特定线程。这里是线程 9 的示例：

```
0D05> !tb 000000ef125f1000
TEB at 000000ef125f1000
ExceptionList: 0000000000000000
StackBase: 000000ef12340000
StackLimit: 000000ef123e0000
SubSystemTIB: 0000000000000000
FiberData: 00000000000001e0
ArbitraryUserPointer: 0000000000000000
Self: 000000ef125c1000
EnvironmentPointer: 0000000000000000
ClientId: 000000000000021bc . 0000000000000158
RpcHandle: 0000000000000000
TLS Storage: 0000026e572b600
PEB Address: 000000ef125c0000
LastError: 0
LastStatusValue: 0
Counted Owned Locks: 0
HardError: 0
```

- 10. 当然，可以查看 TEB 的实际结构（为了节省空间进行了截断）：

```
0D05> ntdll!peb 000000ef125f1000
+0x000 TIB: _NT_TIB
+0x038 EnvironmentPointer: (null)
+0x040 ClientId: _CLIENT_ID
+0x050 ActiveRpcHandle: (null)
+0x058 LocalStoragePointer: 0x00000026eaaf280
+0x060 ProcessEnvironmentBlock: 0x000000ef125c0000
+0x068 LastError: 0
+0x070 CountOfOwnedCritical: 0
+0x078 LockCount: 0
+0x080 TebOffset: 0
+0x090 ResourceRetVal: 0x00000026ea2a5e0
+0x098 ReservedForWdf: (null)
+0x0a0 ReservedForCt: 0
+0xa8 EffectiveId: _GUID({00000000-0000-0000-0000-000000000000})
```

 实验：使用内核调试器检查 TEB

按照以下步骤使用内核调试器查看 TEB：

- 1. 找到感兴趣线程 TEB 的进程。例如，以下显示了 explorer.exe 进程及其线程的基本信息：

```
1kd> Process 0 explorer.exe
PROCESS ffff00012bea780
SessionId: C2 Cid: 10d8 Peb: 0025100
DirBase: 76e1200 HandleCount: <Data Not Accessible:
explorer.exe:

THREAD ffff00012b53080 Cid: 10d8.1dc Teb: 000000000252000
Win32Thread: ffff00012c532f0 WAIT: (UserRequest) UserMode Non-Alertable
ffff0002c257fe0 SynchronizationEvent

THREAD ffff00012a30f080 Cid: 10d8.14c Teb: 000000000266000
Win32Thread: ffff00012c9a290 WAIT: (UserRequest) UserMode Alertable
ffff0012bbab850 SynchronizationEvent

THREAD ffff00012c6cb0d80 Cid: 10d8.1178 Teb: 00000000026c0000
Win32Thread: ffff00012a081310 WAIT: (UserRequest) UserMode Alertable
ffff0012bfd9250 NotificationEvent
ffff0012c9512fe0 NotificationEvent
ffff0012c76b8b0 NotificationEvent
ffff0012c010fe0 NotificationEvent
ffff0012d03ba7e0 NotificationEvent
ffff0012cf9d1e0 NotificationEvent

THREAD ffff00012c8e0e80 Cid: 10d8.1180 Teb: 0000000002700000
Win32Thread: ffff00012c8e0e80 WAIT: (UserRequest) UserMode Alertable
ffff0012adad40 Synchronization
```

- 2. 如果存在多个 explorer.exe 进程，选择一个进行后续操作。

- 3. 每个线程显示其 TEB 地址。由于 TEB 可能驻留在内核内存中，你需要切换到调试器可见的进程。

- 4. 现在你可以使用 `!peb` 命令配合 TEB 地址。

