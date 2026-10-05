# TABLE 3-9 Fields in loader data table entry (continued)

| Field | Meaning |
|---|---|
| ParentDllBase | In case of static (or forward, or delay-load) dependencies, stores the address of the DLL that has a dependency on this one. |
| SigningLevel | Stores the signature level of this image (see Chapter 8, Part 2, for more information on the Code infrastructure). |
| SizeOfImage | The size of the module. |
| SwitchBackContext | Used by SwitchBack (described later) to store the current Windows context GUID associated with this module, and other data. |
| TimeDateStamp | A time stamp written by the linker when the module was linked, which the loader obtains from the module image PE header. |
| TlsIndex | The thread local storage slot associated with this module |

One way to look at a process's loader database is with WinDbg and the next experiment shows you how to do this and how to look at the LDR_DATA_TABLE_ENTRY structures on your own.

# EXPERIMENT: Dumping the loaded modules database

Before starting the experiment, perform the same steps as in the previous two experiments to launch Notepad.exe with WinDbg the debugger. When you get to the initial breakpoint (where you've been instructed to type g until now), follow these instructions:

+   1. You can look at the PE of the current process with the !peb command. For now, you're interested only in the Ldr data that will be displayed.

```
0:000:~peb
PE at 00000000d4c901000
InheritedAddressSpace: No
ReadImageFileExecOptions: No
BeingDebugged: Yes
ImageBaseAddress: 0007ffe820b60000
Ldr: 0007ffe85d253a0
Ldr.Initialized: Yes
Ldr.InInitializationOrderModuleList: 0000022815d23d30 0000022815d24430
Ldr.InLoadOrderModuleList: 0000022815d23ee0 0000022815d31240
Ldr.InMemoryOrderModuleList: 0000022815d23ef0 0000022815d31520
Base Timestamp Module
7ff720b60000 5789896a Jul 16 15:04:02 2016 C:\Windows\System2\
notepad.exe 7ffe85480000 5825828f7 Nov 11 10:59:43 2016 C:\WINDOWS\SYSTEM32\
tdll.dll 7ffe84b00000 57899a29 Jul 16 05:21:26 2016 C:\WINDOWS\System32\
kernel2.dll 7ffe823c0000 582858e6 Nov 11 11:01:26 2016 C:\WINDOWS\System32\
...
```