The fwrite function returns the number of elements successfully written, which will be less than nmemb only if a write error is encountered. If size or nmemb is zero, fwrite returns zero and the state of the stream remains unchanged.

# 7.21.9 File positioning functions

# 7.21.9.1 The fgetpos function

Synopsis

```
#include <stdio.h>
int fgetpos(FILE * restrict stream,
pos_t * restrict pos);
```

Description

The fgetpos function stores the current values of the parse state (if any) and file position indicator for the stream pointed to by stream in the object pointed to by pos. The values stored contain unspecified information usable by the fgetpos function for repositioning the stream to its position at the time of the call to the fgetpos function.

Returns

If successful, the fgetpos function returns zero; on failure, the fgetpos function returns nonzero and stores an implementation-defined positive value in errno.

Forward references: the fsetpos function (7.21.9.3).

# 7.21.9.2 The fseek function

Synopsis

```
#include <stdio.h>
int fseek(FILE *stream, long int offset, int whence);
```

Description

The fseek function sets the file position indicator for the stream pointed to by stream. If a read or write error occurs, the error indicator for the stream is set and fseek fails.

For a binary string, the new position, measured in characters from the beginning of the file, is obtained by adding offset to the position specified by whence. The specified position is the beginning of the file if whence is SEEK_SET, the current value of the file position indicator if SEEK_CUR, or end-of-file if SEEK_END. A binary stream need not meaningfully supporting fseek calls with a value of whence SEEK_END.

For a text stream, either offset shall be zero, or offset shall be a value returned by an earlier successful call to the ftell function on a stream associated with the same file and whence shall be SEEK_SET.