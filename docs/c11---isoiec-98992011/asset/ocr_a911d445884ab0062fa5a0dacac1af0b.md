© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

support positioning requests, or if the stream was opened with append mode, the character is appended to the output stream.

# Returns

+   3 The fputwc function returns the wide character written. If a write error occurs, the error indicator for the stream is set and fputwc returns WEOF. If an encoding error occurs, the value of the macro EISEQ is stored in errno and fputwc returns WEOF.

# 7.29.3.4 The fputwc function

# Synopsis

```
1 #include <stdio.h>
#include <wchar.h>
int fputwc(const wchar_t * restrict s,
FILE * restrict stream);
```

# Description

+   2 The fputwc function writes the wide string pointed to by s to the stream pointed to. The terminating null wide character is not written.

# Returns

+   3 The fputwc function returns EOF if a write error or encoding error occurs; otherwise, it returns a nonnegative value.

# 7.29.3.5 The fwide function

# Synopsis

```
1 #include <stdio.h>
#include <wchar.h>
int fwide(FILE *stream, int mode);
```

# Description

+   2 The fwide function determines the orientation of the stream pointed to by stream. If mode is greater than zero, the function first attempts to make the stream wide oriented. mode is less than zero, the function first attempts to make the stream wide oriented.^{342} Otherwise, mode is zero and the function does not alter the orientation of the stream.

# Returns

+   3 The fwide function returns a value greater than zero if, after the call, the stream has wide orientation, a less value less than zero, or zero if the stream has no orientation.

> 342) If the orientation of the stream has already been determined, fwide does not change it.

# 7.29.3.5 Library 423