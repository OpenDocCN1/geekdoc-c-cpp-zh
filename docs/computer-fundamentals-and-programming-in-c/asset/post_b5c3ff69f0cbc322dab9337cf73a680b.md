
When the user logs on, the kernel runs init and getty to check if the user is authorized and has the correct password. The kernel keeps track of all the programs being run, allots time to each running program, decides when one program stops and another program starts, assigns storage space for files, runs the shell program, and handles the transfer of information between the computer and the peripherals. In short, it provides the following functions:

- Process scheduling (process representation—structure, scheduling, and dispatching)
- Memory management
- Device management
- File management
- System call interface
- Process synchronization and inter-process communication
- Operator console interface

These functions are spread over a number of modules within the UNIX kernel. The utility programs and UNIX commands are not considered a part of the UNIX kernel, which consists of the layers closest to the hardware that are for the most part protected from the user. The kernel may be viewed with the help of a functional layer model (Fig. 5.3).

The kernel communicates directly with the hardware. When UNIX is adapted to a new machine, only the kernel has to be modified. The kernel does not deal directly with a user. It starts up a separate interactive program called a shell for each user, when the user logs on. The shell acts as an interface between the user and the system. The kernel serves as an interface between the shell, UNIX commands, and system hardware.

Every time a process is loaded and started up, a chunk of main memory is allocated for program code and data. Additionally, main memory is required for buffers, system databases, and stack space. The device management routines in this layer start and stop devices, check and reset status, and read and write data from and to devices. Similarly, the disk management routines access the disk drive, and perform the basic block, read, and write functions.

The next layer consists of all kernel services. This layer provides the mapping between the user-level requests and device driver-level actions. The user system call is converted to calls to the kernel service routines that perform requested services. These services consist of process creation and termination, I/O services, receive data functions, and file access and terminal handling services.

The system call interface layer converts a process operating in the user mode to a protected kernel mode process so that the program code can invoke kernel routines to perform system functions.

The uppermost layer consists of user processes running shells, UNIX commands, utility programs, and user application programs. User programs are protected from inadvertent writes by other users. They have no direct access to the UNIX kernel routines and all access is channelled through the system call interface. Additionally, user programs cannot directly access memory used by the kernel routines.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_100_0.png)

## Command Interpreter

This is a utility program and is called the shell. It interacts with the user and translates the user’s request into actions on the part of the kernel and the other utility (Fig. 5.4). Each user opens one shell on logging on. Different types of shells are available such as Bourne shell, C shell, and Korn shell.

- protection of file data
- the treatment of peripheral devices as files

The shell translates typed commands into action; therefore, it is termed as a command interpreter. The shell has a few built-in commands, but the majority of the commands are separate programs stored elsewhere in the system. When a command is typed through the keyboard, it is collected and delivered to the kernel by the shell.

## 5.8.3 The UNIX File System

The file system is one of the major subsystems of the operating system. It is responsible for storing information on disk drives and retrieving and updating this information as directed by the user or by a program. The UNIX operating system regards practically every assemblage of information as a file. The formal definition of a file is a string of characters. Often, it is desirable to organize UNIX files as a set of lines. Every line is terminated by a new line character.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_101_0.png)

**Fig. 5.4** The kernel–shell relationship

The files are identified by filenames that are kept in the file directory. Every user is allocated a personal file directory when the user’s login name and password are authorized.

The file system is organized as a tree with a single root node called root (/). Every non-leaf node of the file system structure is a directory of files, and files at the leaf nodes of the tree are either directories, regular files, or special device files.

Filenames may contain up to 256 characters. The characters may include almost any printable character except a blank. The name of a file is given by a pathname that describes how to locate the file in the file system hierarchy. The file system hierarchy allows an entry only through the root.

The UNIX file system is characterized by the following:

- a hierarchical structure
- consistent treatment of file data
- the ability to create and delete files
- dynamic growth of files

The internal representation of a file is given by a unique inode. Inode stands for index node. Every file has one inode, but it may have several names, all of which map into the same inode. Each name is called a link. An inode contains a description of the disk layout of the file data and other information such as (a) file owner, (b) access permissions, (c) access times, (d) file size, and (e) location of file’s data in the file system. The inode also contains (a) the time of the last modification of the file contents, (b) the time at which the file was last accessed, (c) the time at which the inode was changed (change permission), etc.

Processes access files by a well-defined set of system calls and specify a file by a character string that is a pathname. When a process refers to a file by name, the kernel parses the filename one component at a time and converts the filename to a file’s inode. The kernel then checks that the process has permission to search the directories in the path and eventually retrieves the inode for the file. The system’s internal name for the file is its i-number. When the following command is given:

```
ls -i
```

(The output obtained shows the i-number and the filename.)

| i-number | filename |
| --- | --- |
| 15768 | junk |
| 15274 | recipes |
| 15852 | x |

When a process creates a new file, the kernel assigns it an unused inode. Inodes are stored in the file system but the kernel reads them into an in-core inode table when manipulating the files. The kernel contains two other data structures: file table (global kernel structure) and user file descriptor table (per process).

### Types of files

The UNIX system has the following types of files:

- Ordinary files
- Directory files
- Special files

**Ordinary files** These are files that contain information entered by a user, an application program, or a system utility program. An ordinary file may contain text information (string of characters) and binary information (sequence of words). These files are also called byte streams.

An ordinary file is a string of bytes, stored on disk or on some other physical medium. There is no distinction between program files or data files. If all the bytes in the file represent printable characters, the file is termed a text file. It is often convenient to subdivide text files into lines, separated from each other with the new line character (ASCII 012 octal). The lines do not have fixed lengths.

**Directory files** These are the files that manage the cataloging of the file system. A directory is a file that contains information about a group of files contained in the directory. A directory can contain sub-directories. Files can be accessed by selecting the corresponding directory or pathname.

The directory is defined as a file whose data is a sequence of entries, each consisting of an inode number and the name of a file, contained in the directory. A pathname is defined as a null terminated character string divided into separate components by the character slash, i.e., ‘/’. Every component in the pathname except the last one must be the name of a directory. The last component may be a directory or a non-directory file.
