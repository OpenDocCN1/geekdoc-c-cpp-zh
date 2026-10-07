# 7.22.7 Multibyte/wide character conversion functions

The behavior of the multibyte character functions is affected by the LC_TYPE category of the current locale. For a state-dependent encoding, each function is placed into its initial state at program startup and can be returned to that state by a call for which its character pointer argument, s, is a null pointer. Subsequent calls with s other than a null pointer cause the internal conversion state of the function to be altered as necessary. A call with s as a null pointer causes functions to return a nonzero value if encodings have state dependency, and zero otherwise.³305 Changing the LC_TYPE category causes the conversion state of these functions to be indeterminate.

# 7.22.7.1 mblen function

Synopsis

```
#include <stdlib.h>
int mblen(const char *s, size_t n);
```

Description

If s is not a null pointer, the mblen function determines the number of bytes contained in the multibyte character pointed to s. Except that the conversion state of the mbtowc function is not affected, it is equivalent to

mbtowc((char_t *)0, (const char *)0, 0);
mbtowc((char_t *)0, 0, n);

The implementation shall behave as if no library function calls the mblen function.

Returns

If s is a null pointer, the mblen function returns a nonzero or zero value, if multibyte character encodings, respectively, do or not have state-dependent encodings. If s is not a null pointer, the mblen function returns 0 (if s points to the null character), or returns the number of bytes that are contained in the multibyte character (if the n or fewer bytes form a valid multibyte character), or returns -1 (if they do not form a multibyte character).

Forward references: the mbtowc function (7.22.7.2).