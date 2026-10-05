Although threads have their own execution context, every thread within a process (in addition to the rest of the resources belonging to the process), meaning that all the threads in a process have full read-write access to the process virtual address space. Threads cannot accidentally reference the address space of another process, however, the other process makes available part of its private address space a shared memory section (called a file mapping object in the Windows API) or unless one process has the right to open another process to use process functions, as ReadProcessMemory and WriteProcessMemory (which a process's running with the same user account, and not inside an AppContainer or other type of sandbox, can get by unless the target process has certain protections).

In addition to a private address space and one more threads, each process has a security context and a list of handles to kernel objects such as files, shared memory sections, or one of the synchronization objects such as mutexes, events, or semaphores, as illustrated in Figure 1-2.

![](bbox=[0.323, 0.126, 0.521, 0.563])

**Figure 1-2** A process and its resources.

Each process's security context is stored in an object called an access token. The process access token contains the security identification and credentials for the process. By default, threads don't have their own access token, but they can obtain one, allowing threads to impersonate the security context of another process—including processes on a remote Windows system—without affecting other threads in the process. (See Chapter 7 for more details on process and thread security.)

The virtual address descriptors (VADS) are data structures that the memory manager uses to keep track of the virtual addresses the process is using. These data structures are described in more depth in Chapter 5.

# Jobs

Windows provides an extension to the process model called a job. A job object's main function is to allow the management and manipulation of groups of processes as a unit. A job object allows control of certain attributes and provides limits for the process or processes associated with the job. It also records accounting information for all processes associated with the job and for all processes that were associated with the job but have since terminated. In some ways, the job object compensates for the lack of a structured process tree in Windows—in many ways it is more powerful than a UNIX-style process tree.