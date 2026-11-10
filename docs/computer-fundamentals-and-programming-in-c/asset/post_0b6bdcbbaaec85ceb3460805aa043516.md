
capacity far smaller than those of hard disks. A CD-ROM or DVD-ROM is another portable secondary memory device. CD stands for Compact Disc. It is called ROM because information is stored permanently when the CD is created. Devices for operating storage mediums are known as drives. Most of the drives used for secondary memory are based on electro-mechanical technology. Mechanical components move much more slowly than do electrical signals. That’s why access to secondary memory is much slower than access to main memory.

The **floppy disk** is a thin, round piece of plastic material, coated with a magnetic medium on which information is magnetically recorded, just as music is recorded on the surface of plastic cassette tapes. The flexible floppy disk is enclosed inside a sturdier, plastic jacket to protect it from damage. The disks used in personal computers are usually 3½ inches in diameter and can store 1.44 MB of data. Earlier PCs sometimes used 5¼ inch disks. The disks store information and can be used to exchange information between computers. The floppy disk drive stores data on and retrieves it from the magnetic material of the disk, which is in the form of a disk. It has two motors: one that rotates the disk media and the other that moves two read-write heads, each on either surface of the disk, forward or backward.

Floppy Disk Drive

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_30_0.png)

A **hard disk** is a permanent memory device mounted inside the system unit. Physically, a hard disk consists of one or more metal (sometimes aluminum) platters, coated with a metal oxide that can be magnetized. The platters are all mounted on a spindle, which allows them to spin at a constant rate. Read/write heads are attached to metal arms and positioned over each of the platter surfaces. The arms can move the read/write heads radially inwards and outwards over the surfaces of the platters (see Fig. 1.5). Data and programs are stored on the hard disk by causing the write heads to make magnetic marks on the surfaces of the platters. Read heads retrieve the data by sensing the magnetic marks on the platters. The surface of each platter is divided into concentric rings called tracks. The tracks form concentric circles on the platter’s surface. Each track is divided into a certain number of sectors. A sector is capable of generally 512 bytes or sometimes 1,024 bytes of data. The head is mounted on an arm, which moves or seeks from track to track. The vertical group of tracks at the same position on each surface of each platter is called a cylinder. Cylinders are important, because all heads move at the same time. Once the heads arrive at a particular track position, all the sectors on the tracks that form a cylinder can be read without further arm motion. The storage capacity of a hard disk is very large and expressed in terms of gigabytes (GB). The data that is stored on the hard disk remains there until it is erased or deleted by the user.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_30_1.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_30_2.png)

Fig. 1.5  Hard disk organization

The hard disk drive provides better performance and becomes mandatory for computer systems for the following reasons:

- Higher capacity of data storage
- Faster access time of data
- Higher data transfer rates
- Better reliability of operation
- Less data errors or data loss

A CD is a portable secondary storage medium. Various types of CDs are available: CD-R and CD-RW. CD-R drives are used to create and read both CD-R and CD-RW discs. Once created (i.e. when it has been “burned”), data stored on CD-R (CD-Recordable) disc can’t be changed. On the other hand, a CD-Rewritable (CD-RW) disc can be erased and reused. This disk is made of synthetic resin that is coated with a reflective material, usually aluminum. When information is written by a CD-writer drive, some microscopic pits are created on the surface of the CD. The information bit on a CD-ROM surface is coded in the form of ups and downs (known as pits and bumps), created by infrared heat. There is one laser diode on the reading head. The bits are read by shining a low-intensity laser beam onto the spinning disc. The laser beam reflects strongly from a smooth area on the disc but weakly from a pitted area. A sensor receiving the reflection determines whether each bit is a 1 or a 0 accordingly.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_30_3.png)

CDs were initially a popular storage media for music; they were later used as general computer storage media. Most personal computers are equipped with a CD-Recordable (CD-R) drive. A CD-Rewritable (CD-RW) disc can be reused because the pits and flat surfaces of a normal CD are simulated on a CD-RW by coating the surface of the disc with a material that, when heated to one temperature becomes amorphous (and therefore non-reflective) and when heated to a different temperature becomes crystalline (and therefore reflective).

## 1.7 INTRODUCTION TO OPERATING SYSTEMS

A computer system has many resources such as the processor (CPU), main memory, I/O devices, and files. The operating system acts as the manager of these resources and allocates them to specific programs and uses them as and when necessary for the tasks.

An operating system may be defined as a system software which acts as an intermediary between the user and the hardware, an interface which isolates the user from the details of the hardware implementation. It consists of a set of specialized software modules that makes computing resources (hardware and software) available to users. Thus, the computer system is easier to use with the operating system in place than without it. Some of the operating systems used nowadays are Mac, MS Windows, Linux, Solaris, etc.

The common functions of an operating system includes:

- **Processor management** The process abstraction is a fundamental mechanism implemented by the operating system for management of the execution of programs. A process is basically a program in execution. The operating system decides which process gets to run, for how long and perhaps at what priority or level of importance.
- **Memory management** Operating system is responsible for keeping track of which parts of the memory are currently being used and by whom. It organizes and addresses memory; hands requests to allocate memory, frees up memory no longer being used, and rearranges memory to maximize the useful amount. Often several programs may be in memory at the same time. The operating system selects processes that are to be placed in memory, where they are to be placed, and how much memory is to be given to each.
- **Device management** The operating system allocates the various devices to the processes and initiates the I/O operation. It also controls and schedules accesses to the input/output devices among the processes.
- **File management** A file is just a sequence of bytes. Files are storage areas for programs, source codes, data, documents etc. The operating system keeps track of every file in the system, including data files, program files, compilers, and applications. The file system is an operating system module that allows users and programs to create, delete, modify, open, close, and apply other operations to various types of files. It also allows users to give names to files, to organize the files hierarchically into directories, to protect files, and to access those files using the various file operations.

Apart from these functions, an operating system must provide the facilities for controlling the access of programs, processes, memory segments, and other resources.

The **kernel** is that part of operating system that interacts with the hardware directly. The kernel represents only a small portion of the code of the entire OS but it is intensively used and so remains in primary storage while other portions may be transferred in and out of secondary storage as required. When a computer boots up, it goes through some initialization functions, such as checking the memory. It then loads the kernel and switches control to it. The kernel then starts up all the processes needed to communicate with the user and the rest of the environment.

The user interface is the portion of the operating system that users interact with directly. Operating systems such as MS-DOS and early versions of UNIX accepted only typed-in text commands. Now most operating systems provide users a graphical user interface for their interactions with the system. Operating systems such as Microsoft Windows, Solaris and Linux allow the user to interact with the operating system through icons, menus, keyboard and mouse movements. The user interface and way of interactions vary widely from one operating system to another.

### 1.7.1 Loading an Operating System

In some digital devices like controllers of small appliances, hand-held devices and videogame console, the operating system is relatively simple and small and is stored in ROM (Read-Only Memory). The operating system is also present in a ROM for systems such as industrial controllers and petrol-filling equipment. In such a system, it gains immediate control of the processor, the moment it is turned on.

In personal computer, the operating system is usually stored on hard disk. Because size of the operating system is large enough, it cannot be placed entirely in RAM. The kernel, the core part of the operating system, is loaded into RAM at start-up and is always present in memory. Other parts of the operating system are loaded into RAM as and when required. It is to be noted that there is no operating system resident in a new computer. The operating system is usually sold on a CD or DVD media and has to be permanently transferred from a CD or DVD media to the hard disk by expanding compressed files and initializing the whole system for use.
