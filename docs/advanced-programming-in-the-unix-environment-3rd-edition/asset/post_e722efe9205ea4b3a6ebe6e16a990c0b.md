
![](img/244bf0c3b6d0288ae397336907e37851_559_0.png)

The mapped memory being somewhere between the heap and the stack: this is an implementation detail and may differ from one implementation to the next.

The flag argument affects various attributes of the mapped region.

- **MAP_FIXED**  The return value must equal `addr`. Use of this flag is discouraged, as it hinders portability. If this flag is not specified and if `addr` is nonzero, then the kernel uses `addr` as a hint of where to place the mapped region, but there is no guarantee that the requested address will be used. Maximum portability is obtained by specifying `addr` as 0.

> Support for the `MAP_FIXED` flag is optional on POSIX-conforming systems, but required on XSI-conforming systems.

- **MAP_SHARED**  This flag describes the disposition of store operations into the mapped region by this process. This flag specifies that store operations modify the mapped file—that is, a store operation is equivalent to a write to the file. Either this flag or the next (`MAP_PRIVATE`), but not both, must be specified.

- **MAP_PRIVATE**  This flag says that store operations into the mapped region cause a private copy of the mapped file to be created. All successive references to the mapped region then reference the copy. (One use of this flag is for a debugger that maps the text portion of a program file but allows the user to modify the instructions. Any modifications affect the copy, not the original program file.)

Each implementation has additional MAP_xxx flag values, which are specific to that implementation. Check the mmap(2) manual page on your system for details.

The value of off and the value of addr (if MAP_FIXED is specified) are usually required to be multiples of the system’s virtual memory page size. This value can be obtained from the sysconf function (Section 2.5.4) with an argument of _SC_PAGESIZE or _SC_PAGE_SIZE. Since off and addr are often specified as 0, this requirement is not a big deal.

This requirement is usually imposed by the system implementations. Although the Single UNIX Specification no longer requires that this condition be satisfied, all the platforms covered in this book, except FreeBSD 8.0, have this requirement. FreeBSD 8.0 allows us to use any address alignment and offset alignment as long as the alignments match.

Since the starting offset of the mapped file is tied to the system’s virtual memory page size, what happens if the length of the mapped region isn’t a multiple of the page size? Assume that the file size is 12 bytes and that the system’s page size is 512 bytes. In this case, the system normally provides a mapped region of 512 bytes, and the final 500 bytes of this region are set to 0. We can modify the final 500 bytes, but any changes we make to them are not reflected in the file. Thus we cannot append to a file with mmap. We must first grow the file, as we will see in Figure 14.27.

Two signals are normally used with mapped regions. SIGSEGV is normally used to indicate that we have tried to access memory that is not available to us. This signal can also be generated if we try to store into a mapped region that we specified to mmap as read-only. The SIGBUS signal can be generated if we access a portion of the mapped region that does not make sense at the time of the access. For example, assume that we map a file using the file’s size, but before we reference the mapped region, the file’s size is truncated by some other process. If we then try to access the memory-mapped region corresponding to the end portion of the file that was truncated, we’ll receive SIGBUS.

A memory-mapped region is inherited by a child across a fork (since it’s part of the parent’s address space), but for the same reason, is not inherited by the new program across an exec.

We can change the permissions on an existing mapping by calling mprotect.

```
#include <sys/mman.h>

int mprotect(void *addr, size_t len, int prot);
Returns: 0 if OK, -1 on error
```

The legal values for prot are the same as those for mmap (Figure 14.25). Be aware that implementations may require the address argument to be an integral multiple of the system’s page size.

When we modify pages that we’ve mapped into our address space using the MAP_SHARED flag, the changes aren’t written back to the file immediately. Instead, the kernel daemons decide when dirty pages are written back based on (a) system load and (b) configuration parameters meant to limit data loss in the event of a system failure. When the changes are written back, they are written in units of pages. Thus, if we modify only one byte in a page, when the change is written back to the file, the entire page will be written.

If the pages in a shared mapping have been modified, we can call msync to flush the changes to the file that backs the mapping. The msync function is similar to fsync (Section 3.13), but works on memory-mapped regions.

```
#include <sys/mman.h>
int msync(void *addr, size_t len, int flags);

Returns: 0 if OK, -1 on error
```

If the mapping is private, the file mapped is not modified. As with the other memory-mapped functions, the address must be aligned on a page boundary.

The flags argument allows us some control over how the memory is flushed. We can specify the MS_ASYNC flag to simply schedule the pages to be written. If we want to wait for the writes to complete before returning, we can use the MS_SYNC flag. Either MS_ASYNC or MS_SYNC must be specified.

An optional flag, MS_INVALIDATE, lets us tell the operating system to discard any pages that are out of sync with the underlying storage. Some implementations will discard all pages in the specified range when we use this flag, but this behavior is not required.

> The msync function is included in the XSI option in the Single UNIX Specification. As such, all UNIX systems must support it.

A memory-mapped region is automatically unmapped when the process terminates or we can unmap a region directly by calling the munmap function. Closing the file descriptor used when we mapped the region does not unmap the region.

```
#include <sys/mman.h>
int munmap(void *addr, size_t len);

Returns: 0 if OK, -1 on error
```

The munmap function does not affect the object that was mapped—that is, the call to munmap does not cause the contents of the mapped region to be written to the disk file. The updating of the disk file for a MAP_SHARED region happens automatically by the kernel's virtual memory algorithm sometime after we store into the memory-mapped region. Modifications to memory in a MAP_PRIVATE region are discarded when the region is unmapped.

# Example

The program in Figure 14.27 copies a file (similar to the cp(1) command) using memory-mapped I/O.

```
#include "apue.h"
#include <fcntl.h>
#include <sys/mman.h>

#define COPYINCR (1024*1024*1024)    /* 1 GB */
int
main(int argc, char *argv[])
{
    int         fdin, fdout;
    void        *src, *dst;
    size_t      copysz;
    struct stat sbuf;
    off_t       fsz = 0;
    if (argc != 3)
        err_quit("usage: %s <fromfile> <tofile>", argv[0]);
    if ((fdin = open(argv[1], O_RDONLY)) < 0)
        err_sys("can't open %s for reading", argv[1]);
    if ((fdout = open(argv[2], O_RDWR | O_CREAT | O_TRUNC,
        FILE_MODE)) < 0)
        err_sys("can't creat %s for writing", argv[2]);
    if (fstat(fdin, &sbuf) < 0)            /* need size of input file */
        err_sys("fstat error");
    if (ftruncate(fdout, sbuf.st_size) < 0) /* set output file size */
        err_sys("ftruncate error");
    while (fsz < sbuf.st_size) {
        if ((sbuf.st_size - fsz) > COPYINCR)
            copysz = COPYINCR;
        else
            copysz = sbuf.st_size - fsz;
        if ((src = mmap(0, copysz, PROT_READ, MAP_SHARED,
            fdin, fsz)) == MAP_FAILED)
            err_sys("mmap error for input");
        if ((dst = mmap(0, copysz, PROT_READ | PROT_WRITE,
            MAP_SHARED, fdout, fsz)) == MAP_FAILED)
            err_sys("mmap error for output");
        memcpy(dst, src, copysz);    /* does the file copy */
        munmap(src, copysz);
        munmap(dst, copysz);
        fsz += copysz;
    }
    exit(0);
}
```
