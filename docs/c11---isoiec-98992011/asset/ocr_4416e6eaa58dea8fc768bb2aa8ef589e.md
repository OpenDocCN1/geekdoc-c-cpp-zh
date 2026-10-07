# 7.29.2.11 The wprintf function

Synopsis

```
#include <wchar.h>
int wprintf(const wchar_t * restrict format, ...);
```

Description

The wprintf function is equivalent to fwprintf with the argument stdout interposed before the arguments to wprintf.

Returns

The wprintf function returns the number of wide characters transmitted, or a negative value if an input or encoding error occurred.

# 7.29.2.12 The wscanf function

Synopsis

```
#include <wchar.h>
intscanf(const wchar_t * restrict format, ...);
```

Description

The wscanf function is equivalent to fwscanf with the argument stdin interposed before the arguments to wscanf.

Returns

The wscanf function returns the value of the macro EOF if an input failure occurs before the first conversion (if any) has completed. Otherwise, the wscanf function returns the number of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

# 7.29.3 Wide character input/output functions

# 7.29.3.1 The fgetwc function

Synopsis

```
#include <stdio.h>
#include <wchar.h>
int_t fgetwc(FILE *stream);
```

Description

If the end-of-indicator for the input stream pointed by stream is not set and a next character is present, the fgetwc function obtains that character as a wchar_t converted to a wint_t and advances the associated file position indicator for the stream (defined).