return values is not necessarily meaningful measure of the number of characters written or read.

# Returns

If successful, the ftell function returns the current value of the file position indicator for the stream. On failure, the ftell function returns -1 and stores an implementation-defined positive value in errno.

# 7.21.9.5 The rewind function

# Synopsis

```
#include <stdio.h>
void rewind(FILE *stream);
```

# Description

The rewind function sets the file position indicator for the stream pointed to by the beginning of the file. It is equivalent to

```
(void) fseek(stream, 0, SEEK_SET)
```

except that the error indicator for the stream is also cleared.

# Returns

The rewind function returns no value.

# 7.21.10 Error-handling functions

# 7.21.10.1 The clearerr function

# Synopsis

```
#include <stdio.h>
void clearerr(FILE *stream);
```

# Description

The clearerr function clears the end-of-file and error indicators for the stream pointed to by stream.

# Returns

The clearerr function returns no value.