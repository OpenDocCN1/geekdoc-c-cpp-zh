# EXPERIMENT: Examining the CSR_PROCESS

Csrs processes are protected (see later in this chapter for more on protected processes), so it's not possible to attach a user debugger to a Csrs process (even with elevated privileges or non-invasively). Instead, we use the kernel debugger.

First, list the existing 0 Csrs processes:

```
lkd> process 0 csrs.exe
PROCESS fffe00077ddf080
SessionId: 0 Cid: 02c0 Peb: c4e3fc0000 ParentId: 026c
DirBase: ObjectTable: ffff0004d15d040 HandleCount: 543.
Image: csrs.exe
```

```
PROCESS fffe0007896080
SessionId: 1 Cid: 0338 Peb: d4b4db4000 ParentId: 0330
DirBase: ObjectTable: ffff0004dff0040 HandleCount: 514.
Image: csrs.exe
```

Next, take any one of them and change the debugger context to point to the particular process that its user modules are visible:

```
lkd> .process /r / fffe0007896080
Implicit process is now fffe0007896080
Loading User Symbols
```

The /p changes the process context of the debugger to the provided process object (EPROCESS, mostly needed in line debugging) and /r requests loading of user symbols. Now you can look at the modules themselves using the Lm command or look at the CSR_PROCESS structure:

```
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