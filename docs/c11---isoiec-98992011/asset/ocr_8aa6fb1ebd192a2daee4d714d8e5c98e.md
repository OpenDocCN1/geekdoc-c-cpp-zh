# ISO/IEC 9899:2011 (E)

# K.3.6.4 Multibyte/wide character functions

The behavior of the multibyte character functions is affected by the LC_CTYPE category of the current locale. For a state-dependent encoding, each function is placed into its initial state by a call for which its character pointer argument, s is a null pointer. Subsequent calls with s as other than a null pointer change the internal conversion state of the function to be altered as necessary. A call with s as a null pointer causes these functions to be set the int pointed to by their status argument to a nonzero value if encodings have state dependency, and zero otherwise⁴13) Changing the LC_CTYPE category causes the state of these functions to be indeterminate.

# K.3.6.4.1 The wctomb_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdlib.h>

error_t wctomb_s(int * restrict status,
                 char * restrict s,
                 size_t smax,
                 wchar_t wc);
```

# Runtime-constraints

Let n define the number of bytes needed to represent the multibyte character corresponding to the wide character by wc (including any shift sequences).

If s is not a null pointer, then smax shall not be less than n, and smax shall not be greater than RSIZE_MAX. If s is a null pointer, then smax shall be equal zero.

If there is a runtime-constraint violation, wctomb_s does not modify the int pointed to by status, and if s is not a null pointer, no more than smax elements in the array pointed to by s will be accessed.

# Description

The wctomb_s function returns n and stores the multibyte character representation of wc in the array whose first element is pointed to by s (if s is not a null pointer). The number of characters stored never exceeds MB_CUR_MAX or smax. If wc is a null character, a null byte is stored, preceded by any shift sequence to restore the initial shift state, and the function is left in the initial conversion state.

The implementation shall behave as if no library function calls the wctomb_s function.

> ⁴13) If the locale employs special bytes to change the shift state, these bytes do not produce separate character codes, but are grouped with any multibyte character.