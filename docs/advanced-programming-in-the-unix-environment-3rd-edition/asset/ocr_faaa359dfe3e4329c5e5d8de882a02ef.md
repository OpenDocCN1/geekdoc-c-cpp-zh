# Standard I/O

The standard I/O functions provide a buffered interface to the unbuffered I/O functions. Using standard I/O relieves us from having to choose optimal buffer sizes, such as the BUFFSIZE constant in Figure 1.4. The standard I/O functions also simplify dealing with lines of input (a common occurrence in UNIX applications). The fgets function, for example, reads an entire line. The read function, in contrast, reads a specified number of bytes. As we shall see in Section 5.4, the standard I/O library provides functions that let us control the style of buffering used by the library.

The most common standard I/O function is printf. In programs that call printf, we’ll always include <stdio.h>—normally by including apue.h—as this header contains the function prototypes for all the standard I/O functions.

# Example

The program in Figure 1.5, which we’ll examine in more detail in Section 5.8, is like the previous program that called read and write. This program copies standard input to standard output and can copy any regular file.

```
#include "apue.h"
int
main(void)
{
    int     c;
    while ((c = getc(stdin)) != EOF)
        if (putc(c, stdout) == EOF)
            err_sys("output error");
    if (ferror(stdin))
        err_sys("input error");
    exit(0);
}
```

Figure 1.5 Copy standard input to standard output, using standard I/O

The function getc reads one character at a time, and this character is written by putc. After the last byte of input has been read, getc returns the constant EOF (defined in <stdio.h>). The standard I/O constants stdin and stdout are also defined in the <stdio.h> header and refer to the standard input and standard output.

# 1.6 Programs and Processes

# Program

A program is an executable file residing on disk in a directory. A program is read into memory and is executed by the kernel as a result of one of the seven exec functions. We’ll cover these functions in Section 8.10.