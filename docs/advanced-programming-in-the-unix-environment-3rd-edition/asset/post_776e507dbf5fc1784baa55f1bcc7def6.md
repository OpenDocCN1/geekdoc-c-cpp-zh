
The superuser can call `unlink` with *pathname* specifying a directory if the file system supports it, but the function `rmdir` should be used instead to unlink a directory. We describe the `rmdir` function in Section 4.21.

We can also unlink a file or a directory with the `remove` function. For a file, `remove` is identical to `unlink`. For a directory, `remove` is identical to `rmdir`.

```c
#include <stdio.h>

int remove(const char *pathname);
                             Returns: 0 if OK, −1 on error
```

ISO C specifies the `remove` function to delete a file. The name was changed from the historical UNIX name of `unlink` because most non-UNIX systems that implement the C standard didn’t support the concept of links to a file at the time.

## 4.16 rename and renameat Functions

A file or a directory is renamed with either the `rename` or `renameat` function.

```c
#include <stdio.h>

int rename(const char *oldname, const char *newname);

int renameat(int oldfd, const char *oldname, int newfd,
             const char *newname);

                                  Both return: 0 if OK, −1 on error
```

The `rename` function is defined by ISO C for files. (The C standard doesn’t deal with directories.) POSIX.1 expanded the definition to include directories and symbolic links.

There are several conditions to describe these functions, depending on whether *oldname* refers to a file, a directory, or a symbolic link. We must also describe what happens if *newname* already exists.

- 1. If *oldname* specifies a file that is not a directory, then we are renaming a file or a symbolic link. In this case, if *newname* exists, it cannot refer to a directory. If *newname* exists and is not a directory, it is removed, and *oldname* is renamed to *newname*. We must have write permission for the directory containing *oldname* and the directory containing *newname*, since we are changing both directories.
- 2. If *oldname* specifies a directory, then we are renaming a directory. If *newname* exists, it must refer to a directory, and that directory must be empty. (When we say that a directory is empty, we mean that the only entries in the directory are dot and dot-dot.) If *newname* exists and is an empty directory, it is removed, and *oldname* is renamed to *newname*. Additionally, when we’re renaming a directory, *newname* cannot contain a path prefix that names *oldname*. For example, we can’t rename `/usr/foo` to `/usr/foo/testdir`, because the old name (`/usr/foo`) is a path prefix of the new name and cannot be removed.
- 3. If either oldname or newname refers to a symbolic link, then the link itself is processed, not the file to which it resolves.
- 4. We can’t rename dot or dot-dot. More precisely, neither dot nor dot-dot can appear as the last component of oldname or newname.
- 5. As a special case, if oldname and newname refer to the same file, the function returns successfully without changing anything.

If newname already exists, we need permissions as if we were deleting it. Also, because we’re removing the directory entry for oldname and possibly creating a directory entry for newname, we need write permission and execute permission in the directory containing oldname and in the directory containing newname.

The renameat function provides the same functionality as the rename function, except when either oldname or newname refers to a relative pathname. If oldname specifies a relative pathname, it is evaluated relative to the directory referenced by oldfd. Similarly, newname is evaluated relative to the directory referenced by newfd if newname specifies a relative pathname. Either the oldfd or newfd arguments (or both) can be set to AT_FDCWD to evaluate the corresponding pathname relative to the current directory.

## 4.17 Symbolic Links

A symbolic link is an indirect pointer to a file, unlike the hard links described in the previous section, which pointed directly to the i-node of the file. Symbolic links were introduced to get around the limitations of hard links.

- Hard links normally require that the link and the file reside in the same file system.
- Only the superuser can create a hard link to a directory (when supported by the underlying file system).

There are no file system limitations on a symbolic link and what it points to, and anyone can create a symbolic link to a directory. Symbolic links are typically used to “move” a file or an entire directory hierarchy to another location on a system.

