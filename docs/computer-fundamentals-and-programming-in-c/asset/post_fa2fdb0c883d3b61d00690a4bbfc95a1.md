
## CHAPTER 5 Basic Concepts of Operating Systems

### LEARNING OBJECTIVES

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_87_0.png)

After studying this chapter, the readers will be able to

- explain the basic role of an operating system in modern-day computers
- explain the general functions and components of an operating system
- discuss the interfacing between the operating system and application program or the user
- trace the history of the development of operating systems
- explain the different types of operating systems
- get an overview on some operating systems such as UNIX and MSDOS

### 5.1 INTRODUCTION

Without software, a computer is basically a useless equipment. With software, a computer can store, process, and retrieve information and engage in many other valuable activities. Computer software can be divided roughly into two parts: system programs, which manage the operation of the computer itself, and application programs, which perform the actual work the user wants. The most important system program is the operating system (OS) that controls all the computer resources and provides the base upon which the application program can be written.

A modern computer system consists of one or more processors, main memory, disk drives, printers, keyboard, network interfaces, and other input/output devices. It is a complex system. Writing programs correctly is an extremely difficult job. If every programmer had to be concerned with how the disk drives work, and with all things that could go wrong when reading a disk, it is unlikely that many programs would be written at all.

Some way had to be found to shield programmers from the complexity of the hardware. The way that has evolved gradually is to put a layer of software on top of bare hardware to manage all the parts of the system. This layer of software is the operating system.

This is shown in Fig. 5.1. At the bottom lies the hardware. It is composed of two or more layers. The lowest layer contains physical devices consisting of integrated circuit chips, wires, power supplies, cathode ray tube (CRT) or LCD screen and similar physical devices.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_88_0.png)

**Fig. 5.1** The software–hardware layers in a computer

Next comes primitive software that directly controls these devices. This software is called a micro-program and is usually located in a read only memory. The set of instructions that the micro-program interprets defines the machine language. In this layer, input/output devices are controlled by loading values into special device registers. The layer above is the operating system. One of the major functions of the operating system is to hide all this complexity and give the programmer a more convenient set of instructions to work with. Above the operating system is the rest of the system software consisting of command interpreter (shell), window system, compilers, editors, and similar application independent programs.

Finally, above the system programs come the application programs. These programs are purchased or written by users to solve their particular problems or for specific purposes, for example, word processing, spreadsheets, engineering calculations, games, etc.

### 5.2 INTRODUCTION TO OPERATING SYSTEM

An operating system is a collection of programs that acts as an interface between the user of a computer and the computer hardware. In fact, it provides an environment in which a user may execute programs.

An operating system is an important part of almost every computer system that comprises these three main components:

- The hardware (memory, CPU, arithmetic-logic unit, various storage devices, I/O, peripheral devices, etc.)
- Systems programs (operating system, compilers, editors, loaders, utilities, etc.)
- Application programs (database systems, business programs, etc.)

The basic resources of a computer system are provided by its hardware, software, and data. The hardware provides the basic computing resources while the application programs define the way resources are used to solve the computing problems with the data. The operating system controls and coordinates the use of all the hardware among the various system programs and application programs for the various users. It, thus, provides an environment within which other programs can do useful work.

An operating system can be viewed as a resource allocator. A computer system has many resources (hardware and software) that may be required to solve a problem: CPU time, memory space, files storage space, input/output devices, etc.

Viewing the operating system as a resource manager, each manager must do the following:

- Keep track of the resources
- Enforce policy that determines who gets what, when, and how much
- Allocate the resources
- Reclaim the resources

As the manager of these resources, the operating system allocates them to specific programs and users as necessary for their tasks. Since there may be many, possibly conflicting requests for resources, the operating system must decide which requests are allocated resources to operate the computer system fairly and efficiently.

An operating system is also a control program. It controls the execution of user programs to prevent errors and improper use of the computer. Therefore, it may be defined as follows: An operating system (OS) refers to the software on a computer that lets it run applications, control peripherals, and communicate with other computers.

