```
-rw-r--r--  2 bob  bob  797 Jan 16 10:00 myfile
-rw-r--r--  2 bob  bob  797 Jan 16 10:00 myfile2
$
```

As you see in this screen display (which shows the listing of files in our home directory and will not be the same as the listing of files in your home directory), the information about each file in the current working directory is displayed in eight columns. The first column shows the type of file, where d stands for directory, l stands for symbolic link, and – stands for ordinary or regular file. Also in the first column, the access modes to that file for user, group, and others is shown as r, w, or x. In the second column, the number of links to that file is displayed. In the third column, the username of the owner of that file is displayed. In the fourth column, the name of the group for that file is displayed. In the fifth column, the number of bytes that the file occupies on disk is displayed. In the sixth column, the date that the file was last modified is displayed. In the seventh column, the time that the file was last modified is displayed. In the eighth and final columns, the name of the file is displayed. This way of executing the command is a good way to list more complete information about the file. Examples of using the more complete information are (1) so that you can know the byte size and be able to fit the file on some portable storage medium or (2) to display the access modes so that you can alter the access modes to a particular file or directory.

# In-Chapter Exercise

+   17. Use the ls -la command to list all of the filenames in your home directory on your Linux system. How does the listing you obtain compare with the listing shown earlier? Remember that our listing was done on a Linux Mint 18.2 system.

You can also get a file listing for a single file in the current working directory, by using another variation of the ls command, as follows:

```
$ ls -la myfile
-rw-r--r--  1 bob  bob  797 Jan 16 10:00 myfile
$
```

This variation shows you a long listing with attendant information for the specific file named myfile. A breakdown of what you typed on the command line is (1) ls, the command name; (2) -la, the options; and (3) myfile, the command argument.

What if you make a mistake in your typing and misspell a command name or one of the other parts of a command? Type the following on the command line:

```
$ lx -la myfile
lx: not found
$
```

The lx: not found reply from Linux is an error message. There is no lx command in the Linux operating system, so an error message is displayed. If you had typed an option that did not exist, you would also get an error message. If you supplied a file name that was not in the current working directory, you would get an error message too. This makes an important point about the execution of Linux commands. If no error message is displayed, then the command executed correctly and the results might or might not appear on screen, depending on what the command actually does. If you get an error message displayed, you must correct the error before Linux will execute the command as you type it.

Typographic mistakes account for a large percentage of the errors that beginners make.

# 2.4.4 Creating, Deleting, and Managing Directories

Another critical aspect of file maintenance is the set of procedures and the related Linux commands you use to create, delete, and organize directories in your Linux account on a computer. When moving