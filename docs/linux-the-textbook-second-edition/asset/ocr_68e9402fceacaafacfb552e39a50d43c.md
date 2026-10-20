```
variable
set: nothing appropriate.
$
```

The following in-chapter exercises ask you to use the man and whatis commands to find information about the passwd command. After completing the exercises, you can use what you have learned to change your login password on the Linux system that you use.

# In-Chapter Exercises

+   19. Use the man command with the -k option to display abbreviated help on the passwd command. Doing so will give you a screen display similar to that obtained with the whatis command, but it will show all apropos command names that contain the characters passwd.
+   20. Use the whatis command to get a brief description of the passwd command shown in Exercise 19, and then note the difference between the commands whatis passwd and man -k passwd.

# 2.5 Utility Commands

There are several major commands that allow the beginner to be more productive when using the Linux system. A sampling of these kinds of utility commands is given in the following sections, and is organized as system setups, general utilities, and communication commands.

# 2.5.1 Examining System Setups

The whereis command allows you to search along certain prescribed paths to locate utility programs and commands, such as shell programs. The general syntax of the whereis command is as follows:

```
Syntax:
  whereis [options] filename
Purpose: Locate the binary, source, and man page files for a command
Output: The supplied names are first stripped of leading pathname components and extensions, then pathnames are displayed on screen
Commonly used options/features:
  -b Searches only for binaries
  -s Searches only for source code
```

For example, if you type the command whereis bash on the command line, you will see a list of the paths to the Bash shell program files themselves, as follows:

```
$ whereis bash
bash: /bin/bash /etc/bash.bashrc /usr/share/man/man1/bash.1.gz
```

Note that the paths to a “built-in,” or internal, command cannot be found with the whereis command. We provide more information about internal and external shell commands in Chapter 10.

When you first log on, it is useful to be able to view a display of information about your userid, the computer or system you have logged on to, and the operating system on that computer. These tasks can be accomplished with the whoami command, which displays your userid on the screen. The general syntax of the whoami command is as follows:

```
Syntax:
  whoami
Purpose: Display the effective user id
Output: Displays your effective user id as a name on standard output
```