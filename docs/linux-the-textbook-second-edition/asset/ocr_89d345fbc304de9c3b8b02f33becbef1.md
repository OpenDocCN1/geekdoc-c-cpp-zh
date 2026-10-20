```
$ ls -ld courses memos personal
drwxr-xr-x 2 sarwar faculty 4096 Jul  6 10:31 courses
drwxr-xr-x 2 sarwar faculty 4096 Jul  8 15:19 memos
drwxr-xr-x 2 sarwar faculty 4096 Jul  8 15:19 personal
$ cd ~/courses/ee446/exams
$ ls -l
total 44
-rw-r--r-- 1 sarwar faculty  7878 Jul  8 15:23 mid1
-rw-r--r-- 1 sarwar faculty 32253 Jul  8 15:23 mid2
drwxr-xr-x 2 sarwar faculty  4096 Jul  8 15:22 solutions
$
```

The information displayed by the ls -l command is summarized in Table 4.1.

In the preceding two uses of the ls -l command, courses, memos, personal, and solutions are directories, and mid1 and mid2 are ordinary files. As stated earlier, we discuss access permissions and user types in Chapter 5. The owner of the files is sarwar, who belongs to the group faculty. The values of the remaining fields are self-explanatory.

You can use the ls command with the -i option to display the inode numbers of files and directories. To display the inode number of a directory, you need to use the ls -id command. The following examples of its use show that the inode number for the greeting file is 6278611, and for the directories courses, memos, and personal, they are 6555603, 6555456, and 6555324, respectively.

```
$ ls -i greeting
16517942 greeting
$ ls -id courses memos personal
16517083 courses  16517069 memos  16517079 personal
$
```

The ls -al command displays a long list of all the files in a directory as follows:

```
$ ls -al ~/courses/ee446/exams
total 52
drwxr-xr-x 3 sarwar faculty  4096 Jul  8 15:22 .
drwxr-xr-x 4 sarwar faculty  4096 Jul  8 15:22 ..
-rw-r--r-- 1 sarwar faculty  7878 Jul  8 15:23 mid1
-rw-r--r-- 1 sarwar faculty 32253 Jul  8 15:23 mid2
drwxr-xr-x 2 sarwar faculty  4096 Jul  8 15:22 solutions
$
```

You can use the -F option to identify directories, executable files, and symbolic links. The ls -F command displays an asterisk (*) after an executable file, a slash (/) after a directory, and an "at" symbol (@) after a symbolic link (discussed in Chapter 8), as follows:

```
$ ls -F /
bin/    dev/    initrd.img@  lost+found/  opt/    run/    sys/    var/
boot/   etc/    lib/     media/       proc/   sbin/   tmp/    vmlinuz@
cdrom/  home/   lib64/   mnt/         root/   srv/    usr/
$
```

Note that there is no executable file in the root directory. The output of the ls -F /bin command would show that all the files in the /bin directory are executable. You are encouraged to read the online manual pages for the ls command on your system or see the Command Appendix at the CRC Press website for this book for a detailed description of the command.

By using the shell metacharacters and regular expressions, you can specify a particular set of files and directories in the file system structure or a particular set of strings in files or directories. For example, the following command can be used in the C shell to display a long list for all the files in the ~/courses/ee446 directory that have the .c extension and start with the string lab followed by zero or more characters, with the condition that the first of these characters cannot be 5.