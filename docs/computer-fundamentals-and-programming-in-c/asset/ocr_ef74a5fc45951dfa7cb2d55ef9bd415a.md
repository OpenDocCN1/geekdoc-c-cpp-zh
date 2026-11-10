```
gets(newname);

/* Rename the file */
if(rename(oldname, newname) == 0)
    printf("Renamed %s to %s.\n", oldname, newname);
else
    perror("rename");
    return 0;
}
```

+   **Note**
+   - The copy and delete operations are also associated with file management.
+   - In case of `remove()` function, the only precondition is that the specified file must not be open.
+   - The only restriction in `rename()` function is that both names must refer to the same disk drive; a file cannot be renamed on a different disk drive.

# 15.9 LOW-LEVEL I/O

This form of I/O is unbuffered. This means that, each read or write request results in accessing the disk (or device) directly to fetch/put a specific number of bytes. There are no formatting facilities. Instead of file pointers, we use low-level file handles or file descriptors, which give a unique integer number to identify each file.

To open a file the following function is used.

`int open(char *filename, int flag, int perms);`

The above function returns a file descriptor or -1 for a failure. The flag controls the file access and has the following predefined in `fcntl.h`: `O_APPEND`, `O_CREAT`, `O_EXCL`, `O_RDONLY`, `O_RDWR`, `O_WRONLY`, and others. `perms` is best set to 0 for most of our applications.

The function

`creat(char *filename, int perms);`

can also be used to create a file.

`int close(int handle);`

can be used to close a file.

The following functions are used to read/write a specific number of bytes from a file stored or to be put in the memory location specified by buffer.

`int read(int handle, char *buffer, unsigned length);`

`int write(int handle, char *buffer, unsigned length);`

The `sizeof()` function is commonly used to specify the length. The `read()` and `write()` functions return the number of bytes read/written or -1 if they fail.

+   **Note**
+   - Low-level I/O has no formatting facilities.
+   - Instead of file pointers, low-level file handles or file descriptors, which give a unique integer number to identify each file, are used.

# SUMMARY

Data can also be stored in disk files. C treats a disk file like a stream (a sequence of characters), just like the predefined streams stdin, stdout, and stderr. A stream associated with a disk file must be opened using the fopen() library function before it can be used, and it must be closed after use through the fclose() function. A disk file stream can be opened either in text or in binary mode.

After a disk file has been opened, data can be read from the file, written into the file, or both. Data can be accessed either in a sequential manner or in a random manner. Each open disk file has an associated file position indicator. This indicator specifies the position in the file, measured as the number of bytes from the start of the file, where subsequent read and write operations occur. With some cases, the position indicator is updated automatically by the system, and programmers do not have to be bothered with it. For random file access, the C standard library provides functions such as fseek(), ftell(), and rewind() for manipulating the position indicator.

Finally, C provides some rudimentary file management functions, allowing deletion and renaming of disk files. Low-level file handling functions that do not use formatting and file position indicators are also available.

# KEY TERMS

**Binary file**  It is a collection of bytes or a character stream. The data that is written into and read from binary file remains unchanged, with no separation between lines and no use of end-of-line characters and the interpretation of the file is left to the programmer.

**Buffer**  It is a block of memory used for temporary storage of data being written to and read from the file. It serves as an interface between the stream (which is character-oriented) and the disk hardware (which is block-oriented).

**File management**  It refers to all operations related to creating, renaming, deleting, merging, reading, writing, etc. of any type of files.

**Path**  It specifies the drive and/or directory (or folder) where the file is located. On PCs, the backslash character is used to separate directory names in a path. Some systems like UNIX use the forward slash (/) as the directory separator.

**Random file access**  It means reading from or writing to any position in a file without reading or writing all the preceding data by controlling the position indicator.

**Record**  It consists of a collection of data fields that conforms to a previously defined structure that can be stored on or retrieved from a file.