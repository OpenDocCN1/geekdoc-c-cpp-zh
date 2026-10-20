
The `open()` system call follows a symbolic link and accesses the data or attributes of the file that the link points to. If you want to read the data or attributes of a symbolic link, you must use the `readlink()` system call. Similarly, the `creat()` system call can create only an ordinary file. If you want to create a symbolic link, you should use the `symlink()` system call. You should browse through the man pages of these calls to learn more about them.

## Exercise 15.6

Give the prototypes of the `symlink()` and `readlink()` system call. Briefly describe each parameter for these calls.

## 15.8.2 Closing a File

You can close a file by using the `close()` system call, which takes a file’s descriptor as an argument and deallocates the PPFDT slot corresponding to the given descriptor. The following is a brief description of the call:

```
#include <unistd.h>
int close(int fd);

Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

The `close()` system call may fail for several reasons. Two commonly occurring reasons are given in Table 15.5, along with the symbolic values of the `errno` variable corresponding to these errors.

If an open file is being referenced by more than one process—that is, if entries in multiple PPFDTs are pointing to an entry in the SFT—then closing the file would only deallocate the entry in the relevant PPFDT and decrement the reference count by 1. A file is closed only when this reference count becomes 0. When a process terminates, the kernel automatically closes all of its open files.

In the following example, we open the file passed as the only command line argument, display the file descriptor of the file, and close the file. The compilation and execution of the example program shows the program output. We use the compiler command with the -w option in order to suppress the warning messages.

```
$ cat open_close.c
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int fd;

        /* Open file */
        if (argc == 1) {
                printf("No file specified as command line argument.\n");
                exit(1);
        }
        if ((fd = open(argv[1], O_RDWR)) == -1) {
                perror("File opening");
```

**TABLE 15.5**  
Commonly Occurring Reasons for the Failure of the `close()` System Call

| Reason for Failure | Value of `errno` |
|---|---|
| `fd` is not an active descriptor, i.e., does not correspond to an open file | `EBADF` |
| The file-closing operation was interrupted by a signal | `EINTR` |

```
exit(1);
} else
        printf("The file descriptor is %d.\n",fd);
/* Close file */
if (close(fd) == -1) {
        perror("File closing");
        exit(1);
}
else
        printf("File closed successfully.\n");
exit(0);
}
$ gcc open_close.c -w
$ man talk > foobar
$ a.out foobar
The file descriptor is 3.
File closed successfully.
$
```

Note that this is the first (and the only) file that the process has opened. Since the kernel has already opened the standard files for this process, the kernel allocated file descriptor 3 when the program opened **foobar**.

We now modify the program slightly so that it first closes standard input and then opens the file passed to it as a command line argument. In order to do so, we only need to insert the following line before the open() system call:

```
close(0);
```

Here is the updated program:

```
$ cat open_close_new.c
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        int fd;

        /* Open file */
        if (argc == 1) {
                printf("No file specified as command line argument.\n");
                exit(1);
        }
        close(0); /* Close standard input */
        if ((fd = open(argv[1], O_RDWR)) == -1) {
                perror("File opening");
                exit(1);
        } else
                printf("The file descriptor is %d.\n",fd);
        /* Close file */
        if (close(fd) == -1) {
                perror("File closing");
                exit(1);
        }
        else
                printf("File closed successfully.\n");
        exit(0);
}
$ gcc open_close_new.c -w
$ a.out foobar
The file descriptor is 0.
```

```
File closed successfully.
$
```

As you can see, as expected, the kernel allocated file descriptor 0 to the newly opened file **foobar**.

## Exercise 15.7

Compile and run the programs given in Sections 15.8.1 and 15.8.2. Do they work as intended?

## 15.8.3 Reading from a File

Once a file has been opened using the open() system call, you can read its contents by using the read() system call. Here is a brief description of the read() call.

```
#include <sys/types.h>
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t nbytes);

Success: 0

Failure: -1 and kernel variable errno set to indicate the type of error
```

This call tries to read nbytes bytes from the file with the file descriptor fd into the main memory area pointed to by buf. The data is read starting with the current location of the read/write file pointer. Upon completion, the read() call returns the number of bytes actually read, which may be less than nbytes. The file pointer advances by the number of bytes actually read. For a regular file, the call guarantees reading nbytes if the file has these many bytes left before the end-of-file (EOF). However, with other files, such as pipes or sockets (see Chapters 16, W20, and W21), this is not guaranteed. The read() system call returns 0 when it encounters EOF.

On failure, read() returns -1 and errno is set to indicate the reason for failure. Table 15.6 shows some common reasons for the read() call to fail for regular files.

## 15.8.4 Writing to a File

Once a file has been opened using the open() or creat() system call, you can write to it using the write() system call. Here is a brief description of the write() call:

```
#include <sys/types.h>
#include <unistd.h>
ssize_t write(int fd, const void *buf, size_t nbytes);

Success: 0

Failure: -1 and kernel variable errno set to indicate the type of error
```

# TABLE 15.6

Some Common Reasons for the read() System Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| The fd argument is not a valid descriptor for reading | EBADF |
| The buf argument points to a memory location outside the process address space | EFAULT |
| An I/O error occurred while reading from the file system | EIO |
| The file reading operation was interrupted | EINTR |
| The pointer associated with the fd argument is negative | EINVAL |
| The nbytes value is greater than INT_MAX, i.e., the maximum value of an integer | EINVAL |

# TABLE 15.7

Some Common Reasons for the write() System Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| The fd argument is not a valid descriptor for writing | EBADF |
| The fd argument is associated with a negative pointer | EINVAL |
| File size limit for the process or the maximum file size limit has reached | EFBIG |
| The file system containing the file is full | ENOSPC |
| The user's quota of disk blocks on the file system containing the file has been exhausted | EDQUOT |
| An I/O error occurred while reading from the file system | EIO |
| The file reading operation was interrupted | EINTR |
| The nbytes value is greater than INT_MAX, i.e., the maximum value of an integer | EINVAL |

This call tries to write nbytes bytes from the main memory area pointed to by buf to the file with the file descriptor fd. The data is written starting with the current location of the read/write file pointer. Upon completion, the write() call returns the number of bytes actually written, which may be less than nbytes. The file pointer advances by the number of bytes actually written. For a regular file, the call guarantees writing nbytes if the disk is not full or the file size has not exceeded the maximum file size supported by the Linux system. However, with other files, such as sockets (see Chapter W20), this is not guaranteed.

On failure, write() returns -1 and errno is set to indicate the reason for failure. Table 15.7 shows some common reasons for the read() call to fail for regular files.

We now enhance the open_close.c program and convert it into a file copy program, cpy, with the following syntax:

```
cpy source target
```

The program copies the source file, an existing file, to the target file, a nonexistent file. The compilation and execution of the example program show the program output.

```
$ cat cpy.c
#include <fcntl.h>
#include <unistd.h>

#define SIZE 512

void closefd(int);

int main(int argc, char *argv[])
{
    int rfd, wfd, nr, nw;
    char buf[SIZE];

    if (argc != 3) {
        printf("Inappropriate number of command line arguments.\n");
        exit(0);
    }
    /* Open the source file for reading */
    if ((rfd = open(argv[1], O_RDONLY)) == -1) {
        perror("Source file opening");
        exit(1);
    }
    /* Open the destination file for writing */
    if ((wfd = open(argv[2], O_CREAT | O_WRONLY | O_TRUNC, 0666)) == -1) {
        perror("Creation and opening of destination file");
        exit(1);
    }
}
