
It may be desirable to control the permission to users for accessing, creating, and amending the files.

The operating system is responsible for the following activities for accomplishing the file management functions:

- Creation and deletion of files
- Creation and deletion of directories
- Support of primitives for manipulating files and directories
- Mapping of files onto disk storage
- Backup of files on stable (non-volatile) storage

## Protection

Protection refers to a mechanism for controlling the access of programs, processes, or users to the resources defined by a computer and the controls to be imposed, together with some means of enforcement. For example, the various processes in an operating system must be protected from each other’s activities. The memory address management system ensures that a process can only execute within its own address space. The control mechanism ensures that no process can gain control of the CPU without the latter being relinquished by another process. Finally, no process is allowed to directly communicate with any I/O, to protect the integrity of the data from or to various peripheral devices.

Protection can improve reliability by detecting latent errors at the interfaces between component subsystems. Early detection of interface errors can often prevent contamination of a healthy subsystem by one that is malfunctioning. An unprotected resource cannot defend itself against use or misuse by an unauthorized or incompetent user.

## 5.4 COMPONENTS OF AN OPERATING SYSTEM

In general there are two main components of an operating system: command interpreter and kernel.

### Command interpreter

Command interpreter is one of the most important components of an operating system. It is the primary interface between the user and the rest of the system.

Many commands are given to the operating system by control statements. A program that reads and interprets control statements is automatically executed. This program is variously called (a) the control card interpreter, (b) the command line interpreter, (c) the shell (in UNIX), and so on. Its function is quite simple: it gets the command statement and executes it.

The command statements deal with process management, I/O handling, secondary storage management, main memory management, file system access, protection, and networking.

### Kernel

Kernel is a core part of the operating system and is loaded into the main memory when it starts up. It is the core library of functions that the operating system “knows”. In the kernel, there are the functions and streams to communicate with the system’s hardware resources.

The kernel provides the most basic interface between the machine and the rest of the operating system. The kernel is responsible for the management of the central processor. It includes the dispatcher that allocates the central processor to a process, determines the cause of an interrupt and initiates its processing, and makes some provision for communication among the various systems and user tasks currently active in the system.

The main functions of the kernel are as follows:

- To provide a mechanism for the creation and deletion of processes
- To provide CPU scheduling, memory management, and device management for these processes
- To provide synchronization tools so that the processes can synchronize their actions
- To provide communication tools so that processes can communicate with each other

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_90_0.png)

The kernel-based design is often used for designing the operating system. The kernel, more appropriately called the nucleus, is a collection of primitive facilities over which the rest of the operating system is built and the latter uses the functions provided by the kernel (see Fig. 5.2). Thus, a kernel provides an environment to build an operating system in which the designer has considerable flexibility because policy and optimization decisions are not made at the kernel level. An operating system is an orderly growth of software over the kernel, where all decisions regarding process scheduling, resource allocation, execution environment, file system, resource protection, etc. are made.

Consequently, a kernel is a fundamental set of primitives that allows the dynamic creation and control of processes as well as communication among them. Thus, the kernel only supports the notion of processes and does not include the concept of a resource. However, as operating systems have matured in functionality and complexity, more functionality has been related to the kernel. A kernel should contain a minimal set of functions that is adequate to build an operating system with a given set of objectives.

There are two different methodologies for designing a kernel: monolithic kernels and microkernels.

The monolithic kernel is the design that is used in operating systems such as Windows and Linux. In this case, the kernel is a set of tightly integrated packages that understand and handle the complete hardware of the machine.

An error in the monolithic kernel will bring the whole system crashing down. Since the integration level among the components of the kernel is very high, it is potentially difficult to distinguish and manage smaller parts separately.

A microkernel, on the other hand, takes a different approach. Microkernels usually provide only minimal services such as defining memory address spaces, interprocess communication methods, and process and thread management. All other features, such as hardware management or I/O locking and sharing, are implemented as processes running independently of the microkernel.

A microkernel does not suffer from the same ailments as monolithic kernels. If a certain subprocess of the kernel crashes, it is still possible to save the whole system from a crash by restarting the service which caused the error.

It was claimed that microkernels would revolutionize the way operating systems are designed. But no such thing has happened. Apparently, the improvements were not significant enough to force the majority of operating systems to use this approach. There are only a few operating systems today that use the microkernel approach, for instance, Mach microkernel (used in OS X), BeOS, and AIX.

## 5.5 INTERACTION WITH OPERATING SYSTEM

Broadly speaking, there are two ways to interact with an operating system.

- By means of *operating system calls* in a program
- Directly by means of *operating system commands*

### System calls

System calls provide the interface between a running program and the operating system. These calls are generally available as assembly language instructions, and are usually listed in the manuals used by assembly language programmers. Some systems may allow system calls to be made directly from a high-level language program, in which case the calls normally resemble predefined function or subroutine calls. They may generate a call to a special run-time routine that makes the system call, or the system call may be generated directly in-line. The C language allows system calls to be made directly. Some PASCAL systems also provide an ability to make system calls directly from a PASCAL program to the operating system. System calls can be roughly grouped into five major categories: *process control, file manipulation, device manipulation, information maintenance, and communications*.

A user program makes good use of the operating system. All interactions between the program and its environment must occur as the result of requests from the program to the operating system.

### Operating system commands

Apart from system calls, users may interact with the operating system directly by means of commands. For example, if the user wants to list files or sub-directories in MS-DOS, the *DIR* command is invoked. In either case, the operating system acts as an interface between users and the hardware of a computer system. The fundamental goal of a computer system is to solve user problems. The computer hardware is designed towards this goal. Since the bare hardware alone is not very easy to use, programs (software) are developed. These programs require certain common operations, such as controlling peripheral devices. The common functions of controlling and allocating resources are then brought together into one piece of software, the operating system.

**Note**

- The operating system primarily manages processes, memory, input/output devices, and files and ensures proper control on all the resources to keep them from interfering with each other.
- The *command interpreter* and the *kernel* are the two main components of the operating system.
- The *system calls* and the *operating system commands* are the two ways of interacting with the operating system.

## 5.6 HISTORY OF OPERATING SYSTEMS

To understand what operating systems are and what they do, consider how they have developed over the last 30 years. By tracing that evolution, the common elements of operating systems can be identified as well as how and why they developed as they are now.

Operating systems and computer architecture have a great deal of influence on each other. Operating systems were developed to facilitate the use of the hardware. As operating systems were designed and used, it became obvious that changes in the design of the hardware could simplify it. This short historical review discusses how the introduction of
