
# Process Explorer - Sysinternals.microsoft.com (MSDNRESOFT)

| Process | CPU | % | Working Set | PID | Description | Company Name | Image | Base | Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| services.exe | 0.00 | 0.00 | 1,217,132 | 684 | Windows IIS Host Service | Microsoft Corporation | image | 0x7FFC8000 | Data |
| svchost.exe | 0.00 | 0.00 | 1,184,664 | 15148 | Windows Connection Manager | Microsoft Corporation | image | 0x7FFC8000 | Data |
| svchost.exe | 0.00 | 0.00 | 2,147,256 | 1212 | Local Session Manager | Microsoft Corporation | image | 0x7FFC8000 | Data |
| vmware.exe | 0.00 | 0.00 | 36,726 | 36726 | Windows Memory Worker Proc. | Microsoft Corporation | image | 0x7FFC8000 | Data |
| taskhost.exe | 1.15 | 0.01 | 21,200 | 1438 | Windows Resource Scheduler | Microsoft Corporation | image | 0x7FFC8000 | Data |
| WaveSrv64.exe | 0.00 | 0.00 | 3,864 | 724 | Windows Audio Service | Windows Audio Audit | image | 0x7FFC8000 | Data |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_333_0.png)

CPU Usage: 16.48% Memory Usage: 41.14% Physical Usage: 15.32%

You can also search for memory-mapped files by using the Find and choosing Find Handle or DLL (or pressing Ctrl+F). This can be useful when determining which process(es) is a DLL or a memory-mapped file that you are trying to replace.

## Protecting memory

As explained in Chapter 1, "Concepts and tools," Windows provides memory protection so that no user can inadvertently or deliberately corrupt the address space of another process or the operating system. Windows provides this protection in four primary ways:

- System-wide data structures and memory pools used by kernel-mode system components can be accessed only when in kernel mode. User-mode threads cannot access these pages. If they attempt to do so, Windows generates a general fault, which the memory manager reports to the reader as an access violation.
- Each process has a separate, private address space, protected from access by any thread belonging to another process. Even shared memory is not an exception to this because each process accesses the shared regions that are part of its own virtual address space. The only exception is if another process has memory read or write access to the process object (or SeDebugPrivilege) and can use the ReadProcessMemory or WriteProcessMemory function. Each time a thread references an address, the virtual hardware, in conjunction with the memory manager, intervenes and translates the virtual address into a physical one. Windows can ensure that threads running in one process do not inappropriately access a page belonging to another process.
- In addition to the implicit protection provided by virtual-to-physical address translation, all processors supporting Windows provide some form of hardware-controlled memory protection such as read/write, and so on. (The details of such protection vary according to the processor.) For example, code pages in the address space of a process are marked read-only and are protected from modification by user threads. Table 5-2 lists the memory protection options defined in the Windows API (See the documentation for the VirtualProtect, VirtualProtectEx, VirtualQuery, and VirtualQuery functions).

CHAPTER 5 Memory management 317

## TABLE 5-2 Memory-protection options defined in the Windows API

| Attribute | Description |
| --- | --- |
| PAGE_NOACCESS | Any attempt to read from, write to, or execute code in this region causes an access violation. |
| PAGE_READONLY | Any attempt to write to (on processes with no execute support, execute code in) memory causes an access violation, but reads are. |
| PAGE_READWRITE | The page is readable and not executable. |
| PAGE_EXECUTE | Any attempt to write to memory in this region causes an access violation, but execution is permitted. |
| PAGE_EXECUTE_READ* | Any attempt to write to memory in this region causes an access violation, but reads are permitted. |
| PAGE_EXECUTE_READWRITE* | The page is readable, writable, and executable. Any attempted access will succeed. |
| PAGE_WRITECOPY | Any attempt to write to memory in this region causes the system to give a private copy of the page. |
| PAGE_EXECUTE_WRITECOPY | Any attempt to write to memory in this region causes the system to give a private copy of the page. Reading and executing code in this region is permitted. (No copy is made in this case.) |
| PAGE_GUARD | Any attempt to read from or write to a guard page raises an EXCEPTION_PAGE_GUARD status. Guard pages can then be specified with any of the page protections listed in this table. |
| PAGE_NOCACHE | This uses physical memory that is not cached. This is not recommended for general usage; it is useful for device drivers—for example, mapping a video buffer with caching |
| PAGE_WRITECOMBINE | This enables combined memory accesses. When the processor does not cache writes (possibly significantly more memory traffic than if memory were cached), it tries to aggregate write requests to optimize performance. For example, if multiple writes are made to the same address, only collapsed into a single line. Separate writes to different addresses may be delayed—this is not typical for general applications, but is useful for device drivers—for example, mapping a video buffer as written |
| PAGE_TARGETS_INVALID and PAGE_TARGETS_NO_UPDATE (Windows 10 and Windows Server 2016) These values control Control Flow Guard (CFG) for executable code in these pages. These constants have the same value but are used in different calls, essentially acting as a proxy. PAGE_TARGETS_NO_UPDATE indicates that direct calls should fail but allows to change the page range without updating CFG state. See "Chapter 7, Security", for more information on CFG. No execute is supported on processes that have the necessary hardware support (for example, x64 processors) but not in older x86 processors. If unsupported, "execute" translates to "read." |