> **Note**
>
> - Without software, a modern-day computer is unusable. Software comprising operating system, programming language compilers, etc. are essential to provide an 'user-friendly' interface to the user.
> - An operating system is a software that runs applications, manages all resources like memory and peripherals and communicates with other computers.

### 5.3 FUNCTIONS OF AN OPERATING SYSTEM

An operating system has the following functions.

### Process management

The CPU executes a large number of programs. A process is a program in execution. In general, a process will need certain resources such as CPU time, memory, files, and I/O devices to accomplish its task. These resources are given to the process when it is created. It must be noted that a program by itself is not a process; a program is a passive entity, while a process is an active entity. Two processes may be associated with the same program; they are nevertheless considered two separate execution sequences.

Therefore, a process is the unit of work in a system. Such a system consists of a collection of processes, some of which are operating system processes that execute system code, with the rest being user processes that execute user code. All these processes can potentially execute concurrently.

The operating system is responsible for the following activities with respect to process management:

- The creation and deletion of user and system processes
- The suspension and resumption of processes
- Keep track of the resources (processors and the status of processes). Allocate the resources to a process by setting up the necessary hardware
- Reclaim the resources when the process relinquishes processor usage, terminates, or exceeds the allowed amount of usage
- The provision of mechanisms for process synchronization—decide which process gets the processor, when, and for how much time
- The provision of mechanisms for deadlock handling

### Memory management

**Primary memory management** Memory is central to the operation of a modern computer system. Memory is a large array of words or bytes, each with its own address. Interaction is achieved through a sequence of reads or writes of specific memory address. The CPU fetches data from and stores it in memory.

In order that a program be executed, it must be loaded into memory. As the program executes, it accesses program instructions and data from memory by accessing memory locations.

In order to improve both the utilization of CPU and the speed of the computer's response to its users, several processes must be kept in the memory. There are many algorithms for allocation of memory space to different processes active concurrently and the choice of any particular algorithm depends on the particular situation. Selection of a memory management scheme for a specific system depends upon many factors, especially upon the hardware design of the system. Each algorithm requires its own hardware support.

The operating system is responsible for the following activities for fulfilling memory management functions.

- Keep track of the different parts of memory currently being used by various processes
- Decide which processes are to be loaded into memory when memory space becomes available
- Allocate and de-allocate memory space as needed

**Secondary memory management** The main purpose of a computer system is to execute programs. These programs, together with the data they access, must be in the main memory during execution. Since the main memory is too small to permanently accommodate all data and programs, the computer system must provide a secondary storage that is capable of providing large storage space to back up the main memory. Most modern computer systems use disks as the primary device for online storage of information, both programs and data. Most programs, such as compilers, assemblers, sort routines, and editors are stored on the disk and a copy of any of these is loaded into memory. The disk is thus used as both a source and destination while processing. Hence, the proper management of disk storage is of prime importance to a computer system.

There are few alternatives. Magnetic tape systems are generally too slow. In addition, they are limited to sequential access. These tapes are more suited for storing infrequently used files, where speed is not a primary concern.

The operating system is responsible for the following activities for accomplishing the disk management functions:

- Free space management
- Storage allocation
- Disk scheduling

### Device (I/O) management

One of the purposes of an operating system is to hide the peculiarities of specific hardware devices from the user. For example, in UNIX, the peculiarities of I/O devices are hidden from the user by the I/O system. The I/O system consists of:

- a buffer memory system
- a general device driver program
- drivers for specific hardware devices

Only the device driver program can handle the peculiarities of a specific device.

### File management

File management is one of the most visible services of an operating system. For convenient use of the computer system, the operating system provides a uniform logical view of information storage. The operating system extracts the physical properties of its storage devices to define a logical storage unit, the file. Files are mapped by the operating system onto physical devices.

A file is a collection of related information defined by its creator. Commonly, files contain programs (both source and object forms) and data. Data can be numeric, alphabetic, or alphanumeric. Files may be of free form, such as text files, or may be rigidly formatted. In general, a file is a sequence of bits, bytes, lines, or records whose meaning is defined by its creator and user.

The operating system implements the abstract concept of the file by managing mass storage device, such as tapes and disks. Also, files are normally organized into directories for easy use. Finally, when multiple users have access to files,
