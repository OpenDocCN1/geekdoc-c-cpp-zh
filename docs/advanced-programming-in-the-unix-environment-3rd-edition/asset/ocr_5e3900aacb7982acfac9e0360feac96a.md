buffer. The buffer is terminated with a null byte. If the line, including the terminating newline, is longer than n − 1, only a partial line is returned, but the buffer is always null terminated.

Another call to fgets will read what follows on the line.

The gets function should never be used. The problem is that it doesn’t allow the caller to specify the buffer size. This allows the buffer to overflow if the line is longer than the buffer, writing over whatever happens to follow the buffer in memory. For a description of how this flaw was used as part of the Internet worm of 1988, see the June 1989 issue (vol. 32, no. 6) of Communications of the ACM. An additional difference with gets is that it doesn’t store the newline in the buffer, as fgets does.

> This difference in newline handling between the two functions goes way back in the evolution of the UNIX System. Even the Version 7 manual (1979) states “gets deletes a newline, fgets keeps it, all in the name of backward compatibility.”

Even though ISO C requires an implementation to provide gets, you should use fgets instead. In fact, gets is marked as an obsolescent interface in SUSv4 and has been omitted from the latest version of the ISO C standard (ISO/IEC 9899:2011).

Line-at-a-time output is provided by fputs and puts.

```
#include <stdio.h>

int fputs(const char *restrict str, FILE *restrict fp);
int puts(const char *str);

Both return: non-negative value if OK, EOF on error
```

The function fputs writes the null-terminated string to the specified stream. The null byte at the end is not written. Note that this need not be line-at-a-time output, since the string need not contain a newline as the last non-null character. Usually, this is the case—the last non-null character is a newline—but it’s not required.

The puts function writes the null-terminated string to the standard output, without writing the null byte. But puts then writes a newline character to the standard output.

The puts function is not unsafe, like its counterpart gets. Nevertheless, we’ll avoid using it, to prevent having to remember whether it appends a newline. If we always use fgets and fputs, we know that we always have to deal with the newline character at the end of each line.

# 5.8 Standard I/O Efficiency

Using the functions from the previous section, we can get an idea of the efficiency of the standard I/O system. The program in Figure 5.4 is like the one in Figure 3.5: it simply copies standard input to standard output, using getc and putc. These two routines can be implemented as macros.