© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

maxsize wide characters of s shall accessed by wcsnlen_s.

# K.3.9.3 Extended multibyte/wide character conversion utilities

# K.3.9.3.1 Restartable multibyte/wide character conversion functions

+   Unlike wctomb, wctomb_s does not permit the ps parameter (the pointer to the
conversion state) to be a null pointer.

# K.3.9.3.1.1 The wctomb_s function

Synopsis

```
#include <wchar.h>
erno_t wctomb_s(size_t * restrict retrieval,
char * restrict s, size_t smax,
wchar_t wc, mbstate_t * restrict ps);
```

Runtime-constraints

+   Neither nor ps shall be a null pointer. If s is not a null pointer, smax
shall not equal zero and not be greater than RSIZE_MAX. If s is not a null pointer,
then smax shall not be greater than the number of bytes to be stored in the array pointed
b s. If s is a null pointer, smax shall equal zero.

+   If there is a runtime-constraint violation, wctomb_s does the following. If s is
not a null pointer and smax is greater than and not greater than RSIZE_MAX, then
wctomb_s sets s[0] to the null character. If retval is not a null pointer, then
wctomb_s sets *retrieval to (size_t) (-1).

Description

+   If s is a null pointer, wctomb_s function is equivalent to the call
wctomb_s(&retval, buf, sizeof buf, L'\0', ps)
where retval and buf are variables of the appropriate types, and the size of
buf is greater than MB_CUR_MAX.

+   If s is not a null pointer, the wctomb_s function determines the number of bytes
needed to represent the multibyte character that corresponds to the wide character
wc (any shift sequences), and stores the multibyte character representation
in the array where first element is pointed to by s. At wc is a wide character, a byte is stored, preceded by any
shift sequence to restore the initial shift state; the resulting state describing the initial
conversion state.

452) Note that the wcsnlen_s has no runtime-constraints. This lack of runtime-constraints
along with the values returned for a null pointer or uncertain wide string argument make
wcsnlen_s useful in algorithms that gracefully handle exceptional data.

# §K.3.9.3.1.1

Bounds-checking interfaces

647