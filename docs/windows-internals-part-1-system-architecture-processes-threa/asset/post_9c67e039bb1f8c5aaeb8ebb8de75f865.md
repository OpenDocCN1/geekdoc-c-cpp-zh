
# Locking memory

In general, it's better to let the memory manager decide which pages remain in physical memory. However, there might be special circumstances when it might be necessary for an application or device driver to lock pages in physical memory. Pages can be locked in memory in two ways:

- Applications can use the VirtualLock function to lock pages in their working set. Pages locked using this mechanism remain in memory until explicitly unlocked or the process that locked them terminates. The number of pages a process can't exceed its minimum working set size minus eight pages. If a process needs more pages, it can increase its working set with the SetProcessWorkingSetSizeEx function, discussed later in this chapter in the section "Working management."
- Device drivers can use the ProbeAndLockPages, MLockPagableCodeSection, MLockPagableDataSection, or MLockPagableSectionByKernel-mode functions. Pages locked using this mechanism remain in memory until explicitly unlocked. The last of three APIs enforce no quota on the number of pages that can be locked in memory because the resident available page charge is obtained when the driver first calls. This ensures that it never causes a system crash due to overlocking. For the first API, page quotas must be obtained or the API will return a failure.

# Allocation granularity

Windows aligns each region of process address space to begin on an integral boundary defined by the value of system granularity, which can be retrieved from the Windows-SystemInfo or GetNativeSystemInfo functions. This value is 64 KB, a granularity that is used by the memory manager to efficiently allocate metadata (for example, VADs, bitmaps, and so on) to support various operations. In addition, if support were added for future processes with larger page sizes (for example, up to 64 KB) or virtually indexed caches that require system-wide physical-to-virtual page alignment, the risk of requiring changes to applications that made assumptions about allocation alignment would be reduced.

> Windows kernel-mode code isn't subject to the same restrictions. It can reserve memory on a single-page granularity (although this is not exposed to device drivers for the reasons detailed earlier). This level of granularity is primarily used to pack TE allocations densely. Because this mechanism is internal, this code can be changed if a future platform requires different values. For the purposes of supporting 16-bit and MS-DOS applications on x86 systems only, the memory manager provides the MEM_DOS_LIM flag to the MapViewOfEx API, which is used to force the use of single-page granularity.

Finally, when a region of address space is reserved, Windows ensures that the size and bound of the region is a multiple of the system page size, whatever that may be. For example, x86 systems use 4 KB pages, if you tried to reserve a region of memory 18 KB in size, the actual amount reserved on an x86 system would be 20 KB. If you specified a base address of 3 KB for an 18 KB region, the actual amount reserved would be 24 KB. Note that the VAD for the allocation would then be rounded to 64 KB alignment/length, thus making the remainder of it inaccessible.

# Shared memory and mapped files

As is true with most modern operating systems, Windows provides a mechanism to share memory among processes and the operating system. Shared memory can be defined as memory that is visible to more than one process or that is present in more than one process virtual address space. For example, if two processes use the same DLL, it would make sense to only share the referenced code pages for DLL into physical memory only once and share those pages between all processes that map the DLL, as illustrated in Figure 5-2.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_331_0.png)

FIGURE 5-2 Sharing memory between processes.

Each process would still maintain its private memory areas to store private data but the DLL code and unmodified data pages could be shared without harm. We'll explain later, this kind of sharing happens automatically because the code pages in executable images—EXE and DLL files, and several other types like screen savers (SCR), which are essentially DLLs under other names—are mapped execute-only and writable pages are mapped as copy-write. (See the "Copy-on-write" section in this chapter for more information.)

Figure 5-2 shows two processes, based on different images, that share a DLL mapped just once to physical memory. The memory (EXE) code itself is not shared in this case because the two processes run different images. The EXE code would be shared between processes that run the same image, as two or more processes running Notepad.exe.

The underlying primitives in the memory manager used to implement shared memory are called section objects, which are exposed as file-mapping objects in the Windows API. The internal structure and implementation of section objects are described later in this chapter in the section "Section objects."

This fundamental primitive in the memory manager is used to map virtual addresses whether in main memory, in the page file, or in some other file that an application wants to access as if it were in memory. A section can be opened by one process or by many. In other words, section objects don't necessarily equate to shared memory.

A section object can be connected to an open file on disk (called a mapped file) or committed memory (sections committed to memory are called page-backed sections because the pages are written to the paging file (as opposed to a mapped file) if demands on physical memory require it. (Because Windows can run with no paging file, page-backed sections might be in "backed" only by physical memory.) As shared committed pages are zero-filled when they are first accessed to ensure that no sensitive data is leaked. To create a section object, call the CreateFileMapping, CreateFileMappingFrom, or CreateFileMappingNuma function specifying a previously opened file (or INVALID_HANDLE_VALUE for page-backed section) and a security descriptor. If the section has a name, other processes can use it with OpenFileMapping or the CreateFileMapping functions. You can access section objects through either handle inheritance (by specifying the handle as inheritable when opening or creating the handle) or handle duplication (using DuplicateHandle). Device drivers can also manipulate section objects with the ZwSection, ZwMapViewSection, and ZwUnmapSection functions.

A section object can refer to files that are larger than fit in the address space of a process. (If the paging backs a section object, sufficient space must exist in the file and/or RAM to contain it.) To access a large section object, a process can map only the portion of the object it requires (a view of the section) by calling the MapViewOfEx, MapViewFileFromApp, MapViewFileNuma and then specifying the range to map. Mapping views permits to conserve address space because only the views of the section object needed at the time will be mapped into memory.

Windows applications can use mapped files to perform I/O by simply making them appear as data in memory within their address space. User applications are not the consumers of section objects; the image loader uses section objects to map executables, DLLs, and device drivers into memory, and the cache manager uses their access to data files. (For information on how the cache manager integrates with the memory manager, see Chapter 14 in Part 2.) The implementation of shared memory sections, in terms of address translation and the internal data structures, is explained in the "Section objects" later.

# EXPERIMENT: Viewing memory-mapped files

You can list the memory-mapped files in a process using Process Explorer. To do so, configure the lower pane to show the DLL view. (Open the View menu, select Lower Pane, and choose DLLs.) Note that this is more than just a list of DLLs—it represents every memory-mapped file in the process address space. Some of these DLLs, the image file (EXE) running, and additional entries might represent memory-mapped data files.

The following display from Process Explorer shows a Winbg using several memory mappings to access the memory dump file being examined. Like most Windows programs, (or one of the Windows DLLs it is using) is also using memory mapping to access a Windows data file Locale.nl, which is part of the internationalization support in Windows.
