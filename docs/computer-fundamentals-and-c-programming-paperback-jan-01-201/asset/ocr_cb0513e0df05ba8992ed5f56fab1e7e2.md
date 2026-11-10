operating system. Unlike MSDOS and Windows, UNIX is a *true* multi-user and multi-tasking system that runs on hardware ranging from PCs to supercomputers. UNIX/Linux systems form the backbone of the Internet.

The core of the OS is known as the *kernel*, which directly communicates with the hardware. Users interact with a shell (similar to the MSDOS shell) which acts as an interface between the user and kernel. When you enter a command through the keyboard, the shell examines the command line before forwarding it to the kernel for execution. If a program needs to access the hardware, it makes calls to the kernel. These calls (known as *system calls*) are special C functions that have been left out of ANSI C.

The UNIX utilities that handle files and processes are the finest in the business. Linux is a programmer’s paradise; it supports compilers for *all* programming languages. UNIX was originally a CUI system where all programs or commands were executed at the shell prompt. The GUI, which was added to the system later, supports a CUI-based terminal window representing the shell. However, most of the command-line programs don’t have GUI equivalents.

![](bbox=[0.084, 0.414, 0.133, 0.453])

> **Tip:** Linux users can switch to the CUI mode using *[Ctrl][Alt][F1]* and to the GUI mode using *[Ctrl][Alt][F7]*.

# 2.9.1 The UNIX File System

Files and directories are related to one another by being part of a file system. Even though MSDOS and Windows have emulated the UNIX file system, the following differences must be noted:

+   - The separator of a UNIX pathname is a / instead of \. The MSDOS pathname `a\b\c` becomes `a/b/c` in UNIX. This convention is also followed on the World Wide Web.
+   - There are no drive prefix likes C: and D: in the pathname.
+   - In UNIX, all files in *all* devices attached to a computer are part of a *single* file system with a single root (/ instead of \). So, the pathnames `/home/sumit/progs` and `/home2/kanetkar/progs` can be on two different disks.
+   - Unlike in MSDOS/Windows, UNIX filenames are case-sensitive, so `foo` and `F00` are two different filenames that can coexist in the same directory.

The third point has far-reaching implications. Unlike with MSDOS/Windows, the UNIX file system integrates multiple disks and file systems into a single file system. These systems may reside on multiple connected machines—perhaps on two different continents! The user still sees a single file system.

# 2.9.2 Basic Directory and File Handling Commands

As you know well by now, files are containers for storing static information. But UNIX also considers directories and devices as files, and the same command sometimes works with multiple file types. By convention, UNIX commands are in lowercase and the following ones are used for handling directories: