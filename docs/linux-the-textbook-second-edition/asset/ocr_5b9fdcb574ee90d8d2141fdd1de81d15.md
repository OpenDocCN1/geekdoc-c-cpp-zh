You can use the findmnt command to display information about all mounted file systems, including their type such as ext4. This command with -t option may be used to display the file systems of a particular type. For example, you can use the findmnt -t ext4 command to display the list of all ext4 file systems mounted on your system.

Table 4.4 shows a summary comparison of Linux file systems XFS, Ext4, and ZFS. Browse through the relevant websites listed in “Web Resources” (Table 4.5 at the book GitHub site) to find out more about Ext4, XFS, and ZFS.

# Exercise 4.8

Use the findmnt command to display information about all the file systems mounted on your system. How many file systems are mounted on your system?

# Exercise 4.9

Use the findmnt command to display information about all ext4 file systems mounted on your system. How many of these file systems are mounted on your system?

# 4.7.1 Displaying Disk Usage of Files and Directories

You can display the disk usage by files and directories by using the du command. It is a useful command for new Linux users with runaway log files, hitting their quotas. Here is a brief description of this command.

```
Syntax:
  du [option]... file-list...
Purpose: Display a summary of the disk usage of files in file-list, recursively for directories
Commonly used options/features:
  -a    Display disk usage for all files, not only directories
  -h    Display in humanly readable format, e.g., 1.7 K, 31.9 M, and 3 G
  -s    Display only total disk usage each file in file-list
```

In the following session, we use the du command without any option, and with -s and -h options, to show disk usage for various files and directories in 1 K block sizes and in K, M, and G bytes.

```
$ du ~
4               /home/sarwar/.linuxmint/mintMenu/applications
34724           /home/sarwar/.linuxmint/mintMenu
...
27450108        /home/sarwar
$ du -h ~
4.0K    /home/sarwar/.linuxmint/mintMenu/applications
34M     /home/sarwar/.linuxmint/mintMenu
```

# TABLE 4.4

A Summary Comparison of Linux File Systems

| Feature | Ext4 | ZFS | XFS |
|---|---|---|---|
| Introduced to Linux or Open Source | 2006 | 2005 | 2001 |
| Maximum file size | 16 tebibytes (TiBᵃ) | 16 exbibytes (EiBᵇ) | 8 EiB |
| Maximum volume size | 1 EiB | 2¹²⁸ bytes = 256 trillion yobibytes (YiBᶜ) | 8 EiB |
| Maximum number of files | 4 billion | Unlimited (2⁴⁸ per directory) | 16 EiB |
| Maximum filename length | 255 bytes | 255 bytes | 255 bytes |

a. TiB = 2⁴⁰ = 1024⁴.
b. EiB = 2⁶⁰ = 1024⁶.
c. YiB = 2⁸⁰ = 1024⁸.