# 22.7.8.2 The wcstombs function

# Synopsis

```
#include <stdlib.h>
size_t wcstombs(char * restrict s,
const wchar_t * restrict pwcs,
size_t n);
```

# Description

The wcstombs function converts a sequence of wide characters from the array pointed to by pwcs into a sequence of corresponding multibyte characters that begins in the initial shift state, and stores these multibyte characters into the array pointed to by s, stopping if a multibyte character would exceed the limit of n total bytes or if a null character is stored. Each wide character is converted as if by a call to the wctomb function, except that the conversion state of the wctomb function is not affected.

No more than n bytes will be modified in the array pointed to by s. If copying takes place between objects that overlap, the behavior is undefined.

# Returns

If a wide character is encountered that does not correspond to a valid multibyte character, the wcstombs function returns (size_t) (-1). Otherwise, the wcstombs function returns the number of bytes modified, not including a terminating null character, if any.