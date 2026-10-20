The following command searches the present working directory for files that have the name core or have extensions .jpg or .o, displays their absolute pathnames, and removes them from the file structure. Parentheses are used to enclose a complex criterion. Be sure that you use spaces before and after \(, \), and -o. The command does not prompt you for permission to remove ; in order to be prompted, replace -exec with -ok, or use the rm -i command.

```
$ find . \( -name core -o -name '*.jpg' -o -name '*.o' \) -print -exec rm {} \;
...
$
```

You can use the whereis command to find out whether your system has a particular command, and if it does, where it is in the file structure. You typically need to get such information when you are trying to execute a command that you know is valid but that your shell cannot locate because the directory containing the executable for the command is not in your search path (see Chapters 2 and 4). Under these circumstances, you can use the whereis command to find the location of the command and update your search path. Although whereis is a Berkeley Software Distribution (BSD) command, most Linux systems today have it because they have a BSD compatibility package. Depending on the system you are using, the command not only gives you the absolute pathname for the command that you are searching for but also gives you the absolute pathnames for its manual page and source files if they are available on your system. The following is a brief description of the command.

Syntax:
    whereis [options] [file-list]
Purpose: Locate binaries (executable files), source codes, and manual pages for the commands in file-list—a space-separated list of command names
Output: Absolute pathnames for the files containing binaries, source codes, and manual pages for the commands in file-list
Commonly used options/features:
    -b Search for binaries (executable files) only
    -s Search for source code only

The following examples illustrate the use of whereis command. The first command is used to locate the ftp command. The second command is used to locate the executable file for the cat command. The last command locates the information for the find and tar commands.

```
$ whereis ftp
ftp: /usr/bin/ftp /usr/share/man/man1/ftp.1.gz
$ whereis -b cat
cat: /bin/cat
$ whereis find tar
find: /usr/bin/find /usr/share/man/man1/find.1.gz /usr/share/info/find.info.gz
tar: /usr/lib/tar /bin/tar /usr/include/tar.h /usr/share/man/man1/tar.1.gz
$
```

In the outputs of these commands, the /bin directory contains the executable files (also called binaries) essential user commands, the directory /usr/bin contains the executable files for utilities, applications, and commands, the directory /usr/share/man contains several subdirectories that contain various sections of the Linux online manual, /usr/lib libraries for programming languages and packages, and the /usr/include directory contains header files.

In a system that has multiple versions of a command, the which utility can be used to determine the location (absolute pathname) of the version that is executed by the shell you are using when you type the command. The following sessions show sample runs of this command.