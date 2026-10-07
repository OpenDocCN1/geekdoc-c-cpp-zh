
# INTERLUDE: FILES AND DIRECTORIES

As you can see, the pathname /home/users/ now refers to the root of the newly-mounted directory. Similarly, we could access directories a and b with the pathnames /home/users/a and /home/users/b. Finally, the files named foo could be accessed via /home/users/a/foo and /home/users/b/foo. And thus the beauty of mount: instead of having a number of separate file systems, mount unifies all file systems into one tree, naming your system uniform and convenient.

To see what is on your system, and at which points, simply run the mount program. You'll see like this:

```
/dev/sda on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
/dev/sda5 on /tmp type ext3 (rw)
/dev/sda7 on /var/vice/cache type ext3 (rw)
tmpfs on /dev/shm tmpfs (rw)
AFS on /afs type afs (rw)
```

This crazy mix shows that a whole number of different file systems, including ext3 (a standard disk-based file system), the proc file system (a file system for accessing information about current processes), tmpfs (a file system just for temporary files), and AFS (a distributed file system) are all glued together onto this one machine's file-system tree.

# 39.18 Summary

The file system interface in UNIX systems (and indeed, in any system) is quite rudimentary, but there is a lot to understand if you wish to master it. Nothing is better, of course, than simply using it (a lot). So please do so! Of course, read more; as always, Stevens [SR05] is the place to begin.

# INTERLUDE: FILES AND DIRECTORIES

# ASIDE: KEY FILE SYSTEM TERMS

- **A file** is an array of bytes which can be created, read, written, and deleted. It has a low-level name (i.e., a number) that refers to it uniquely. The low-level name is often called *i-number*.

- **A directory** is a collection of tuples, each of which contains a human-readable name and low-level name to which it maps. Each directory entry refers to another directory or a file. Each directory also has a low-level name (i-number) itself. A directory always has two special entries: the `.` , which refers to itself, and the `..`, which refers to its parent.

- **A directory tree or directory hierarchy organizes all files and directories into a large tree, starting at the `root`.**

- To access a file, a process must use a system call (usually, `open()`) to request permission from the operating system. If granted, the OS returns a `file descriptor`, which can be used for read or write access, as permissions and intent allow.

- Each file descriptor is a private, per-process entry, which refers to an entry in the `open file table`. The entry tracks which file this access refers to, the `current offset` of the file (i.e., which part of the file the next read or write will access), and other relevant information.

- Calls to `read()` and `write()` naturally update the current offset; otherwise, processes can use `lseek()` to change its value, enabling random access to different parts of the file.

- To force updates to persistent media, a process must use `fsync()` or related calls. However, doing correctly while maintaining high performance is challenging [P+14], so think carefully when doing so.

- To have multiple human-readable names in the file system refer to the same underlying file, use `hard links` or `symbolic links`. Each is useful in different circumstances, so consider their strengths and weaknesses before usage. And remember, deleting a file is just performing that last `unlink()` of it from the directory hierarchy.

- Most file systems have mechanisms to enable and disable sharing. A rudimentary form of such controls are provided by `permissions bits`; more sophisticated `access control lists` allow for more precise control over exactly who can access and manipulate information.

# INTERLUDE: FILES AND DIRECTORIES

# References

[BD96] "Checking for Race Conditions in File Access" by Matt Bishop, Michael Dilger. Computing Systems 9-2, 1996. A great description of the TOCTOU problem and its presence in file systems.

[CK-08] "The xv Operating System" by Russ Cox, Frans Kaashek, Robert Morris, Nickolai Zeldovich. From: http://github.com/mit-pdos/xv-base. As mentioned before, a cool and simple Unix implementation. We have used an older version (2012-01-30-1-c41342) and hence some examples in the book may not be the latest in source.

[HT-18] "Fastly later File System Crash Consistency to Produce ACID Transactions" by Y. Hu, J. Lee, Y. Kwon, T. Cheng, Y. Chidambaram, E. Witchel. USENIX AT’18, 2018. The first fast file system at UNIX AT’18, and a great place to start learn about transactional file systems.

[Processes-84] "Processes as Files" by Maurice Uman. The paper that introduced the Unix file system, where each process was created as a file

[Cap-84] "Capability-Based User Systems" by Henry M. Levy. 1984. Available: http://homes.washington.edu/

[ML-94] "All File Systems in Linux" by Marshall McKusik, Joy Levy, 1994. An excellent overview of capability-based systems.

[P-13] "Event Ordering, Application-Level Consistency" by Thamalian Chidambaram, Joshua Young, 2013.

[P-14] "All File Systems Are Not Equal: Crafting Consistency" by Thamalian Chidambaram, 2014. 

[MK-99] "Complexity of Computer Systems" by Saltzer and Kahn, 1999.

[SR05] "Advanced Programming in the Unix Environment" by Richard Stevens and Stephen A. Rago, Addison-Wesley, 2005.

[T-08] "Portably Solving TOCTOU Races with Hardness Amplification" by Dsafrir, Silva, 2008.

# Homework (Code)

In this homework, we'll familiarize ourselves with how the APIs described in the chapter. To do so, you'll just write a few programs, mostly based on utilities.

- 1. **Stat**: Write your version of the command line program *stat*, which simply calls the `stat()` system call on a given file or directory. Print out file size, number of blocks allocated, link count, and so forth. What is the link count of a directory, as the number of entries in the directory changes? Useful interfaces: `stat()`.

- 2. **Files**: Write a program that lists files in the given directory. When called without any arguments, the program should print the filenames. When invoked with the `-l` flag, the program should out information about each file, such as the owner, group, permissions, and other information obtained from the `stat()` call. The program should take one additional argument, which is the directory to read. If no directory is given, the program should use the current working directory. Useful interfaces: `stat()`, `opendir()`, `readdir()`, `getcwd()`.

- 3. **Tail**: Write a program that prints out the last few lines of a file. The program should be efficient, in that it seeks to near the end of the file, reads in a block of data, and then goes backwards until it the requested number of lines; at point, it should print out those lines from beginning to the end of the file. To invoke the program, one should type: `mytail -n file`, where n is the number of lines at the end of the file to print. Useful interfaces: `stat()`, `lseek()`, `open()`, `readdir()`, `close()`.

- 4. **Recursive**: Write a program that prints the names of each file and directory in the file system tree, starting at a given point in the tree. For example, when without arguments, the program should start with the current working directory and print its contents, as well as the contents of any sub-directories, etc., until the entire tree, root at the CWD, is printed. If a single argument of a directory name, use that as the root of the tree instead. Refine your recursive search with more function options, similar to the powerful `find` command line tool.
