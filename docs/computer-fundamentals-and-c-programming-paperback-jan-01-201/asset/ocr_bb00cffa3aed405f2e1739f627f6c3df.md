+   - *CPU Management*　The instructions provided in the program are executed by the CPU. The OS keeps track of the instruction that was last executed. This enables it to resume a program if it had to be taken out of the CPU before it completed execution.
+   - *Memory Management*　The OS allocates memory for the program and loads the program to the allocated memory. After the program has completed execution, the OS cleans up the memory (and registers) and makes them available for the next program.
+   - *Device Management*　If the program needs to access the hardware, it makes a call to the OS rather than attempt to do the job itself. For instance, if the program needs to print a file, the OS directs the device driver associated with the printer to operate the device.
+   - *File Management*　Programs read and write files and the OS has to ensure that disk blocks are allocated to the program as and when needed. It maintains a record of all blocks used by a file so it can readily provide the data to a program that reads the file. Also, the OS has to free up these blocks when a file is deleted.

Because the OS directly handles the hardware, it must present a consistent view of devices to all programs. Application programmers can thus write programs with the confidence that they will continue to run even after the hardware has been replaced or upgraded. The confidence doesn’t end here; a program must also run on other similar computers but with different hardware configurations. Operating systems alone can’t handle this flexibility; they need *device drivers* (2.6) to bail them out.

In addition to these basic services, an OS provides a wide range of other services for the user. It offers standalone programs for creating files and directories, handling processes, copying files across a network and performing backups. These programs don’t form the core of the operating system, but may be considered as additional services that benefit both users and programmers. The schematic view of an operating system is depicted in Figure 2.1.

# 2.5.1　How Users Interact with an Operating System

We know that programs make a call to the operating system whenever they need to access the hardware. But who asks the OS to run a program and how? We, the users do, using an interface called the *shell*. The primary job of the shell is to wait for user input and then invoke a program associated with the input. There are basically two forms of the shell—the Character User Interface (CUI) and the Graphical User Interface (GUI).

The *Character User Interface (CUI)* presents a screen with a *prompt string* beside a blinking cursor. To talk to the OS, you must key in the name of a program at this $ or C> prompt and then press *[Enter]*:

```
    $ a.out  [Enter]        UNIX/Linux systems
    C> AOUT  [Enter]         MSDOS/Windows systems
```

The string a.out or AOUT is interpreted by the shell as a command to execute. This command is often an executable program. The shell looks for a file of this name in specified directories of the hard disk. If it finds the file, it directs the OS to run the program.