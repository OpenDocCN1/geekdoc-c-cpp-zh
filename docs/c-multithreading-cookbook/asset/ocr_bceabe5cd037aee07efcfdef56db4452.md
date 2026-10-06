# The Concepts of Process and Thread

The other important concept besides process is a thread of execution, which is usually called thread. The thread is the lowest unit that can be scheduled for execution on the CPU. In another words, the process itself cannot get CPU time, only one of its threads can. The thread saves information about CPU registers with its working variables, along with the stack. The stack contains data related to functions call - with one frame for each function called but not yet returned from. A thread can be executed on the CPU, not a process. However, a process must have at least one thread, which is usually called main thread, so when we say that a process is executing on the CPU, we are referring to the 'process' main thread.

Processes are used to group processes together, threads are the entities scheduled for execution on the CPU. It is important to understand that a thread allows multiple executions to take place in the same process environment. Having multiple threads running in parallel in a single process context is the same as having multiple processes running in parallel on one computer. The term "multithreading" is used to describe the situation where multiple threads are running in the context of the single process.

In the following figure, we see three processes:

| Process 1 | Process 2 | Process 3 |
| --- | --- | --- |
| User space | | | |
| Kernel space | Kernel | |

In the following figure, we see a single process with three threads of control. Although in both cases we have three threads, in the first figure, each of the threads operates in a different address space, whereas in the second figure, all the three threads share the same address space.