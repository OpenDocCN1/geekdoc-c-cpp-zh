
- The executable path and command-line arguments.

- Optional security attributes applied to the new process and thread object that's about to be created.

- A Boolean flag indicating whether all handles in the current (creating) process that are marked inheritable (copied) to the new process. (See Chapter 8, "System mechanisms," in Part 2 for handles and handle inheritance.)

- Various flags that affect process creation. Here are some examples. (Check the Windows SDK documentation for a complete list.)
    - CREATE_SUSPENDED: creates the initial thread of the new process in the suspended state. A later call to ResumeThread will cause the thread to begin execution.
    - DEBUG_PROCESS: The creating process is declaring itself to be a debugger, creating the new process under its control.
    - EXTENDED_STARTUPINFO_PRESENT: The extended STARTUPINFO structure is provided instead of STARTUPINFO (described below).

- An environment block for the new process (specifying environment variables). If not specified, it will be inherited from the creating process.

- An current directory for the new process. (If not specified, it uses the one from the creating process.) The created process can call SetCurrentDirectory to set a different one. The current directory of a process is used in non-full path searches (such as loading a DLL with a filename only).

- A STARTUPINFO or STARTUPINFOEX structure that provides more configuration for process creation. STARTUPINFO contains an additional opaque field that represents a set of process and thread attributes that are essentially an array of key/value pairs. These attributes are filled by calling UpdateThreadAttr, for each attribute that's needed. Some of these attributes are undocumented and used internally, such as when creating stores, as described in the next section.

- A PROCESS_INFORMATION structure that is the output of a successful process creation. This structure holds the new unique process ID, the new unique thread ID, a handle to the new process and a handle to the new thread. The handles are useful for the creating process if it wants to manipulate the new process or thread in some way after creation.

## Creating Windows modern processes

Chapter 1 described the new types of applications available starting from Windows 8 and Windows Server 2012. The names of these apps have changed over time, but we'll refer to them as modern apps, UWP apps, or immersive processes, to distinguish them from the classic, also known as desktop, applications.

Creating a modern application process requires more than just calling CreateProcess with the correct executable path. Another requirement is adding an undocumented process attribute (using UpdateProcThreadAttribute) with a key named PROC_THREAD_ATTRIBUTE_PACKAGE_NAME to set the value. While this attribute is undocumented, there are other ways (from an API perspective) to execute a store app. For example, Windows provides a COM interface IApplicationActivationManager that is implemented by a COM class with a CLSID CLSID_ApplicationActivationManager. One of the methods in the interface is ActivateApplication, which can be used to launch a store app after opening something known as UserUserModel from the store app package name by calling GetPackageApplicationIds. (See the Windows SDK for more information on these APIs.)

Package names and the way a store app is typically created, from a user tapping on a modern app tile, eventually leading to CreateProcess, is discussed in Chapter 9 Part 2.

## Other kinds of processes

Although Windows launches either classic or modern applications, the Executive includes support for additional kinds of processes that must be started by bypassing the Windows API, as as native processes, minimal processes, or Pico processes. For example, we described in Chapter 2 the existence of Smss, the Session Manager, which is an example of a native image. Since it is created by the kernel, it obviously does not use the CreateProcess API, but instead calls directly NtCreateUserProcess. Similarly, when Smss creates Autoch (the check disk utility) or Csrss (the Windows subsystem process), the Windows API is also not available, and NtCreateUserProcess cmdlet must be used. Additionally, native processes cannot be created from Windows applications, as the CreateProcessInternal function will reject images with the subsystem image type. To alleviate these complications, the native library, Ntdll.dll, includes an exported helper function called RtlCreateProcess, providing a simpler wrapper around NtCreateUserProcess.

As its name suggests, NtCreateUserProcess is used for the creation of user-mode processes. However, as we see in Chapter 2, Windows also includes a number of kernel-mode processes, such as the System process and the Memory Compression processes (which are minimal), plus the possible processes managed by a provider such as the Windows Subsystem for Linux. The creation of such processes is instead provided by the NtProcessEx system, with capabilities reserved solely for kernel-mode callers (such as the creation of minimal processes).

Finally, Pico providers call a helper function, which takes care of both creating the minimal process as well as initializing PspCreatePicoProcess. This function is not exported, and is only available to Pico providers through their special interface.

As we will see in the flow section later in this chapter, although NtCreateProcessEx and NtUserProcess are different systems, the internal routines are used to perform the work: PspAllocateProcess and PspInsertProcess. All the possible ways we have enumerated so far to create a process, and any you can imagine, from a WMI PowerShell cmdlet to a kernel driver, will end up there.

## Process internals

This section describes the Windows process data structures maintained by various parts of the system and describes different ways and tools to examine this data.

Each Windows process is represented by an executive process (EPROCESS) structure. Besides containing many attributes relating to a process, EPROCESS contains and points to a number of other related data structures. For example, each process has one or more threads, each represented by an executive thread (ETHREAD) structure. (Thread data structures are explained in Chapter 4, "Threads")

The EPROCESS and most of its related data structures exist in system address space. One exception is the Process Environment Block (PEB), which exists in the process (user) address space (because it contains information accessed by user-mode code). Additionally, some of the process data structures used in memory management, such as the working set, are list only within the context of the current process, because they are stored in process-specific system space. (See Chapter 5, "Memory management," for more information on process address space)

For each process that is executing a Windows program, the Windows subsystem process (Csrss) maintains a parallel structure called CSR_PROCESS. Additionally, the kernel-mode part of the Windows subsystem (w32ks.sys) maintains a per-process data structure, w32process, which is created the first time a thread calls a Windows USER or GUI function that it can. This happens as soon as the User32.dll library is loaded. Typical functions that this library is loaded by are CreateWindow(Ex) and GetMessage.

Since the kernel-mode Windows subsystem makes heavy use of DirectX-based hardware acceleration, the Graphics Device Interface (GDI) component infrastructure causes the DirectX Kernel (Dxgkrnl.sys) to initialize a structure of its own, DXPROCESS. This structure contains information for DirectX objects (surfaces, shaders, etc.) and the GPU-related counters and policy settings for computational and memory management-related scheduling.

Except for the idle process, every EPROCESS structure is encapsulated as a process object by the executive manager (described in Chapter 8 in Part 2). Because processes are not named objects, they are not visible in the WinObj tool (from Sysinternals). You can see the Type object Process in the ObjectTypes directory (in WinObj). A handle to a process provides, through use of the process-related APIs, access to some of the data in the EPROCESS structure and in some of its associated structures.

Many drivers and system components, by registering process-creation notifications, choose to create their own data structures to track information on a per-process basis. The executive functions PsSetCreateProcessNotifyRoutine(Ex, Ex, Ex,2) allow this and are documented in the WDK. Additionally, some of these functions allow them to disable, or block, the creation of processes. This provides anti-malware vendors with an architectural way to add security enhancements to the operating system, either through hash-based blacklisting or other techniques.
