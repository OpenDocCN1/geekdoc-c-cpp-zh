
![](img/d75612dcf3ab36327142238ab5bb21d8_71_0.png)

**FIGURE 2.2** Role of the Device Driver

but the systems programmer knows how to *implement* the call in the driver software. Programming a device thus needs detailed knowledge of the device internals, the reason why device drivers are normally written by the device manufacturer.

Instead of having a separate program for driving a device, doesn’t it make sense to include the code for it in the OS or the application? No, because if the device changes, the OS and all applications using it would need to be changed as well. The outcome would then be a programmer’s nightmare. Applications must be independent of the type of hardware they access. Keeping the device driver separate from the OS and programs allows a driver to be shared between multiple programs.

That said, it is true that operating systems include built-in drivers for some commonly used devices. You don’t need a separate driver for attaching flash memory. But even if the OS contains a driver for a device, you should install the (possibly) updated version that is shipped with the product. The newer version would contain improved features and fixes for bugs encountered in previous versions. If you can’t locate the media containing the driver, get the driver software from the Web site of the device manufacturer.

**Takeaway:** Even though the operating system shields the programmer from knowledge of the hardware, it’s the device driver that completely knows the hardware. The OS manages the call it makes to the driver and the response it receives from it.

**Caution:** A driver is meant for a specific model of the device and a specific version of the operating system. Installing a wrong driver may damage the hardware or make it behave improperly. It is also possible that the device may not work at all.

## 2.7 MSDOS: A CUI OPERATING SYSTEM

We begin our examination of the commonly used operating systems with MSDOS, the Microsoft Disk Operating System. MSDOS was used in the earliest personal computers and is now a part of Windows. The OS shipped with IBM's own PC was identical to MSDOS but was called PCDOS. In its initial years, MSDOS was loaded from a floppy diskette on a PC having two diskette drives but no hard disk. MSDOS is a single-user and single-tasking OS that needs only 640 KB of RAM. We must know this "outdated" OS because it gives us a first-hand feel of working with an OS.

The startup sequence loads the boot loader (2.4) located in the first sector of the hard disk, which then pulls up the basic OS by loading the files IO.SYS, MSDOS.SYS and COMMAND.COM into memory. The system eventually displays the prompt:

```
C:\>
Ready to accept commands
```

You are now in the MSDOS shell from where you can key in any of its commands or a program that you have written. You will see this shell prompt in all versions of Microsoft Windows, which offer a trimmed version of MSDOS (as `cmd.exe`).

> **Note:** Most features of MSDOS are derived from UNIX.

### 2.7.1 Files and the File System

