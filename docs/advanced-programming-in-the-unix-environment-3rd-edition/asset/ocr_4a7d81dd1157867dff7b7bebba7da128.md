+   3. If either oldname or newname refers to a symbolic link, then the link itself is processed, not the file to which it resolves.
+   4. We can’t rename dot or dot-dot. More precisely, neither dot nor dot-dot can appear as the last component of oldname or newname.
+   5. As a special case, if oldname and newname refer to the same file, the function returns successfully without changing anything.

If newname already exists, we need permissions as if we were deleting it. Also, because we’re removing the directory entry for oldname and possibly creating a directory entry for newname, we need write permission and execute permission in the directory containing oldname and in the directory containing newname.

The renameat function provides the same functionality as the rename function, except when either oldname or newname refers to a relative pathname. If oldname specifies a relative pathname, it is evaluated relative to the directory referenced by oldfd. Similarly, newname is evaluated relative to the directory referenced by newfd if newname specifies a relative pathname. Either the oldfd or newfd arguments (or both) can be set to AT_FDCWD to evaluate the corresponding pathname relative to the current directory.

# 4.17 Symbolic Links

A symbolic link is an indirect pointer to a file, unlike the hard links described in the previous section, which pointed directly to the i-node of the file. Symbolic links were introduced to get around the limitations of hard links.

+   - Hard links normally require that the link and the file reside in the same file system.
+   - Only the superuser can create a hard link to a directory (when supported by the underlying file system).

There are no file system limitations on a symbolic link and what it points to, and anyone can create a symbolic link to a directory. Symbolic links are typically used to “move” a file or an entire directory hierarchy to another location on a system.

When using functions that refer to a file by name, we always need to know whether the function follows a symbolic link. If the function follows a symbolic link, a pathname argument to the function refers to the file pointed to by the symbolic link. Otherwise, a pathname argument refers to the link itself, not the file pointed to by the link. Figure 4.17 summarizes whether the functions described in this chapter follow a symbolic link. The functions mkdir, mkfifo, mknod, and rmdir do not appear in this figure, as they return an error when the pathname is a symbolic link. Also, the functions that take a file descriptor argument, such as fstat and fchmod, are not listed, as the function that returns the file descriptor (usually open) handles the symbolic link. Historically, implementations have differed in whether chown follows symbolic links. In all modern systems, however, chown does follow symbolic links.