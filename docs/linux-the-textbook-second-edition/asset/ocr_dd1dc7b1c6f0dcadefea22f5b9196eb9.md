as its *address space*. The kernel ensures that no process accesses an area of memory that does not belong to its address space. The kernel maintains areas in the main memory that are free to be allocated to processes. The kernel code that performs this task is called the *free space manager*. When a program is to be loaded in the main memory, the free space manager allocates adequate space for it, and the *loader* loads the program into this space. The kernel also records where all the processes reside in the memory so that, when a process tries to access main memory space that does not belong to it, the kernel can terminate the process and give a meaningful message to the user. When a process terminates, the kernel deallocates the space allocated to the process and puts it back in the free space pool so that it can be reused.

# 1.7.2.4 Disk Management

The kernel is also responsible for maintaining free and used disk space and for the orderly and fair allocation and deallocation of disk space. It decides where and how much space to allocate to a newly created file. The kernel code that performs this task is known as the *disk storage manager*. Also, the kernel performs *disk scheduling*, deciding which request to serve next when multiple requests for file read, write, and so on arrive for the same disk.

# 1.7.3 System Call Interface

The system call interface layer contains entry points into the kernel code. Because the kernel manages all system resources, any user or application request that involves access to any system resource must be handled by the kernel code. However, user processes must not be given open access to the kernel code for security reasons so that user processes can invoke the execution of kernel code. Linux provides several openings, or function calls, into the kernel, known as *system calls*. There are numerous system calls that deal with the manipulation of processes, files, and other system resources. These calls are well tested, and most of them have been used for several years, so their use poses much less of a security risk than if any user code was allowed to perform the task.

# 1.7.4 Language Libraries

A *language library* is a set of prewritten and pretested functions in a programming language available to programmers for use with the software that they develop. The availability and use of libraries save time because programmers do not have to write these functions from scratch. This layer contains libraries for several languages, including C, C++, C#, Java, Perl, and Python. For the C language, for example, there are several libraries, including a string library (which contains functions for processing strings, such as a function for comparing two strings) and a math library (which contains functions for mathematical operations, such as finding the cosine of an angle).

As we stated earlier in this chapter, the libraries and system call interface form what is commonly known as the API. In other words, programmers who write software in a language such as C can use in their code the prewritten functions available in the various C libraries and system calls.

# 1.7.5 Linux Shell

The *Linux shell* is a program that starts running when you log on and interprets the commands that you enter. The most popular shells are the Bourne Again shell (bash, the default shell in all major distributions of Linux), Bourne shell (sh), C shell (csh), TC shell (tcsh), and Korn shell (ksh). We show the usage of shell commands in all of the core chapters of this book, and shell scripting in Chapters 12 and 13 for bash, and Chapters W29 and W30 for the TC shell.

# 1.7.6 Applications

The application layer contains all the applications (tools, commands, and utilities) that are available for your use. A typical Linux system contains hundreds of applications; we discuss the most useful and