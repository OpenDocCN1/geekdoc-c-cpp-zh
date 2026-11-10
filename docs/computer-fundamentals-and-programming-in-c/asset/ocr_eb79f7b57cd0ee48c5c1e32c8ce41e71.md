it may be desirable to control the permission to users for accessing, creating, and amending the files.

The operating system is responsible for the following activities for accomplishing the file management functions:

+   - Creation and deletion of files
+   - Creation and deletion of directory
+   - Support of primitives for manipulating files and directories
+   - Mapping of files onto disk storage
+   - Backup of files on stable (non-volatile) storage

# Protection

Protection refers to a mechanism for controlling the access of programs, processes, or users to the resources defined by a computer and the controls to be imposed, together with some means of enforcement. For example, the various processes in an operating system must be protected from each other’s activities. The memory address management system ensures that a process can only execute within its own address space. The control mechanism ensures that no process can gain control of the CPU without the latter being relinquished by another process. Finally, no process is allowed to directly communicate with any I/O, to protect the integrity of the data from or to various peripheral devices.

Protection can improve reliability by detecting latent errors at the interfaces between component subsystems. Early detection of interface errors can often prevent contamination of a healthy subsystem by one that is malfunctioning. An unprotected resource cannot defend itself against use or misuse by an unauthorized or incompetent user.

# 5.4 COMPONENTS OF AN OPERATING SYSTEM

In general there are two main components of an operating system: component interpreter and kernel.

# Command interpreter

Command interpreter is one of the most important components of an operating system. It is the primary interface between the user and the rest of the system.

Many commands are given to the operating system by control statements. A program that reads and interprets control statements is automatically executed. This program is variously called (a) the control card interpreter, (b) the command line interpreter, (c) the shell (in UNIX), and so on. Its function is quite simple: it gets the command statement and executes it.

The command statements deal with process management, I/O handling, secondary storage management, main memory management, file system access, protection, and networking.

# Kernel

Kernel is a core part of the operating system and is loaded on the main memory when it starts up. It is the core library of functions; the operating system “knows”. In the kernel, there are the functions and streams to communicate with the system’s hardware resources.

The kernel provides the most basic interface between the machine and the rest of the operating system. The kernel is responsible for the management of the central processor. It includes the dispatcher that allocates the central processor to a process, determines the cause of an interrupt and initiates its processing, and makes some provision for communication among the various systems and user tasks currently active in the system.

The main functions of the kernel are as follows:

+   - To provide a mechanism for the creation and deletion of processes
+   - To provide CPU scheduling, memory management, and device management for these processes
+   - To provide synchronization tools so that the processes can synchronize their actions
+   - To provide communication tools so that processes can communicate with each other

![](bbox=[0.559, 0.494, 0.89, 0.686])

The kernel-based design is often used for designing the operating system. The kernel, more appropriately called the nucleus, is a collection of primitive facilities over which the rest of the operating system is built and the latter uses the functions provided by the kernel (see Fig. 5.2). Thus, a kernel provides an environment to build an operating system in which the designer has considerable flexibility because policy and optimization decisions are not made at the kernel level. An operating system is an orderly growth of software over the kernel, where all decisions regarding process scheduling, resource allocation, execution environment, file system, resource protection, etc. are made.

Consequently, a kernel is a fundamental set of primitives that allows the dynamic creation and control of process as well as communication among them. Thus, the kernel only