The third argument (...) in the prototype of the open() call means that the number and type of remaining arguments may vary. The mode argument in the creat() call is used to specify the access permissions (see Chapter 5) for the newly created file. Both calls return a nonnegative integer called the file descriptor of the opened file, which can be used to perform the desired I/O operations by using the read() and write() system calls (discussed later), change the position of the read/write file pointer for random access, and close the file using the close() system call. The returned descriptor is the first unused descriptor in the PPFDT, starting with descriptor 0. If the file opens successfully, the read/write file pointer is set to the beginning of the file. It means that the first read or write operation starts at the first byte of the file. Both calls return -1 on failure.

Bitwise ORing two or more constants listed in the <fcntl.h> file forms the flag argument. Table 15.3 shows some of the commonly used flags used for file I/O and their meanings.

The open() call may fail for several reasons. Some of the commonly occurring reasons for the call to fail for regular files are given in Table 15.4, along with the corresponding symbolic values saved in the errno variable.

Since the creat() system call creates a file and, by default, opens it for writing only, the following calls are equivalent to each other:

```
creat(pathname, mode);
open(pathname, O_WRONLY | O_CREAT | O_TRUNC, mode);
```

# TABLE 15.3

Commonly Used Flags for File I/O

| Flag | Meaning |
|---|---|
| O_RDONLY | Open the file for reading only |
| O_WRONLY | Open the file for writing only |
| O_RDWR | Open the file for reading and writing |
| O_CREAT | Create the file if it does not exist. If you use this option, you must specify the access permissions for the newly created file as the third argument, mode |
| O_APPEND | Each write operation appends at the end of file |
| O_TRUNC | If the file exists, its length is set to 0. Previous file contents are not accessible anymore |

# TABLE 15.4

A Few Common Reasons for the Failure of the open() System Call

| Reason for Failure | Value of errno |
|---|---|
| A component in the path does not exist | ENOENT |
| A component in the path is not a directory | ENOTDIR |
| The named file is a directory | EISDIR |
| Search permission is not set on a component in the path | EACCESS |
| The process has already opened the maximum number of files allowed by the system, i.e., the PPFDT is already full | EMFILE |
| The system has already reached the limit of the maximum number of files that may be opened on it simultaneously (i.e., the SFT is full) | EMFILE |
| The file opening operation was interrupted by a signal | EINTR |
| A component in path exceeds the file name size limit (255 characters) or the entire path exceeds the 1,023 characters | ENAMETOOLONG |
| The named file is a special file, but the device associated with the file does not exist | ENXIO |
| O_CREAT flag is specified to create a file but the file system is read only | EROFS |
| O_CREAT flag is specified and error occurred while creating an inode for the new file or making the directory entry for the file to be created | EIO |
| O_CREAT and O_EXCL flags are specified and the file specified in path exists | EEXIST |