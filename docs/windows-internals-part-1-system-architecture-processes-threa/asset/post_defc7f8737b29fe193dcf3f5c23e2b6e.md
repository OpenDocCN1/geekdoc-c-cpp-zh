
Drivers, on the other hand, the specific event name that the memory manager set up in the KernelObjects object directory. This is because notification is implemented by the memory manager signaling one of a globally named event objects it defines, shown in Table 5-18. When memory condition is detected, the appropriate event is signaled, waking up any waiting threads.

## **TABLE 5-18** Memory notification events

| Event Name | Description |
| --- | --- |
| HighCommitCondition | This event is set when the commit charge is near the maximum limit—in other words, memory usage is very high, very little space is available in physical memory or paging files, and the operating system cannot increase the size of its pages |
| HighMemoryCondition | This event is set whenever the amount of free physical memory exceeds the defined amount |
| HighNonPagedPoolCondition | This event is set whenever the amount of non-paged pool exceeds the defined amount |
| HighPagedPoolCondition | This event is set whenever the amount of p pool exceeds the defined amount |
| LowCommitCondition | This event is set when the commit charge is low relative to the current limit—in other words, memory usage is low and a lot of space is available in physical memory or paging files |
| LowMemoryCondition | This event is set whenever the amount of free physical memory falls below the defined amount |
| LowNonPagedPoolCondition | This event is set whenever the amount of free non-paged pool falls below the defined amount |
| LowPagedPoolCondition | This event is set whenever the amount of free paging pool falls below the defined amount |
| MaximumCommitCondition | This event is set when the commit charge is near the maximum limit—in other words, memory usage is very high, very little space is available in physical memory or paging files, and the operating system cannot increase the size or number of paging pages |
| MemoryErrors | This indicates that a bad page (non-zero page) has been detected. |

> Note: You can override the high and low memory values by adding the LowMemoryThreshold or HighMemoryThreshold DWORD registry value under HKLM\SYSTEM\ControlSet\Session Manager\Memory Management. This specifies the number of megabytes to use the low or high threshold. You can also configure the system to crash when a bad page is detected instead of signaling a memory error event by setting the PageValidationAction registry value in the same key to 1.

### **EXPERIMENT: Viewing the memory resource notification events**

to see the memory resource notification events, run WinObj from Sysinternals and click the KernelObjects folder. You will see both the low and high memory condition events shown in the pane on the right:

## Page frame number database

If you double-click each event, you can see how many handles and/or references have been made to the objects. See whether any processes in the system have requested memory resource notification, search the handle table for references to LowMemoryCondition or HighMemoryCondition. To do so, use Explorer Find menu (choose Find Handle or DLL) or use WinDbg. For a description of the handle table, see the section "Object manager" in Chapter 8 in Part 2.)

Several previous sections contrasted on the virtual view of a Windows process—page tables, PTEs, and VADs. The remainder of this chapter will explain how Windows manages physical memory, whereas working sets decide the resident pages owned by a process or the system, the PFN database describes the state of each page in physical memory. The page states are listed in Table 5-19.

## TABLE 5-19 Physical page states

| Status | Description |
| --- | --- |
| Active (also called) | The page is part of a working set (either a process working set, or a system working set), or it's not in any paging list (for example, a non-paged page) and a valid PTE usually points to it |
| Transition | This is a temporary state for a page that isn't owned by a working set and isn't on any paging list. A page is in this state when an I/O to it is progress. The PTE is encoded so that collided page faults can be recognized and handled properly. (Use of this term differs from the use of word; see the section on invalid PTEs. An invalid transition refers to a page on the standby or modified list.) |
| Standby | The page previously belonged to a working set but was removed or was prefetched/clustered directly into the standby list. The page was not modified if it was last written to disk. The PTE still refers to the physical page but it is marked invalid and in |

## TABLE 5-19 Physical page states (continued)

| Status | Description |
| --- | --- |
| Modified | The page previously belonged to a working set but was removed. However, the page was modified while it was in use and its contents haven't been written to disk or remote storage. The PTE still refers to the physical page but is marked invalid and in transition. It was worth writing to the store buffer before the physical page can be reused. |
| Modified no-write | This is the same as a modified except that the page has been marked so that the memory manager's modified page would not write to disk. The cache manager marks pages as modified no-write at the request of file writers. For example, NTFS uses this state for pages containing file metadata so that it can first ensure that transaction log entries are flushed to disk before the pages are written to disk. (NTFS transaction logging is explained in Chapter 13, "File systems," in Part 2.) |
| Free | The page is free without unspecified dirty data in it. For security reasons, these pages can be given as a user to a process without being initialized with zeros, or can be |
| Zeroed | The page is free and has been initialized with zeros. |
| Rom | The page is read-only. |
| Bad | The page has generated parity errors and cannot be used. |

The PFN database contains an array of structures that represent each physical page of memory. Figure 5-35 shows, the PFN database and its relationship to PTEs (and the PFN database for system- prototype PFNs point to the page). For prototype PFNs, they point back to.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_442.png)

Page list dynamics

Of the page states listed in Table 5-19, six are organized into linked lists so that the memory manager can quickly locate pages of a specific type. (Active/valid, transition pages, and "bad" pages.) Additionally, the standby state is associated with eight different lists ordered by priority. Figure 5-36 shows an example of how these entries are linked together.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_443.png)

In the next section, you'll find out how these linked lists are used to satisfy page faults and how pages move to and from various.

### **EXPERIMENT: Viewing the memory resource notification events**

you can use the MemInfo tool from the Windows Internals book to dump the size of the various lists by using the s flag. The following is the output from this command:

C:\Tools>MemInfo.exe -s
MemInfo v3.00 - Show PFN database
Copyright (C) 2007-2016 Alex Ionescu
www.alex-ionescu.com.

Initializing PFN List... Done
PFN Database Statistics
Zeroed: 4867 (19468 kb )
Free: 3076 (12304 kb)
Standby: 4669104 (1867416 kb)
Modified: 7845 (31380 kb)
ModifiedNoWrite: 117 (468 kb)
Active/Valid: 3677990 (14711960 kb)
Transition: 5 (20 kb)
Bad: 0 (0 kb)
Unknown: 1277 (5108 kb)
TOTAL: 8346281 (33457124 kb)

Using the kernel debugger image command, you can obtain similar information, although through this will take considerably longer to execute.

Figure 5-37 shows a state diagram for page frame transitions. For simplicity, the modified-no-free, bad and ROM lists aren't shown.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_444.png)

Page frames move between the paging lists in the following ways:

- When the memory manager needs a zero-initialized page to service a demand-zero page fault (reference to a page that is defined to be all zeroes or a user-mode committed private page that has never been accessed), it first attempts to get from the zero page list. If the list is empty, it gets one from the free page list. If the free list is empty, it goes to the standby list and zeroes that page.
