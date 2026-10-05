| Thread Control Block (TCB) |
| Thread Creation and Exit times |
| Thread ID and Parent Process ID |
| Process this thread belongs to | EPROCESS |
| Thread Flags |
| Access Token | TOKEN |
| Thread Start Address |
| Impersonation Information |
| Pending I/O requests | IRP |
| Timer Information |
| ALPC Message Information |
| Thread List Entry | ETHREAD |
| Thread Lock |
| Exit Code |
| Energy consumption values (Win 10) |
| CPU Set information (Win 10) |

FIGURE 4-1 Important fields of the executive thread structure (ETHER).

| Dispatcher Header |
| Thread Environment Block (TEB) | TEB |
| Kernel Time and User time |
| System Service Table Pointer (x86) | System Service Table |
| Freeze Count and Suspend Count | W32THREAD |
| Win32 Thread Object |
| Parent Process | KPROCESS |
| Stack Information |
| Scheduling Information |
| Trap Frame |
| Synchronization information |
| Wait Block |
| List of objects thread is waiting on |
| List of Pending APCs |
| Thread List Entry | KTHREAD |

FIGURE 4-2 Important fields of the kernel thread structure (KTHREAD).

The Windows subsystem process (Csrss) maintains a parallel structure for each thread created in a Windows subsystem application, called the CSR_THREAD. For threads that have called a Windows subsystem USER or GDI function, the kernel-mode portion of the Windows subsystem (Win32k.sys) maintains a per-thread data structure (w32THREAD) that the KTHREAD structure points to.

CHAPTER 4 Threads 195