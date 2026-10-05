OF64290_024502518 - LdrpMinimalMapModule - ENTER: DLL name: C:\WINDOWS\nSystem32\KERNEL32.dll
ModLoad:00007fff5b4b000 00007fff5b5d000 C:\WINDOWS\System32\KERNEL32.dll
OF64290_024502518 - LdrpMinimalMapModule - RETURN: Status: 0x00000000
OF64290_024502518 - LdrpProcessDllName - INFO: api-win-core-
tupport:11-2-0.dll was redirected to C:\WINDOWS\System32\ntdll1.dll by API set
OF64290_024502518 - LdrpFindKnownDll - ENTER: DLL name: KERNEL_BASE.dll
OF64290_024502518 - LdrpFindKnownDll - RETURN: Status: 0x00000000
OF64290_024502518 - LdrpMinimalMapModule - ENTER: DLL name: C:\WINDOWS\nSystem32\KERNEL_BASE.dll
ModLoad:00007fff5b890000 00007fff58dc600 C:\WINDOWS\System32\KERNEL_BASE.dll
OF64290_024502518 - LdrpMinimalMapModule - RETURN: Status: 0x00000000
OF64290_024502518 - LdrpProcessDllName - INFO: api-win-
eventing-provider-11-2-1.dll was redirected to C:\WINDOWS\System32\nkernelbase.dll by API set
OF64290_024502518 - LdrpProcessDllName - INFO: api-win-core-
appery-11-2-0.dll was redirected to C:\WINDOWS\SYSTEM32\ntdll.dll by API set

+   4. Eventually, the debugger breaks inside the loader, at a location
the loader checks whether a debugger is attached and freezes a breakpoint. If
press the g key to continue execution, you will see more messages from the loader, and
Notepad will appear.

+   5. Trying with Notepad and see how certain operations invoke the loader. A good
experiment is to use the Save/Open dialog box. That demonstrates that the loader
not only runs at startup, but continuously responds to requests that can cause
delayed loads of other modules (which can then be unloaded after use).

# Early process initialization

Because the loader is present in ntdll.dll, which is a native DLL associated with any
subsystem, all processes are to the same loader behavior (with some minor differences). Earlier,
we took a detailed look at the steps that leads to the creation of a process in kernel, as well
some of the work performed by the Windows function CreateProcess. Here, we'll see all the other
work that takes place in user mode, independent of any subsystem, as soon as the first thread-
instruction starts execution.

When a process starts, the loader performs the following steps:

+   1. It checks if LdrProcessInitialized is already set to 1 or if the SkipLoaderInit flag is set in
teB. In this case, skip initialization and wait three times for someone to call LdrProcess-
InitializationComplete. This is used in cases where process reflection is used by Windows
Error Reporting, or other process fork attempts where loader initialization is not needed.

+   2. It sets the LdrInitState to 0, meaning that the loader is uninitialized. Also set the PEB
ProcessInitializing flag to 1 and the TEB's ProcessInit1 to 1.