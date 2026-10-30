# 3.7 **read Function**

Data is read from an open file with the read function.

```
```c
#include <unistd.h>

ssize_t read(int fd, void *buf, size_t nbytes);

Returns: number of bytes read, 0 if end of file, −1 on error
```
```

If the read is successful, the number of bytes read is returned. If the end of file is encountered, 0 is returned.

There are several cases in which the number of bytes actually read is less than the amount requested:

+   - When reading from a regular file, if the end of file is reached before the requested number of bytes has been read. For example, if 30 bytes remain until the end of file and we try to read 100 bytes, read returns 30. The next time we call read, it will return 0 (end of file).
+   - When reading from a terminal device. Normally, up to one line is read at a time. (We’ll see how to change this default in Chapter 18.)
+   - When reading from a network. Buffering within the network may cause less than the requested amount to be returned.
+   - When reading from a pipe or FIFO. If the pipe contains fewer bytes than requested, read will return only what is available.
+   - When reading from a record-oriented device. Some record-oriented devices, such as magnetic tape, can return up to a single record at a time.
+   - When interrupted by a signal and a partial amount of data has already been read. We discuss this further in Section 10.5.

The read operation starts at the file’s current offset. Before a successful return, the offset is incremented by the number of bytes actually read.

POSIX.1 changed the prototype for this function in several ways. The classic definition is

```
```c
int read(int fd, char *buf, unsigned nbytes);
```
```

+   - First, the second argument was changed from char * to void * to be consistent with ISO C: the type void * is used for generic pointers.
+   - Next, the return value was required to be a signed integer (ssize_t) to return a positive byte count, 0 (for end of file), or −1 (for an error).
+   - Finally, the third argument historically has been an unsigned integer, to allow a 16-bit implementation to read or write up to 65,535 bytes at a time. With the 1990 POSIX.1 standard, the primitive system data type ssize_t was introduced to provide the signed return value, and the unsigned size_t was used for the third argument. (Recall the SSIZE_MAX constant from Section 2.5.2.)