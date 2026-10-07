# ISO/IEC 9899:2011 (E)

bytes is encountered that does not form a valid multibyte character, or (if dst is not a null pointer) when len wide characters have been stored in the array pointed to by dst.414) If dst is not a null pointer and no wide character was stored into the array pointed to by dst, then dst[len] is set to the wide character. Each conversion takes place as by a call to the mbtowc function

+   5 Regardless of whether dst is or not a null pointer, if the input conversion encounters a sequence of bytes that do not form a valid multibyte character, an encoding error occurs: the mbtowcs_s function stores the value (size_t)(-1) into *retval. Otherwise, the mbtowcs_s function stores into *retval the number of multibyte characters successfully converted, not including the terminating character (if any).

+   6 All elements the terminating wide character (if any) written by mbtowcs_s in the array dstmax wide characters pointed to by dst unspecified values when mbtowcs_s returns.415)

+   7 If copying takes place between objects that overlap, the objects take on unspecified values.

Returns

The mbtowcs_s function returns zero if no runtime-constraint violation and no encoding error occurred. Otherwise, a nonzero value is returned.

# K.3.6.5.2 The wctombs_s function

Synopsis

```
#include <stdlib.h>
errno_t wctombs_s(size_t * restrict retval,
char * restrict dst, rsize_t dstmax,
const wchar_t * restrict src, rsize_t len);
```

Runtime-constraints

+   2 Neither retval nor src shall be a null pointer. If dst is not a null pointer, neither len dstmax shall be greater than RSIZE_MAX. If dst is a null pointer, then dstmax shall not equal zero. If dst is not a null pointer, then dstmax is not less than dstmax, and the conversion shall have been shown (see below) because a terminating wide character was reached or because an encoding error occurred.

> 414) Thus, the value of len is ignored if dst is a null pointer.

> 415) This allows an implementation to convert the multibyte string before discovering a terminating null did not occur where required.

612

Bounds-checking interfaces

§K.3.6.5.2