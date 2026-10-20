| -user name | Search for files owned by the user name or ID name |
| \( expr \ ) | True if expr is true; used for grouping criteria combined with OR or AND |
| ! expr | True if expr is false |

You can use [-a] or a space to logically AND, and -o to logically OR two criteria. Note that at least one space is needed before and after an open bracket (\() or a close bracket (\), and before and after -o. A complex expression can be enclosed in parentheses, \( and \). We now discuss some illustrative examples.

The find (or find .) command lists pathname for all the files and directories under the current directory. The most common use of the find command is to search one or more directories for a file, as shown in the first example. Here, the command searches for the USA.gif and Pakistan.gif files in your home directory and displays the pathname of the directory that contains them. If the file(s) being searched for occurs in multiple directories, the pathnames of all the directories are displayed.

```
$ find ~ -name USA.gif -o -name Pakistan.gif
/home/sarwar/myweb/USA.html
/home/sarwar/myweb/Pakistan.html
$
```

The following command displays the absolute pathnames of all the files in your home directory that end in .c and .C.

```
$ find ~ -name '*.c' -o -name '*.C'
...
$
```

The next command searches the /usr/include directory recursively for a file named socket.h and prints the absolute pathname of the file.

```
$ find /usr/include -name socket.h
/usr/include/asm-generic/socket.h
/usr/include/x86_64-linux-gnu/sys/socket.h
/usr/include/x86_64-linux-gnu/asm/socket.h
/usr/include/x86_64-linux-gnu/bits/socket.h
/usr/include/linux/socket.h
$
```

You might want to know the pathnames for all the hard links (discussed in Chapter 8) to a file—that is, files that have the same inode number. The following command recursively searches the root directory for all the files that have inode number 36700164 and prints the absolute pathnames of all such files.

```
$ find /usr . -inum 36700164
/usr/include
$
```

You can use the -perm option to display files under a directory hierarchy with given permissions. For example, you can use the find . -perm 755 command to display a list of files in your current directory with octal permissions 755 (i.e., read, write, and execute for the file owner, and read and execute for other users on your system). You can use the ls -l command to verify the output of the find command.

```
$ find . -perm 755
.
./sandbox_dir
./my_cat
$ ls -l
total 1916
...
```