When using functions that refer to a file by name, we always need to know whether the function follows a symbolic link. If the function follows a symbolic link, a pathname argument to the function refers to the file pointed to by the symbolic link. Otherwise, a pathname argument refers to the link itself, not the file pointed to by the link. Figure 4.17 summarizes whether the functions described in this chapter follow a symbolic link. The functions mkdir, mkfifo, mknod, and rmdir do not appear in this figure, as they return an error when the pathname is a symbolic link. Also, the functions that take a file descriptor argument, such as fstat and fchmod, are not listed, as the function that returns the file descriptor (usually open) handles the symbolic link. Historically, implementations have differed in whether chown follows symbolic links. In all modern systems, however, chown does follow symbolic links.

Symbolic links were introduced with 4.2BSD. Initially, chown didn’t follow symbolic links, but this behavior was changed in 4.4BSD. System V included support for symbolic links in SVR4, but diverged from the original BSD behavior by implementing chown to follow symbolic links. In older versions of Linux (those before version 2.1.81), chown didn’t follow symbolic links. From version 2.1.81 onward, chown follows symbolic links. With FreeBSD 8.0, Mac OS X 10.6.8, and Solaris 10, chown follows symbolic links. All of these platforms provide implementations of lchown to change the ownership of symbolic links themselves.

| Function | Does not follow symbolic link | Follows symbolic link |
|---|---|---|
| access |  | • |
| chdir |  | • |
| chmod |  | • |
| chown |  | • |
| creat |  | • |
| exec |  | • |
| lchown | • |  |
| link |  | • |
| lstat | • |  |
| open |  | • |
| opendir |  | • |
| pathconf |  | • |
| readlink | • |  |
| remove | • |  |
| rename | • |  |
| stat |  | • |
| truncate |  | • |
| unlink | • |  |

Figure 4.17 Treatment of symbolic links by various functions

One exception to the behavior summarized in Figure 4.17 occurs when the open function is called with both O_CREAT and O_EXCL set. In this case, if the pathname refers to a symbolic link, open will fail with errno set to EEXIST. This behavior is intended to close a security hole so that privileged processes can’t be fooled into writing to the wrong files.

### Example

It is possible to introduce loops into the file system by using symbolic links. Most functions that look up a pathname return an errno of ELOOP when this occurs. Consider the following commands:

```
$ mkdir foo                  make a new directory
$ touch foo/a                create a 0-length file
$ ln -s ../foo foo/testdir   create a symbolic link
$ ls -l foo
total 0
-rw-r--r-- 1 sar 0 Jan 22 00:16 a
lrwxrwxrwx 1 sar 6 Jan 22 00:16 testdir -> ../foo
```

This creates a directory foo that contains the file a and a symbolic link that points to foo. We show this arrangement in Figure 4.18, drawing a directory as a circle and a file as a square.

![](img/244bf0c3b6d0288ae397336907e37851_155_0.png)

Figure 4.18 Symbolic link testdir that creates a loop

If we write a simple program that uses the standard function ftw(3) on Solaris to descend through a file hierarchy, printing each pathname encountered, the output is

```
foo
foo/a
foo/testdir
foo/testdir/a
foo/testdir/testdir
foo/testdir/testdir/a
foo/testdir/testdir/testdir
foo/testdir/testdir/testdir/a
(many more lines until we encounter an ELOOP error)
```

In Section 4.22, we provide our own version of the ftw function that uses lstat instead of stat, to prevent it from following symbolic links.

> Note that on Linux, the ftw and nftw functions record all directories seen and avoid processing a directory more than once, so they don't display this behavior.

A loop of this form is easy to remove. We can unlink the file foo/testdir, as unlink does not follow a symbolic link. But if we create a hard link that forms a loop of this type, its removal is much more difficult. This is why the link function will not form a hard link to a directory unless the process has superuser privileges.

> Indeed, Rich Stevens did this on his own system as an experiment while writing the original version of this section. The file system got corrupted and the normal fsck(1) utility couldn't fix things. The deprecated tools clri(8) and decheck(8) were needed to repair the file system.

> The need for hard links to directories has long since passed. With symbolic links and the mkdir function, there is no longer any need for users to create hard links to directories.

When we open a file, if the pathname passed to open specifies a symbolic link, open follows the link to the specified file. If the file pointed to by the symbolic link doesn't exist, open returns an error saying that it can't open the file. This response can confuse users who aren't familiar with symbolic links. For example,
