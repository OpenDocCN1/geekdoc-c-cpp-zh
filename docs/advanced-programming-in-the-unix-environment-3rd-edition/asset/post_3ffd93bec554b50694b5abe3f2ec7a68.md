
## 14.6 `readv` and `writev` Functions

The readv and writev functions let us read into and write from multiple noncontiguous buffers in a single function call. These operations are called *scatter read* and *gather write*.

```
#include <sys/uio.h>

ssize_t readv(int fd, const struct iovec *iov, int iovcnt);

ssize_t writev(int fd, const struct iovec *iov, int iovcnt);
```

Both return: number of bytes read or written, −1 on error

The second argument to both functions is a pointer to an array of iovec structures:

```
struct iovec {
    void   *iov_base;   /* starting address of buffer */
    size_t  iov_len;    /* size of buffer */
};
```

The number of elements in the *iov* array is specified by *iovcnt*. It is limited to IOV_MAX (recall Figure 2.11). Figure 14.22 shows a diagram relating the arguments to these two functions and the iovec structure.

![](img/244bf0c3b6d0288ae397336907e37851_554_0.png)

The writev function gathers the output data from the buffers in order: iov[0], iov[1], through iov[iovcnt−1]; writev returns the total number of bytes output, which should normally equal the sum of all the buffer lengths. The readv function scatters the data into the buffers in order, always filling one buffer before proceeding to the next. readv returns the total number of bytes that were read. A count of 0 is returned if there is no more data and the end of file is encountered.

> These two functions originated in 4.2BSD and were later added to SVR4. These two functions are included in the XSI option of the Single UNIX Specification.

## Example

In Section 20.8, in the function `_db_writeidx`, we need to write two buffers consecutively to a file. The second buffer to output is an argument passed by the caller, and the first buffer is one we create, containing the length of the second buffer and a file offset of other information in the file. There are three ways we can do this.

- 1. Call `write` twice, once for each buffer.
- 2. Allocate a buffer of our own that is large enough to contain both buffers, and copy both into the new buffer. We then call `write` once for this new buffer.
- 3. Call `writev` to output both buffers.

The solution we use in Section 20.8 is to use `writev`, but it’s instructive to compare it to the other two solutions.

Figure 14.23 shows the results from the three methods just described.

| Operation | Linux (Intel x86) |  |  | Mac OS X (Intel x86) |  |  |
|---|---:|---:|---:|---:|---:|---:|
|  | User | System | Clock | User | System | Clock |
| two writes | 0.06 | 2.04 | 2.13 | 0.85 | 8.33 | 13.83 |
| buffer copy, then one write | 0.03 | 1.13 | 1.16 | 0.70 | 4.87 | 9.25 |
| one writev | 0.04 | 1.21 | 1.26 | 0.43 | 5.34 | 9.24 |

**Figure 14.23** Timing results comparing `writev` and other techniques

The test program that we measured output a 100-byte header followed by 200 bytes of data. This was done 1,048,576 times, generating a 300-megabyte file. The test program has three separate cases—one for each of the techniques measured in Figure 14.23. We used times (Section 8.17) to obtain the user CPU time, system CPU time, and wall clock time before and after the writes. All three times are shown in seconds.

As we expect, the system time increases when we call `write` twice, compared to calling either `write` or `writev` once. This correlates with the results in Figure 3.6.

Next, note that the sum of the CPU times (user plus system) is slightly less when we do a buffer copy followed by a single write compared to a single call to `writev`. With the single write, we copy the buffers to a staging buffer at user level, and then the kernel will copy the data to its internal buffers when we call `write`. With `writev`, we should do less copying, because the kernel only needs to copy the data directly into its staging buffers. The fixed cost of using `writev` for such small amounts of data, however, is greater than the benefit. As the amount of data we need to copy increases, the more expensive it will be to copy the buffers in our program, and the `writev` alternative will be more attractive.

