any other operation on the stream, we can change the buffering if we want to, with the setbuf or setvbuf functions from the previous section.

An open stream is closed by calling fclose.

```
#include <stdio.h>
int fclose(FILE *fp);

Returns: 0 if OK, EOF on error
```

Any buffered output data is flushed before the file is closed. Any input data that may be buffered is discarded. If the standard I/O library had automatically allocated a buffer for the stream, that buffer is released.

When a process terminates normally, either by calling the exit function directly or by returning from the main function, all standard I/O streams with unwritten buffered data are flushed and all open standard I/O streams are closed.

# 5.6 Reading and Writing a Stream

Once we open a stream, we can choose from among three types of unformatted I/O:

+   1. Character-at-a-time I/O. We can read or write one character at a time, with the standard I/O functions handling all the buffering, if the stream is buffered.
+   2. Line-at-a-time I/O. If we want to read or write a line at a time, we use fgets and fputs. Each line is terminated with a newline character, and we have to specify the maximum line length that we can handle when we call fgets. We describe these two functions in Section 5.7.
+   3. Direct I/O. This type of I/O is supported by the fread and fwrite functions. For each I/O operation, we read or write some number of objects, where each object is of a specified size. These two functions are often used for binary files where we read or write a structure with each operation. We describe these two functions in Section 5.9.

> The term direct I/O, from the ISO C standard, is known by many names: binary I/O, object-at-a-time I/O, record-oriented I/O, or structure-oriented I/O. Don't confuse this feature with the O_DIRECT open flag supported by FreeBSD and Linux—they are unrelated.

(We describe the formatted I/O functions, such as printf and scanf, in Section 5.11.)

# Input Functions

Three functions allow us to read one character at a time.

```
#include <stdio.h>
int getc(FILE *fp);
int fgetc(FILE *fp);
int getchar(void);

All three return: next character if OK, EOF on end of file or error
```