# 7.21.10.2 The feof function

Synopsis

```
#include <stdio.h>
int feof(FILE *stream);
```

Description

The feof function tests the end-of-file indicator for the stream pointed to by stream.

Returns

The feof function returns nonzero if and only if the end-of-file indicator is set for stream.

# 7.21.10.3 The ferror function

Synopsis

```
#include <stdio.h>
int ferror(FILE *stream);
```

Description

The ferror function tests the error indicator for the stream pointed to by stream.

Returns

The ferror function returns nonzero if and only if the error indicator is set for stream.

# 7.21.10.4 The perror function

Synopsis

```
#include <stdio.h>
void perror(const char *s);
```

Description

The perror maps the error number in the integer expression errno to an error message. It writes a sequence of characters to the standard error stream: first (if s is not a null pointer and the character pointed to by s is not the null character), the string pointed by s followed by a colon:) and a space; then an appropriate error message string followed by a new-line character. The contents of the error message strings are those returned by the strerror function with argument errno.

Returns

The perror function returns no value.

Forward references: the strerror function (7.24.6.2).