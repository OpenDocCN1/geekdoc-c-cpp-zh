# 5.9.2 Role of Disk Drive for loading DOS

A disk drive is a device that either stores data or reads data from the disk, which may be a floppy or a hard disk. A PC has floppy drives, hard disk drives, and CD-ROM drives. The first floppy drive is conventionally called drive A whereas the second floppy drive is designated as drive B and the first hard disk drive is designated as drive C.

Booting is synonymous with starting a computer. When the computer is switched on, the BIOS program, fused in the ROM, checks the memory and peripherals. Drive A of a microcomputer is the primary drive, which a computer first looks for when switched on. It reads the disk in drive A and checks for any boot record or system files. If drive A does not have these, it goes to drive C, skipping drive B. On finding drive C, the computer starts the process of loading the DOS into the RAM of the computer. Once the DOS is loaded, it is said that the DOS has booted the computer and is ready to accept the user's orders. The following prompt appears and awaits orders from the user:

```
`A:>_ or C:>_`
```

The above prompt is displayed along with a flashing cursor, depending upon whether the system has been booted from drive A or C. When the booting is from drive A, there must be a dos diskette in drive A. When the booting is from C drive, DOS must have been previously installed in the hard disk so that the system files are duly loaded into RAM.

# 5.9.3 Starting DOS

When the computer starts working, it does not have an ordinary program loaded into it. The computer does, however, have two special built-in programs it can rely on, and it does know how to do the following:

+   - How to do self-testing to see that things are in working order
+   - How to start up DOS

This start-up program is usually called a bootstrap loader, since it pulls DOS up by the bootstraps. This bootstrap operation works in two stages.

First, the tiny program built into the computer goes to work. It just knows how to read the beginning of a diskette or the hard disk, in case the diskette is not used, and runs whatever it finds there as any other operating system. However, this program in the computer does not actually know anything about DOS. The simple start-up program is located in the beginning of a diskette or hard disk. The start-up program, which is the DOS's own starting routine, knows how to set up DOS in the computer.

Second, the start-up program checks the memory. Then, it loads the DOS system files into the memory. There are three main system files in DOS. These are as follows:

```
`IO.SYS`
```

```
`DOS.SYS`  
`COMMAND.COM`
```

First, the IO.SYS file is loaded into the memory and checks whether all the input and output devices are correctly connected to the computer. Then the program loads the DOS.SYS file, which starts the loading of COMMAND.COM into primary memory. COMMAND.COM is the command interpreter for DOS commands. It stays in the primary memory as long as the machine is on. The DOS.SYS also loads another system file known as HIMEM.SYS, which is a program that manages the memory. Then, it sets the configuration of the system by checking the file CONFIG.SYS. In the end, it checks for the existence of AUTOEXEC.BAT file. If it exists, then it executes the particular file. Eventually, the system prompt appears and the system is ready for use.

To run MS-DOS, 640 KB of primary memory is required. This memory is called the conventional base memory. The primary memory of the personal computer is subdivided into three parts.

+   - Conventional memory
+   - Extended memory
+   - Expanded memory

Extended memory requires HIMEM.SYS to manage it.

# 5.9.4 The Command Prompt

When the personal computer is turned on, some cryptic information flashes by. MSDOS displays this information to let the user know how it is configuring the computer. This can be ignored now. When the display stops scrolling past the information, the following is seen on the screen:

```
`C:\>`
```

This is called the command prompt or DOS prompt. The flashing underscore next to the command prompt is called the cursor. The cursor shows the position where the command typed in would appear.

Any line in DOS that begins like this is a command prompt. The actual character that symbolizes the prompt is the ‘greater than’ symbol: ‘>’. This line prompt is a way of informing the users where they are in DOS. The characters that appear with ‘>’ in the line prompt indicate the following:

+   - The C: means that the user is working within the file space (disk storage) on the hard drive, which is designated as C. C is usually reserved for the internal hard disk of a PC.
+   - The backslash (\) represents a level in the hierarchy of the file structure. There is always at least one, which represents the root directory. The root directory represents the very first level of the file structure on the hard disk.

Nowadays, while MSDOS is not commonly used, it can still be accessed from every version of Microsoft Windows by clicking Start/Run and typing command or by typing CMD in Windows NT, Windows 2000, or Windows XP.