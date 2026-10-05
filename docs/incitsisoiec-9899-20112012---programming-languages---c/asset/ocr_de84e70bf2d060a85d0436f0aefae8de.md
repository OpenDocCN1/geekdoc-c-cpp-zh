The implementation shall behave as if no library function calls the wctomb function.

If s is a null pointer, the wctomb function returns a nonzero or zero value, if multibyte encodings, or do not have state-dependent effects. If s is not a null pointer, the wctomb function returns -1 if wc does not correspond to a multibyte character, or returns the number of bytes that are contained in the multibyte character corresponding to the value of wc.

In no case will the value be greater than the value of the MB_CUR_MAX macro.

# 72.2.8 Multibyte/wide string conversion functions

The behavior of the multibyte string functions is affected by the LC_CTYPE category of the current locale.

# 72.2.8.1 The mbstowcs function

# Synopsis

```
#include <stdlib.h>
size_t mbstowcs(wchar_t * restrict pwcs,
               const char * restrict s,
               size_t n);
```

# Description

The mbstowcs function converts a sequence of multibyte characters that begins in the initial state from the array pointed to by s into a sequence of corresponding wide characters and stores more than n wide characters into the array pointed to by pwcs. No multibyte characters follow a null character (which is converted into a null wide character) will be examined or converted. Each multibyte character is converted as if a call to the mbtowc function, except the conversion state of the mbtowc function is not affected.

No more than n elements are modified in the array pointed to by pwcs. If copying takes between objects that overlap, the behavior is undefined.

# Returns

If an invalid multibyte character is encountered, the mbstowcs function returns (size_t) (-1). Otherwise, the mbstowcs function returns the number of array elements modified, not including a terminating null wide character, if any.306

306) The array will not be null-terminated if the value returned is n.