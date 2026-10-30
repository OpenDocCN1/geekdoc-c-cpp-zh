The open_memstream function creates a stream that is byte oriented, and the open_wmemstream function creates a stream that is wide oriented (recall the discussion of multibyte characters in Section 5.2). These two functions differ from fmemopen in several ways:

+   - The stream created is only open for writing.
+   - We can't specify our own buffer, but we can get access to the buffer's address and size through the bufp and sizep arguments, respectively.
+   - We need to free the buffer ourselves after closing the stream.
+   - The buffer will grow as we add bytes to the stream.

We must follow some rules, however, regarding the use of the buffer address and its length. First, the buffer address and length are only valid after a call to fclose or fflush. Second, these values are only valid until the next write to the stream or a call to fclose. Because the buffer can grow, it may need to be reallocated. If this happens, then we will find that the value of the buffer's memory address will change the next time we call fclose or fflush.

Memory streams are well suited for creating strings, because they prevent buffer overflows. They can also provide a performance boost for functions that take standard I/O stream arguments used for temporary files, because memory streams access only main memory instead of a file stored on disk.

# 5.15 Alternatives to Standard I/O

The standard I/O library is not perfect. Korn and Vo [1991] list numerous defects—some in the basic design, but most in the various implementations.

One inefficiency inherent in the standard I/O library is the amount of data copying that takes place. When we use the line-at-a-time functions, fgets and fputs, the data is usually copied twice: once between the kernel and the standard I/O buffer (when the corresponding read or write is issued) and again between the standard I/O buffer and our line buffer. The Fast I/O library [fio(3) in AT&T 1990a] gets around this by having the function that reads a line return a pointer to the line instead of copying the line into another buffer. Hume [1988] reports a threefold increase in the speed of a version of the grep(1) utility simply by making this change.

Korn and Vo [1991] describe another replacement for the standard I/O library: sfio. This package is similar in speed to the fio library and normally faster than the standard I/O library. The sfio package also provides some new features that aren't found in most other packages: I/O streams generalized to represent both files and regions of memory, processing modules that can be written and stacked on an I/O stream to change the operation of a stream, and better exception handling.

Krieger, Stumm, and Unrau [1992] describe another alternative that uses mapped files—the mmap function that we describe in Section 14.8. This new package is called ASI, the Alloc Stream Interface. The programming interface resembles the UNIX System memory allocation functions (malloc, realloc, and free, described in