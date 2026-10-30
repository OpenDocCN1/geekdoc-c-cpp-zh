
If we examine the i-node and data block portion of a cylinder group in more detail, we could have the arrangement shown in Figure 4.14.

![](img/244bf0c3b6d0288ae397336907e37851_147_0.png)

## Figure 4.14 Cylinder group's i-nodes and data blocks in more detail

Note the following points from Figure 4.14.

- Two directory entries point to the same i-node entry. Every i-node has a link count that contains the number of directory entries that point to it. Only when the link count goes to 0 can the file be deleted (thereby releasing the data blocks associated with the file). This is why the operation of “unlinking a file” does not always mean “deleting the blocks associated with the file.” This is why the function that removes a directory entry is called unlink, not delete. In the stat structure, the link count is contained in the st_nlink member. Its primitive system data type is nlink_t. These types of links are called hard links. Recall from Section 2.5.2 that the POSIX.1 constant LINK_MAX specifies the maximum value for a file’s link count.

- The other type of link is called a symbolic link. With a symbolic link, the actual contents of the file—the data blocks—store the name of the file that the symbolic link points to. In the following example, the filename in the directory entry is the three-character string lib and the 7 bytes of data in the file are usr/lib:

  ```
  lrwxrwxrwx 1 root 7 Sep 25 07:14 lib -> usr/lib
  ```

  The file type in the i-node would be S_IFLNK so that the system knows that this is a symbolic link.

- The i-node contains all the information about the file: the file type, the file’s access permission bits, the size of the file, pointers to the file’s data blocks, and so on. Most of the information in the stat structure is obtained from the i-node. Only two items of interest are stored in the directory entry: the filename and the i-node number. The other items—the length of the filename and the length of the directory record—are not of interest to this discussion. The data type for the i-node number is ino_t.

- Because the i-node number in the directory entry points to an i-node in the same file system, a directory entry can't refer to an i-node in a different file system. This is why the ln(1) command (make a new directory entry that points to an existing file) can't cross file systems. We describe the link function in the next section.

- When renaming a file without changing file systems, the actual contents of the file need not be moved—all that needs to be done is to add a new directory entry that points to the existing i-node and then unlink the old directory entry. The link count will remain the same. For example, to rename the file /usr/lib/foo to /usr/foo, the contents of the file foo need not be moved if the directories /usr/lib and /usr are on the same file system. This is how the mv(1) command usually operates.

We’ve talked about the concept of a link count for a regular file, but what about the link count field for a directory? Assume that we make a new directory in the working directory, as in

```
$ mkdir testdir
```

Figure 4.15 shows the result. Note that in this figure, we explicitly show the entries for dot and dot-dot.

![](img/244bf0c3b6d0288ae397336907e37851_148_0.png)

## Figure 4.15 Sample cylinder group after creating the directory testdir

The i-node whose number is 2549 has a type field of “directory” and a link count equal to 2. Any leaf directory (a directory that does not contain any other directories) always has a link count of 2. The value of 2 comes from the directory entry that names the directory (testdir) and from the entry for dot in that directory. The i-node whose number is 1267 has a type field of “directory” and a link count that is greater than or equal to 3. We know that this link count is greater than or equal to 3 because, at a minimum, the i-node is pointed to from the directory entry that names it (which we don’t show in Figure 4.15), from dot, and from dot-dot in the testdir directory. Note that every subdirectory in a parent directory causes the parent directory’s link count to be increased by 1.

This format is similar to the classic format of the UNIX file system, which is described in detail in Chapter 4 of Bach [1986]. Refer to Chapter 7 of McKusick et al. [1996] or Chapter 8 of McKusick and Neville-Neil [2005] for additional information on the changes made with the Berkeley fast file system. See Chapter 15 of McDougall and Mauro [2007] for details on UFS, the Solaris version of the Berkeley fast file system. For information on the HFS file system format used in Mac OS X, see Chapter 12 of Singh [2006].

## 4.15 link, linkat, unlink, unlinkat, and remove Functions

As we saw in the previous section, a file can have multiple directory entries pointing to its i-node. We can use either the link function or the linkat function to create a link to an existing file.

```
#include <unistd.h>

int link(const char *existingpath, const char *newpath);
int linkat(int olddirfd, const char *existingpath, int newdirfd, const char *newpath, int flag);

Both return: 0 if OK, -1 on error
```

These functions create a new directory entry, newpath, that references the existing file existingpath. If the newpath already exists, an error is returned. Only the last component of the newpath is created. The rest of the path must already exist.

With the linkat function, the existing file is specified by both the olddirfd and existingpath arguments, and the new pathname is specified by both the newdirfd and newpath arguments. By default, if either pathname is relative, it is evaluated relative to the corresponding file descriptor. If either file descriptor is set to AT_FDCWD, then the corresponding pathname, if it is a relative pathname, is evaluated relative to the current directory. If either pathname is absolute, then the corresponding file descriptor argument is ignored.

When the existing file is a symbolic link, the flag argument controls whether the linkat function creates a link to the symbolic link or to the file to which the symbolic link points. If the AT_SYMLINK_FOLLOW flag is set in the flag argument, then a link is created to the target of the symbolic link. If this flag is clear, then a link is created to the symbolic link itself.

## Example

The program shown in Figure 4.16 opens a file and then unlinks it. The program then goes to sleep for 15 seconds before terminating.

```
#include "apue.h"
#include <fcntl.h>
int
main(void)
{
    if (open("tempfile", O_RDWR) < 0)
        err_sys("open error");
    if (unlink("tempfile") < 0)
        err_sys("unlink error");
    printf("file unlinked\n");
    sleep(15);
    printf("done\n");
    exit(0);
}
```

Figure 4.16 Open a file and then unlink it

Running this program gives us

```
$ ls -l tempfile                look at how big the file is
-rw-r--r-- 1 sar 413265408 Jan 21 07:14 tempfile
$ df /home                       check how much free space is available
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/hda4      11021440 1956332  9065108 18% /home
$ ./a.out &                      run the program in Figure 4.16 in the background
1364                           the shell prints its process ID
$ file unlinked                  the file is unlinked
$ ls -l tempfile                 see if the filename is still there
ls: tempfile: No such file or directory  the directory entry is gone
$ df /home                       see if the space is available yet
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/hda4      11021440 1956332  9065108 18% /home
$ done                           the program is done, all open files are closed
df /home                         now the disk space should be available
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/hda4      11021440 1552352  9469088 15% /home
                               now the 394.1 MB of disk space are available
```

This property of unlink is often used by a program to ensure that a temporary file it creates won't be left around in case the program crashes. The process creates a file using either open or creat and then immediately calls unlink. The file is not deleted, however, because it is still open. Only when the process either closes the file or terminates, which causes the kernel to close all its open files, is the file deleted.

If pathname is a symbolic link, unlink removes the symbolic link, not the file referenced by the link. There is no function to remove the file referenced by a symbolic link given the name of the link.
