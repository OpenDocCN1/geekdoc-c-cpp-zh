+   - Because the i-node number in the directory entry points to an i-node in the same file system, a directory entry can't refer to an i-node in a different file system. This is why the ln(1) command (make a new directory entry that points to an existing file) can't cross file systems. We describe the lnk function in the next section.

+   - When renaming a file without changing file systems, the actual contents of the file need not be moved—all that needs to be done is to add a new directory entry that points to the existing i-node and then unlink the old directory entry. The link count will remain the same. For example, to rename the file /usr/lib/foo to /usr/foo, the contents of the file foo need not be moved if the directories /usr/lib and /usr are on the same file system. This is how the mv(1) command usually operates.

We’ve talked about the concept of a link count for a regular file, but what about the link count field for a directory? Assume that we make a new directory in the working directory, as in

```
$ mkdir testdir
```

Figure 4.15 shows the result. Note that in this figure, we explicitly show the entries for dot and dot-dot.

![](bbox=[0.23, 0.57, 0.9, 0.9])

# Figure 4.15 Sample cylinder group after creating the directory testdir

The i-node whose number is 2549 has a type field of “directory” and a link count equal to 2. Any leaf directory (a directory that does not contain any other directories) always has a link count of 2. The value of 2 comes from the directory entry that names the directory (testdir) and from the entry for dot in that directory. The i-node whose