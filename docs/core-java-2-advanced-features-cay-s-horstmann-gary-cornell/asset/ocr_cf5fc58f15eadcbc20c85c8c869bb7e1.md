To get these attributes, call

```
    BasicFileAttributes attributes = Files.readAttributes(path, BasicFileAttributes.class);
```

If you know that the user’s file system is POSIX-compliant, you can instead get
an instance of PosixFileAttributes:

```
    PosixFileAttributes attributes = Files.readAttributes(path, PosixFileAttributes.class);
```

Then you can find out the group owner and the owner, group, and world access
permissions of the file. We won’t dwell on the details since so much of this
information is not portable across operating systems.

| java.nio.file.Files 7 |
| --- |
| • static boolean exists(Path path) |
| • static boolean isHidden(Path path) |
| • static boolean isReadable(Path path) |
| • static boolean isWritable(Path path) |
| • static boolean isExecutable(Path path) |
| • static boolean isRegularFile(Path path) |
| • static boolean isDirectory(Path path) |
| • static boolean isSymbolicLink(Path path)<br>checks for the given property of the file given by the path. |
| • static long size(Path path)<br>gets the size of the file in bytes. |
| • `A readAttributes(Path path, Class<A> type, LinkOption... options)`<br>reads the file attributes of type A. |

| java.nio.file.attribute.BasicFileAttributes 7 |
| --- |
| • FileTime creationTime() |
| • FileTime lastAccessTime() |
| • FileTime lastModifiedTime() |
| • boolean isRegularFile() |
| • boolean isDirectory() |
| • boolean isSymbolicLink() |
| • long size() |
| • Object fileKey()<br>gets the requested attribute. |