- Shared memory objects have Standard access lists (ACLs) that are checked when processes attempt to open them, limiting access of shared memory to processes with the proper rights. Access also comes into play when a thread creates a section to a mapped file. To create this, the thread must have at least read access to the underlying file or the operation will fail.

Once a thread has opened a handle to a section, its actions are still subject to the memory manager and the hardware-based page protections described above. A change can affect the page-level protection on virtual pages in a section if that does not violate the permissions in the ACL for that section object. For example, the memory manager allows a thread to change the pages of a page-only section to copy-on-write access have read/write access. The copy-on-write access is permitted because it has no effect on other processes sharing the data.

CHAPTER 5 Memory management 318

## Data Execution Prevention

Data Execution Prevention (DEP), or no-execute (NX) page protection, causes an attempt to transfer control to an instruction in a page marked as "no execute" to generate an access fault. This can prevent certain types of malware from exploiting bugs in the system through the execution of code placed in a data page such as the stack. DEP can also catch poorly written programs that do not correctly set permissions on pages they intend to execute. If an attempt is made in kernel mode to execute a page marked as "no execute," the system will crash with the bug check EXECUTE_OF_NOEXECUTE_MEMORY (0FC). (See Chapter 15, "Crash analysis," in Part 2 for an explanation of these codes) If this occurs in user mode, a STATUS_VIOLATION (0xC0000005) is delivered to the thread attempting the illegal reference. If a process allocates memory that needs to be executable, it must explicitly mark such pages by specifying the PAGE_EXECUTE, PAGE_EXECUTE_READ, PAGE_EXECUTE_READWRITE, and PAGE_EXECUTE_WRITECOPY flags on the page-granularity memory allocation functions.

On 32-bit systems that support DEP, bit 63 in the page table entry (PTE) is used to mark a page as non-executable. Therefore, the DEP feature is available only when the processor is running in Physical Address Extension (PAE) mode, which page table entries are only 32 bits wide. (See the x86 virtual address translation in this chapter) Thus, support for hardware on 32-bit systems requiring the PAE kernel (%SystemRoot%\System32\ntnl.exe), is currently the supported kernel on x86 systems.

On ARM systems, DEP is set to AlwaysOn.

On 64-bit Windows, execution protection is always applied to all 64-bit processes and device drivers which can be disabled by setting the BCD option to AlwaysOff. Execution protection for 32-bit processes depends on system configuration settings, described shortly. It applies to stacks (both user and kernel mode), user-mode pages not marked as executable, the kernel paged pool, and the kernel pool. For a description of kernel memory pools, see the section "Kernel-mode heaps (system pools)." However, on 32-bit Windows, execution protection is only applied to thread stacks and user-mode pages, not to the paged and session pool.

The application of execution protection for 32-bit processes depends on the value of the BCD option. To change the settings, open the Data Execution Prevention in the Options dialog box (see Figure 5-3). To open this dialog box, right-click Computer, select Properties, click Advanced Settings, and choose Performance Settings). If you configure no-execution protection in the Options dialog box, the BCD option is set to the appropriate value. Table 5-3 lists 32-bit applications that are excluded from execution protection under HKLM\Software\Windows NT\CurrentVersion\AppCompatFlags\Keys, with a value being the full path of the executable and the data set to 1DisableUI.

CHAPTER 5 Memory management 319