Every operating system needs a *file system* to hold all files and directories in a rigid structure. (*A directory* is a folder that contains multiple files.) Like UNIX, MSDOS supports a hierarchical file system as an inverted tree structure (Fig. 2.3). The top of this structure is called *root* (represented by `\`), which serves as the reference point for all files.

A file is uniquely identified by a *pathname* which specifies its location in the file system. For instance, the pathname **`C:\PROGS\INTRO.C`** locates the file **`INTRO.C`** in the directory **`PROGS`**, which in turn is under `\` (root) of the C: drive or partition of the hard disk. The prompt **`C:\>`** shows this root directory.

Earlier versions of MSDOS supported an 8.3 file-naming convention which allowed a maximum length of 8 characters for the basic filename and 3 characters for the extension. Thus, **`INTRO.C`** and **`AUTOEXEC.BAT`** are valid filenames, but not **`INTRODUCTION.C`** or **`INDEX.HTML`**. However, these filenames are valid in later versions of MSDOS (Windows 95 onwards) that support 255-character filenames. MSDOS filenames are not case-sensitive, so you can't have two files named **foo** and **FOO** in the same directory.

MSDOS is always installed in the file system named **C:**. The names **A:** and **B:** are reserved for the two floppy drives that once resided on the PC. File systems created subsequently have the labels **E:, F:, G:** etc. (If the computer has an optical drive, it would be accessed as **D:**.) Thus, the pathname **`C:\PROGS\INTRO.C`** won't conflict with **`E:\PROGS\INTRO.C`**.

> **Note:** We used uppercase for MSDOS commands and filenames simply because that was the way this OS was initially used. Versions of MSDOS built into the later versions of Windows use lowercase though.

![](img/d75612dcf3ab36327142238ab5bb21d8_73_0.png)

| | |
|---|---|
| Pathname for directory iTunes: | `C:\Program Files\iTunes` |
| Pathname for file Woodstock69.avi: | `C:\Videos\Concerts\Pop\Woodstock69.avi` |

**FIGURE 2.3** The MSDOS Hierarchical File System

### 2.7.2 Internal and External Commands

MSDOS supports a set of *internal commands* for basic operations and a larger set of *external commands* for advanced tasks (Table 2.1). Internal commands are built into the shell (the file `COMMAND.COM` or `cmd.exe` in later versions of Windows). For instance, the `DIR` command, which lists files, is an internal command of MSDOS. There's no file named `DIR.COM` or `DIR.EXE` in the file system. The commands that copy and remove files (`COPY` and `DEL`) are also internal.

The external commands are available as executable files having the `.EXE`, `.COM` or `.BAT` extension. Commands that format a disk partition (`FORMAT.COM`), back up files (`BACKUP.EXE`), or check the integrity of the disk (`CHKDSK.EXE`) are implemented as external commands. However, the location of the external commands must be known to the OS, so the `PATH` variable must be set accordingly.

The default behavior of a command can be changed by using it with *options* or *switches*. For instance, `DIR` can be used with the `/P` switch (as in `DIR /P`) for the output to pause at every page.

> **Takeaway:** Internal commands are built into the shell. External commands exist as separate files which the shell locates using the information provided in the `PATH` variable.

> **Tip:** Use the `/?` switch with any MSDOS command to learn about its usage. For instance, `MKDIR /?` displays the help screen for the `MKDIR` command.

| Command | Significance |
|---|---|
| ATTRIB | Displays or changes the attributes of one or more files. |
| FIND | Displays lines containing a specified string. |
| FORMAT | Reformats a device to create an empty file system. |
| MORE | Displays output one page at a time. |
| SORT | Orders a file in ASCII sequence but is case-insensitive. |
| TREE | Graphically displays directory structure with all subdirectories. |
| XCOPY | Copies an entire directory structure. |

### 2.7.3 Working with Files and Directories

Like UNIX, MSDOS supports a powerful illusion that a user is placed at a specific point in the file system. You can know where you are, create and remove directories and navigate the file system without losing track of your location. Some of these commands take arguments, which are additional words that follow a command. The following internal commands are used to handle directories:

- `MKDIR progs` — Makes a directory progs. (Also `MD progs`)
- `RMDIR progs` — Removes directory progs. (Also `RD progs`)
- `CHDIR` — Displays current directory. (Also `CD`)
- `CHDIR progs` — Changes current directory to progs. (Also `CD progs`)
- `DIR` — Lists contents of current directory.

Note from the description that MSDOS also offers synonyms for three commands: MD, RD and CD. MKDIR and RMDIR compulsorily need arguments but CHDIR and DIR can work both with and without arguments. Also keep in mind that RMDIR progs won’t work unless the directory progs is empty and you are placed above it.

The preceding commands obviously won’t work on ordinary files, which are handled by a separate set of internal commands:

- `TYPE foo` — Displays the contents of foo.
- `COPY foo bar` — Copies file foo to bar.
- `DEL foo` — Deletes file foo. (Also `ERASE foo`)
- `RENAME foo bar` — Renames foo to bar. (Also `REN foo bar`)
- `MOVE foo bar` — Renames foo to bar.

There are two synonyms here as well (ERASE and REN). You need to be comfortable working with the last four commands because they can be used on multiple files.

The COPY command is special; apart from copying a file, it can be used to create a file and concatenate (combine) multiple files:

- `COPY CON foo` — Creates a file foo. (Press `[Ctrl-z]` at end.)
- `COPY foo1 + foo2 + foo3 foo4` — Concatenates three files to foo4.
