+   - Controlling access so that only users with proper authorization are allowed to access particular resources
+   - Making use of remote resources, which appears to be identical to the use of local resources
+   - Providing up-to-the-minute network documentation online

As was mentioned earlier, the key issue that distinguishes a network operating system from a distributed one is how aware the users are of the fact that multiple machines are being used. This visibility occurs in three primary areas: file system, protection, and program execution.

The important issue in file system is related to how a file is accessed on one system from another in a network. There are two important approaches to this problem.

**Running a special file transfer program** When connecting two or more systems together, the first issue that is faced is how to access the file system available on some other system. To deal with this issue, the user runs a special file transfer program that copies the needed remote file to the local machine, where it can then be accessed normally. Sometimes remote printing and mail is also handled this way.

**Specifying a pathname** The second approach in this direction is for programs on one machine to open files on another machine by providing a pathname, thereby indicating where the file is located.

Some examples of the network operating systems are: Linux, Windows 2000 server/2003 server.

# 5.7.6 Distributed Operating System

A distributed computing system consists of a number of computers that are connected and managed so that they automatically share the job-processing load among the constituent computers, or separate the job load, as appropriate, to particularly configured processors. Such a system requires an operating system that in addition to the typical stand-alone functionality, provides coordination of the operations and information flow among the component computers.

The networked and distributed computing environments and their respective operating systems are designed with more complex functional capabilities. In a network operating system the users are aware of the existence of multiple computers, and can login to remote machines and copy files from one machine to another. Each machine runs its own local operating system and has its own user or users.

A distributed operating system, in contrast, is one that appears to its users as a traditional uniprocessor system, even though it is actually composed of multiple processors. In a true distributed system, users should not be aware of where their programs are being run or where their files are located; that should all be handled automatically and efficiently by the operating system.

Network operating systems are not fundamentally different from single processor operating systems. They obviously need a network interface controller and some low-level software to drive them, as well as programs to achieve remote login and remote file access, but these additions do not change the essential structure of the operating systems.

True distributed operating systems require more than just adding a little code to a uniprocessor operating system, because distributed and centralized systems differ in critical ways. Distributed systems, for example, often allow a program to run on several processors at the same time, thus requiring more complex processor scheduling algorithms in order to optimize the amount of parallelism achieved.

# Advantages of distributed operating systems

Though the design and implementation are complex, there are certain advantages for which the distributed system is used. Some of these are given below.

**Major breakthrough in microprocessor technology** With microprocessors becoming very powerful and cheap compared to mainframes and minicomputers, it has become attractive to think about designing large systems consisting of small processors. These distributed systems clearly have a price/performance advantage over more traditional systems.

**Incremental growth** The second advantage is that if there is a need for 10 per cent more computing power, one should just add 10 per cent more processors. System architecture is crucial to the type of system growth. However, it is hard to increase computing power by 10 per cent for each user.

**Reliability** Reliability and availability can also be a big advantage. A few parts of the system can be down without disturbing people using the other parts. One of the disadvantages may be that unless one is very careful, it is easy for the communication protocol overhead to become a major source of inefficiency.

Now, let us discuss how the file system protection and program execution are supported in a distributed operating system.

# File system

The distributed operating system supports a single global file system visible from all machines. When this method is used, there is one directory for executable programs (in UNIX, it is the bin directory), one password file, and so on.

The convenience of having a single global namespace is obvious. In addition, this approach means that the operating system is free to move files around machines to keep all the disks generally full and busy and that the system can maintain replicated copies of files if it chooses. The user of the program must specify the machine name as the system cannot decide on its own to move a file to a new machine. However, the user visible name, which is used to access the file, would change.