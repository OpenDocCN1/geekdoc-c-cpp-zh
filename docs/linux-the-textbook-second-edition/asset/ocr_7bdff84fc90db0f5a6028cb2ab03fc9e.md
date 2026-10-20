Another difference between pipes and FIFOs is that whereas a pipe is a main memory buffer maintained by the Linux kernel and has no name, a FIFO is created on disk and has a name like a filename. This means that, like files, FIFOs have to be created and opened before they can be used for communication between processes. Thus, accessing a FIFO requires an access to the secondary storage device where it resides. Pipes are process persistent, which means that they exist as long as the process that creates them exists. FIFOs on most Linux systems are filesystem persistent, meaning that they exist on the system until they are explicitly removed/deleted or the relevant file system is unmounted (i.e., removed from the system).

You can use the mknod() system call or the mkfifo() library call to create a FIFO in a program and the mkfifo command to create a file in a shell session. We discuss the command line use of FIFOs in this section. We discuss the use of FIFOs, pipes, and the related system calls and library calls in the chapters on system programming (Chapters 15 and 16, and W20 and W21 at the book website). Here is a brief description of the mkfifo command.

```
Syntax:
  mkfifo [option] file-list
Purpose: Create FIFOs with pathnames given in file-list
Output: FIFOs for the pathnames given in file-list are created in the relevant directories
Commonly used options/features:
  -m mode    Set access permissions for newly created FIFOs to "mode"; the access permissions are specified in "mode" as they are with the chmod command, such as 666, meaning read and write permissions for everyone and execute permission for nobody
```

In the following session, we use the first command to create a FIFO, called myfifo1, with default permissions based on the current value of umask (see discussion in Chapter 5). We use the second command to create a FIFO, called myfifo2, with read and write permissions for the owner and no permissions for all other users. We use the ls -al myfifo1 myfifo2 command to display the access permissions of the two FIFOs. Note that the first character in the long listing of the two FIFOs is "p," indicating that myfifo1 and myfifo2 are of the FIFO (named pipe) type.

```
$ mkfifo myfifo1
$ mkfifo -m 600 myfifo2
$ ls -l myfifo3 myfifo4
prw-r--r-- 1 sarwar faculty 0 Aug  9 08:30 myfifo3
prw------ 1 sarwar faculty 0 Aug  9 08:31 myfifo4
$
```

The general method by which two commands, cmd1 and cmd2, can communicate with a FIFO, called myfifo1, is shown in the following command sequence.

```
cmd1 < myfifo1 &
cmd2 infile | tee myfifo1 | cmd3
```

Note that we run the first command in the background (see Chapter 10 for background processes) so that we could run cmd2. When we execute cmd1, it blocks, because myfifo1 is empty. Note that cmd1 blocks and returns immediately if myfifo1 is a file. When the output of cmd2 is sent to myfifo1 and cmd3 via the tee utility, cmd1 unblocks and starts processing data in myfifo1. Outputs of commands cmd1 and cmd3 are sent to standard output (i.e., the display screen). Figure 9.18 shows these semantics with the help of a diagram.