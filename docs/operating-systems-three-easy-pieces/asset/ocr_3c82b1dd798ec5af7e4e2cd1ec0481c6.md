# I/O DEVICES

# Application

| | POSIX API [open, read, write, close, etc.] |
| File System | Raw |
| Generic Block Interface [block read/write] |
| Generic Block Layer |
| Specific Block Interface [protocol-specific read/write] |
| Device Driver [SCSI, ATA, etc.] |

Figure 36.4: The File System Stack

The diagram also shows a raw interface to devices, which enables applications (such as a file-system checker, described later [AD14], or a disk defragment tool) to directly read and write blocks without using the abstraction. Most systems provide this type of interface to support these low-level storage management applications.

Note that the encapsulation seen above can have its downside as well. For example, if there is a device that has many special capabilities, those capabilities will go unused. This situation arises, for example, in Linux with SCSI devices, which have very rich error reporting; because other block devices (e.g., ATA/IDE) have much simpler error handling, and that higher levels of software ever receive a generic (generic IO error) error code; any extra detail that SCSI may have provided is lost to the file system [G08].

Interestingly, because device drivers are needed for any device you might plug into your system, over time they come to represent a huge percentage of kernel code. Studies of the Linux kernel reveal that over 70% of OS code is found in device drivers [CO01]; for Windows-based systems, it is quite high as well. When people tell you the OS has millions of lines of code, what they really saying is that the OS has millions of lines of device driver code. Of course, for any given installation, that code may not be active (i.e., only a few devices are connected to the system at a time). Perhaps more depressingly, as drivers are often written by "amateurs" (instead of full-time kernel developers), they tend to have many bugs and are a primary contributor to kernel crashes [S03].

# 36.8 Case Study: A Simple IDE Disk Driver

To dig a little deeper here, let's take a quick look at an actual device: an IDE disk drive [L94]. We summarize the protocol as described in this reference [W10]; we'll also peek at the source code for a simple example of a working IDE driver [CK+08].