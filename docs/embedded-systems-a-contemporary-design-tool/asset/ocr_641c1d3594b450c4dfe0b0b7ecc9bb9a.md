processes are concurrently executing in memory, an errant pointer or stack error can easily result in memory owned by other processes being overwritten.

The system software must restrict the range of addresses that are accessible to the executing process. A process (thread) trying to access memory outside its allowed range should be immediately stopped before it can inflict damage on memory belonging to other processes. One means by which such restrictions are enforced is through the concept of privilege level.

Processes are segregated into those that have supervisor mode capability and those that have user mode capability. User mode limits the subset of instructions that a process can use. To be able to access the entire memory space requires supervisory mode access.

Processes with a low (user mode) privilege level are simply not allowed to perform certain kinds of memory accesses or to execute certain instructions. When a process attempts to execute such restricted instructions, an interrupt is generated and a supervisory program with a higher privilege level decides how to respond. The higher (supervisory mode) privilege level is generally reserved for supervisory or administration types of tasks that one finds delegated to the operating system or other such software. Processes with such privilege have access to any firmware and can use any instructions within the microprocessor's instruction set as we see in the diagram of the processor's firmware address space in Figure 11.8.

![](bbox=[0.352, 0.426, 0.648, 0.686])

# Figure 11.8 Address Space Access Privileges

# 11.6.2 Process-Level Management

+   * **child processes** A process may create or spawn child processes. When doing so, that parent process may choose to give a subset of its resources to each of the children. The children are separate processes and each has its own data address space, data, status, and stack. The code portion of the address space is shared.
+   * **multiple threads** A process may create multiple threads. When doing so, that parent process shares most of its resources with each of the threads. These are not separate processes but separate threads of execution within the same process. Each thread will have its own stack and status information.