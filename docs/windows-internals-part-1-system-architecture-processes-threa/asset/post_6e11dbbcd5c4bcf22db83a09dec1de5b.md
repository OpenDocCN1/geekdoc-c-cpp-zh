
The TEB, illustrated in Figure 4-3, is one of the data structures explained in this section that exists in the process address space (as opposed to the system space). Internally, it is made up of a header called the Thread Information Block (TIB), which mainly existed for compatibility with OS/2 and Win9x applications. It also allows exception and stack information to be kept in a smaller structure when creating new threads by using an initial TIB.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_217_0.png)

FIGURE 4-3 Important fields of the thread environment block.

The TEB stores context information for the image loader and various Windows DLLs. Because these components run in user mode, we need a data structure writable from user mode. That's why this exists in the process address space instead of the system space, where it would be writable only from kernel mode. You can find the address of the TEB with the kernel debugger `thread` command.

## EXPERIMENT: Examining the TEB

You can dump the TEB structure with the `tb` command in the kernel or user-mode debugger. The command can be used on its own to dump the TEB for the current thread of the debugger or with a `tb` address to get it for an arbitrary thread. In case of a kernel debugger, the current process must be set before issuing the command on a TEB address so that the correct process context is used.

To view the TEB with a user-mode debugger, follow these steps. (You'll learn how to view the TEB using a kernel debugger in the next experiment.)

- 1. Open WinDbg.
- 2. Open the File menu and choose Run Executable.
- 3. Navigate to `c:\windows\system32\Notepad.exe`. The debugger should break at the initial breakpoint.
- 4. Issue the `!peb` command to view the TEB of the only thread existing at the moment (the example is from 64 bit Windows):

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

- 5. Enter the `g` command or press F5 to proceed with running Notepad.
- 6. In Notepad, open the File menu and choose Open. Then click Cancel to dismiss the Open dialog box.
- 7. Press Ctrl-Break or open the Debug menu and choose Break to forcibly break into the process.
- 8. Enter the `~` (tilde) command to show the threads in the process. You will see something like this:

```
0:005->~
0 Id: 21bc.1b74 Suspend: 1 Teb: 000000ef125c1000 Unfrozen
1 Id: 21bc.6450 Suspend: 1 Teb: 000000ef125e3000 Unfrozen
2 Id: 21bc.1a98 Suspend: 1 Teb: 000000ef125e5000 Unfrozen
3 Id: 21bc.8860 Suspend: 1 Teb: 000000ef125e7000 Unfrozen
4 Id: 21bc.28e0 Suspend: 1 Teb: 000000ef125c9000 Unfrozen
5 Id: 21bc.23e0 Suspend: 1 Teb: 000000ef124a0000 Unfrozen
6 Id: 21bc.244c Suspend: 1 Teb: 000000ef125eb0000 Unfrozen
7 Id: 21bc.168c Suspend: 1 Teb: 000000ef125ed0000 Unfrozen
8 Id: 21bc.c90 Suspend: 1 Teb: 000000ef125ef0000 Unfrozen
9 Id: 21bc.1558 Suspend: 1 Teb: 000000ef125f1000 Unfrozen
10 Id: 21bc.a64 Suspend: 1 Teb: 000000ef125f3000 Unfrozen
11 Id: 21bc.20c4 Suspend: 1 Teb: 000000ef125f5000 Unfrozen
12 Id: 21bc.a254 Suspend: 1 Teb: 000000ef125f7000 Unfrozen
13 Id: 21bc.f7d8 Suspend: 1 Teb: 000000ef125f9000 Unfrozen
14 Id: 21bc.f4b Suspend: 1 Teb: 000000ef125fb000 Unfrozen
15 Id: 21bc.17cb Suspend: 1 Teb: 000000ef125fd000 Unfrozen
```

- 9. Each thread shows its TEB address. You can examine a specific thread by specifying its TEB address to the `tb` command. Here is an example for thread 9:

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

- 10. Of course, it is possible to view the actual structure of the TEB (truncated to save space):

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
+0x0a8 EffectiveContainerId: _GUID({00000000-0000-0000-0000-000000000000})
```

## EXPERIMENT: Examining the TEB with a kernel debugger

Follow these steps to view the TEB with a kernel debugger:

- 1. Find the process for which a thread's TEB is of interest. For example, the following looks for explorer.exe processes and lists its threads with basic information (truncated):

```
1kd> Process 0 explorer.exe
PROCESS ffff00012bea7840
SessionId: C2 Cid: 10d8 Peb: 00251000 Parentid: 10bc
DirBase: 76e1200 ObjectTable: ffff00c1ca080 HandleCount: <Data Not Accessible:
explorer.exe:

THREAD ffff00012b53080 Cid: 10d8.10dc Teb: 000000000252000
Win32Thread: ffff00012c5352f0 WAIT: (UserRequest) UserMode Non-Alertable
ffff0002c257fe0 SynchronizationEvent

THREAD ffff00012a30f080 Cid: 10d8.114c Teb: 000000000266000
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

- 2. If more than one explorer.exe process exists, select one for the following:

- 3. Each thread shows its TEB address. Because the TEB is probably resident in kernel memory, you need to switch to the process as seen by the debugger.

- 4. Now you can use the `!peb` command with the TEB address.
