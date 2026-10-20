With no argument, the echo command displays a blank line on the screen. You can determine the absolute pathname of your home directory by using the echo command, as follows:

```
$ echo $HOME
/home/sarwar
$
```

where HOME is a shell variable (a placeholder) in the Bourne shell. The shell uses this variable to keep track of the absolute pathname of your home directory. In the C shell, the variable is home. We discuss shell variables and the echo command in detail in Chapters 12, 13, W29, and W30.

Another way to display the absolute pathname of your home directory is to use the pwd command. You use this command to determine the absolute pathname of the directory you are currently in, that is, your present working directory, also known as the current directory. This command does not require any arguments. When you log on, the Linux system puts you in your home directory. You can use the pwd command right after logging on to display the absolute pathname of your home directory as follows:

```
$ pwd
/home/sarwar
$
```

# 4.5.2 Browsing the File System

You can browse the file system by going from your home directory to other directories in the file system structure and displaying a directory's contents (files and subdirectories in the directory), provided that you have the permissions to do so. We cover file security and access permissions in detail in Chapter 5. For now, we show how you can browse your own files and directories by using the cd (change directory) and ls (list directory) commands. The following is a brief description of the cd command.

**Syntax:**
cd [directory]

**Purpose:** Change the present working directory to directory, or to the home directory if no argument is specified

The shell variable PWD is set after each execution of the cd command. The pwd command uses the value of this variable to display the present working directory. After getting into a directory, you can view its contents (the names of files or subdirectories in it) by using the ls command. The following is a brief description of this command. The cd and ls commands are two of the most heavily used Linux commands.

**Syntax:**
ls [option] [pathname-list]

**Purpose:** Send the names of the files in the directories and files specified in pathname-list to the display screen

**Output:** Names of the files and directories in the directory specified by pathname-list, or the names only if pathname-list contains file names only

**Commonly used options/features:**
-F Display/after directories, * after binary executables, and @ after symbolic links
-a Display names of all files, including hidden files .., and so on.
-h Display output in human readable sizes (e.g., 1.1 K, 31 M, 2.6 G) when used with -l and/or -s option
-i Display inode number and file name
-l Display long list that includes access permissions, hard link count, owner, group, file size (in bytes), and modification time