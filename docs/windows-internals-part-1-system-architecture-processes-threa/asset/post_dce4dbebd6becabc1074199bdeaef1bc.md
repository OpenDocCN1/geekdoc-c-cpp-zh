
- System-wide code and data System contains global operating system code and data visible by kernel-mode code regardless of which process is currently executing. System space consists of the following components:

- System code: This contains the OS image, HAL, and device drivers used to boot the system.
- Nonaged pool: This is the non-pageable system memory heap.
- Paged pool: This is the pageable system memory heap.
- System cache: This is virtual address space used to map files in the system cache. (See Chapter 11, "Startup and shutdown," in Part 2 for detailed information.)
- System page table entries (PTEs): This is the pool of PTEs used to map system pages such as I/O space, kernel stacks, and memory descriptor lists. You can see how many PTEs are available by using Performance Monitor to examine the value of the Memory: Free System Page Table entries.
- System working set lists: These are the working set list structures that describe the three working system sets: cache, paged pool, and system PTEs.
- System mapped views: This is used to map Win32.sys, the loadable kernel-mode part of the Windows subsystem, as well as kernel-mode graphics drivers it uses. (See Chapter 2 for more information on Win32.sys.)
- Hyperspace is a special region used to map the working set list and other-process data that doesn't need to be accessible in arbitrary process context. Hyperspace is also used to temporarily map physical pages into the system space. One example of this is invalidating page table entries in processes other than the current one, or when a page is removed from the standby list.
- Crash dump information: This is reserved to record information about the state of a system crash.
- HAL usage: This is system memory reserved for HAL-specific structures.

Now we've described the basic components of the virtual address space in Windows, let's examine the system layout on the x86, ARM, and x64 platforms.

## x86 address space layouts

By default, each user process on 32-bit versions of Windows has a 2 GB private address space. The operating system takes the remaining (2 GB). However, for x86, the system can be configured with the increases BCD option to permit user address spaces up to 3 GB. Two possible address layouts are shown in Figure 5-10.

The ability of a 32-bit process to grow beyond 2 GB was added to accommodate the need for 32-bit applications to keep more data in memory than could be done with a 2 GB address space. Of course, 64-bit systems provide a much larger address space.

## HAL Reserved (4 MB)

| Address | Description |
| :--- | :--- |
| FFC00000 | System Cache Paged Pool |
| C0C00000 | Non Paged Pool |
| C080000 | Hyperspace (4 MB) |
| C000000 | Process Page Tables (8 MB) |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_366_0.png)
![](img/ff0e6a9d867a3a6e9527eb1d946810fc_366_1.png)
![](img/ff0e6a9d867a3a6e9527eb1d946810fc_366_2.png)
![](img/ff0e6a9d867a3a6e9527eb1d946810fc_366_3.png)

FIGURE 5-1 x86 virtual address space layouts (2 GB on the left, 3 GB on the right).

For a process to grow beyond 2 GB of address space, the image file must have the IMAGE_FILE_LARGE_ADDRESS_AWARE flag set in the image header (in addition to the global increaseusersva setting). Windows reserves the additional address space for process the application won't see virtual addresses greater than 0xFFFFFFFF. Access to the additional virtual memory is opt-in because some applications assume they'll be at most 2 GB of the address space. Because the high bit of a pointer referencing an address below 2 GB is always zero (31 bits are needed to refer to a 2 GB address space), applications would use the high bit in their pointers as a flag for their other data—clearing it, of course, before referencing the data. If they run with a 3 GB address space, would inadvertently truncate pointers that have values greater than 2 GB, causing program errors, including possible data corruption. You set this flag by specifying the /LARGEADDRESSAWARE linker flag when building the executable. Alternatively, use the property in Visual Studio (choose Linker, select System, and click Enable Large Addresses). You can add the flag to an executable image even without building (no source code required) by using a tool as Edin.exe (part of the Windows SDK toolkit), assuming the file is not signed. This flag has no effect when running the application on a system with 2 GB user address space.

Several systems are marked as large address space so that they can take advantage of systems running with large process address spaces. These include the following:

- LSass.exe The Security Authority Subsystem
- Ininet.exe Internet Information Server
- Chkdsk.exe The Check Disk utility

CHAPTER 5 Memory management
