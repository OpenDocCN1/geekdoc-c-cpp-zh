
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

## EXPERIMENT: Using the kernel debugger !thread command

The kernel debugger !thread command dumps a subset of the information in the thread data structures. Some key elements of the kernel debugger displays can't be displayed by any utility, including the following information:

- Internal structure addresses
- Priority details
- The pending I/O request list
- For threads in a wait state, the list of objects the thread is waiting for

To display thread information, use either the !process command (which displays all the threads of a process after displaying the process information) or the !thread command (which displays the address of a thread object to display a specific thread.

Let's find all instances of explorer.exe:

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

We'll select one of the instances and show its threads:

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

THREAD fffe000232f3080 Cid 23b0.3a8f Teb: 0000000003d100 Win32Thread:
00000000000000000 WAIT: (WaitForQueue) UserMode Alertable
fffe0001aec9080 QueueObject

THREAD fffe000232b0f80 Cid 23b0.2d6c Teb: 0000000003d300 Win32Thread:
00000000000000000 WAIT: (WaitForQueue) UserMode Alertable
fffe0001aec9080 QueueObject

THREAD fffe0001f0b5800 Cid 23b0.3398 Teb: 0000000003e300 Win32Thread:
00000000000000000 WAIT: (UserRequest) UserMode Alertable
fffe0001d1ad9790 SynchronizationEvent
fffe0002b42660 SynchronizationTimer

The list of threads is truncated for the sake of space. Each thread shows its address (ETHREAD), which can be passed to the thread command; its client ID (Cid)-process ID and thread ID (the process ID for all preceding threads is, they are part of the explorer process); the Thread Environment Block (TEB, discussed monumentally); and the thread state (must be in the Wait state, with the wait for the parents). The next line may show a list of synchronization objects that is waiting.

To get more information on a specific thread, pass its address to the thread command:

```
1kd> thread fffe0001d45d800
THREAD fffe0001d45d800 Cid 23b0.45c2 Teb: 0000000026d000 Win32Thread:
fffe0001aace630 WAIT: (UserRequest) UserMode Non-Alertable
fffe00013678350 NotificationEvent
fffe000222ab370 Limit 0xffff
fffe000222564b50 SynchronizationEvent
Not impersonating
Owning Process ffffc0004f7ddb0 Image: explorer.exe
fffe00018c17c00 198 Threads

Attached Process N/A Image: N/A
WaitCount 7233205 Ticks: 00:00:04.218 Context Count 6570 Processor: 7
UserTime: 00:00:00.078
KernelTime: 00:00:00.046
Win32 Start Address ffff000271d4c90 ffff0000271d3f
Stack In ffff000271d5000 Limit ffff0000271c00 Call 000000000000000
Priority 9 Degree 0 Priority 5
GetContext failed, 0x8004001
unable to get current state, HRESULT 0x8004001
Child-SP ffff000271d3fc0 ffff00f3f0886ca 0000000000000000000001
00000000000000000000000 : ntKiSwapContext+0x16
fffff000271d4100 ffff000271b08519 ffff000271d5a8d ffff0003b88039
fffff0001eac9080 00000000000000f : ntKiSwapThread+0x15
fffff000271d41b60 ffff00f3f086ce 000000000000000000000000
fffff000271d419cf 000000000000000 : ntKiCommitThread+0x19
fffff000271d42a40 ffff0003bf2a4ad ffff000271d3c0
000000000000000 : ntKiWaitForObjects+0xbd
fffff000271d4300 ffff00f3bf2a2a6 ffff0083bf1a40 ffff000271d488
fffff000271d4858 ffff0003bf1e6e8 ntKiWaitForObjects+0x24
fffff000271d4810 ffff00f3bf3defaa ffff000fa0 ffff0083bf2ef0ad
fffff0001e4d5d800 000000000 16e2f1d98 ntKiWaitForObjects+0x66
fffff000271d49a0 000077ffe-42b5c24 000000000000000
0000000000000000 : 00
```

There is a lot of information about the thread, such as its priority, stack details, and kernel times, and much more. You'll look at many of these details throughout this chapter and in Chapter 5, "Memory management," and Chapter 6, "I/O system."

## EXPERIMENT: Viewing thread information with list

The following output is the detailed display of a process using list the Debugging Tools for Windows (Make sure you run list from "fitness" as the target process.) Notice that the thread shows Win32StartAddr This is the address passed to the CreateThread function by the application. All the utilities (except Process Explorer) will show the thread start address the actual start address (a function in Ntdll.dll), or the application-specific start address.

The following output is from running list on Windows 2016 (truncated):

```
C:\Dbg\x86>list winword
120 WINWORD.EXE Chapter04.docm - Word
Cw: C:\Users\pavel\Documents\
```

```
CmdLine:C="C:\Program Files (x86)\\Microsoft Office\Root\office16\WINWORD.EXE" /n
D="C:\OneDrive\WindowsBook\tEdition\Chapter04\Chapter04.docm
VirtualSize:77012 KB PeakVirtualSize:83268 KB
WorkingSetSize:16536 KB PeakWorkingSetSize:227144 KB
Threads:4
12132 StartAddr:0x00920100 LastAddr:0x00000000 State:Waiting
15540 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
7096 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
17696 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
17492 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
4052 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
2688 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
9100 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
1836 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
1118 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
9352 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
15052 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
13612 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
1208 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
9456 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
16208 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
8054 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
5396 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
11232 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
15540 StartAddr:0x07cc2fd8 LastAddr:0x00000000 State:Waiting
```