> Don’t infer too much about the relative performance of Linux and Mac OS X from the numbers shown in Figure 14.23. The two computers were very different: they had different processor generations, different amounts of RAM, and disks with different speeds. To do an apples-to-apples comparison of one operating system to another, we need to use the same hardware for each operating system.

of file while reading, we return the number of bytes copied to the caller’s buffer if we already read some data successfully and have not yet satisfied the amount requested.

```
#include "apue.h"

ssize_t                 /* Read "n" bytes from a descriptor */
readn(int fd, void *ptr, size_t n)
{
    size_t      nleft;
    ssize_t     nread;

    nleft = n;
    while (nleft > 0) {
        if ((nread = read(fd, ptr, nleft)) < 0) {
            if (nleft == n)
                return(-1);      /* error, return -1 */
            else
                break;           /* error, return amount read so far */
        } else if (nread == 0) {
            break;               /* EOF */
        }
        nleft -= nread;
        ptr   += nread;
    }
    return(n - nleft);          /* return >= 0 */
}

ssize_t                 /* Write "n" bytes to a descriptor */
writen(int fd, const void *ptr, size_t n)
{
    size_t      nleft;
    ssize_t     nwritten;

    nleft = n;
    while (nleft > 0) {
        if ((nwritten = write(fd, ptr, nleft)) < 0) {
            if (nleft == n)
                return(-1);      /* error, return -1 */
            else
                break;           /* error, return amount written so far */
        } else if (nwritten == 0) {
            break;
        }
        nleft -= nwritten;
        ptr   += nwritten;
    }
    return(n - nleft);          /* return >= 0 */
}
```

Figure 14.24 The readn and writen functions

## 14.8 Memory-Mapped I/O

Memory-mapped I/O lets us map a file on disk into a buffer in memory so that, when we fetch bytes from the buffer, the corresponding bytes of the file are read. Similarly, when we store data in the buffer, the corresponding bytes are automatically written to the file. This lets us perform I/O without using read or write.

Memory-mapped I/O has been in use with virtual memory systems for many years. In 1981, 4.1BSD provided a different form of memory-mapped I/O with its vread and vwrite functions. These two functions were then removed in 4.2BSD and were intended to be replaced with the mmap function. The mmap function, however, was not included with 4.2BSD (for reasons described in Section 2.5 of McKusick et al. [1996]). Gingell, Moran, and Shannon [1987] describe one implementation of mmap. Version 4 of the Single UNIX Specification moved the mmap function from an option to the base specification. All POSIX-conforming systems are required to support it.

To use this feature, we have to tell the kernel to map a given file to a region in memory. This task is handled by the mmap function.

```
#include <sys/mman.h>
void *mmap(void *addr, size_t len, int prot, int flag, int fd, off_t off);
Returns: starting address of mapped region if OK, MAP_FAILED on error
```

The addr argument lets us specify the address where we want the mapped region to start. We normally set this value to 0 to allow the system to choose the starting address. The return value of this function is the starting address of the mapped area.
The fd argument is the file descriptor specifying the file that is to be mapped. We have to open this file before we can map it into the address space. The len argument is the number of bytes to map, and off is the starting offset in the file of the bytes to map. (Some restrictions on the value of off are described later.)
The prot argument specifies the protection of the mapped region.

| prot | Description |
|---|---|
| PROT_READ | Region can be read. |
| PROT_WRITE | Region can be written. |
| PROT_EXEC | Region can be executed. |
| PROT_NONE | Region cannot be accessed. |

Figure 14.25 Protection of memory-mapped region

We can specify the protection as either PROT_NONE or the bitwise OR of any combination of PROT_READ, PROT_WRITE, and PROT_EXEC. The protection specified for a region can't allow more access than the open mode of the file. For example, we can't specify PROT_WRITE if the file was opened read-only.

Before looking at the flag argument, let's see what's going on here. Figure 14.26 shows a memory-mapped file. (Recall the memory layout of a typical process, shown in Figure 7.6.) In this figure, "start addr" is the return value from mmap. We have shown
