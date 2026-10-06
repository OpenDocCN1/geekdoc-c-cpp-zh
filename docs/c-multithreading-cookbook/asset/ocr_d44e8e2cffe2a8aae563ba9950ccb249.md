# Managing Threads

In the following figure, we see one process with three threads loaded into the memory.
Its threads are ready to execute on the CPU:

![](bbox=[0.333, 0.198, 0.666, 0.413])

# There's more...

You should consider the creation of threads each time the program performs an asynchronous operation. For example, programs with multiple windows have much to gain from creating a thread for each window. Another example would be to use a modern word processor, such as Microsoft Word, with built-in automatic grammar checking. Here, one thread (or several) is responsible for responding to the activities of the keyboard, another thread to update the text on the screen, and another one to govern the regular updating of the spare version of the work file, and so on.

# Permissive versus preemptive multitasking

It is good for users to understand the current operating system's implementation regarding thread behavior, so we will give a short explanation regarding multitasking.

The earlier versions of the Windows operating system prior to Windows 2000 have worked on the permissive multitasking principle, while the newer versions of the Windows operating system are implemented on the preemptive multitasking principle.

In permissive multitasking, the operating system is relying on the fair share of resources. In other words, the applications return the control to the system, so that another process could get processor time as well.