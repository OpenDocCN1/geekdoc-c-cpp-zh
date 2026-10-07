© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

characters have been stored into the array pointed to by dst.{453} If dst is not a null pointer and no wide character was stored into the array pointed to by dst, dst[len] is to set the wide character. Each conversion takes place as if by a call to mbrtowc function.

+   If dst is not a null pointer, the pointer object pointed to by src is assigned a null pointer (if conversion stopped due to reaching a null character) or the address just past the last multibyte character converted (if any). If conversion stopped due to reaching a terminating null character and if dst is not a null pointer, the resulting state describes the initial state.

+   Regardless of whether dst is not a null pointer, the input conversion encounters a sequence of bytes that do not form a valid multibyte character, (size_t) {-1} *retval and the conversion is unspecified. Otherwise, the mbrtowcs_s function stores into the mbrtowcs_s function stores into the *retval the number of multibyte characters successfully converted, not including the terminating null character (if any).

+   All elements forming the terminating wide character (if any) written by mbrtowcs_s in the array ofmax wide characters pointed to by dst unspecified values using mbrtowcs_s returns.{454}

+   If copying takes place between objects that overlap, the objects take on unspecified values.

# Returns

The mbrtowcs_s function returns zero no runtime-constraint violation and no encoding error occurred. Otherwise, a nonzero value is returned.

# K.3.9.3.2.2 Wcsrtombs_s function

# Synopsis

```
#include <wchar.h>
erno_t wcsrtombs_s(size_t * restrict retval,
char * restrict dst, rsize_t dstmax,
const char ** restrict src, rsize_t len,
state_t * restrict ps);
```

453) Thus, the value of len is ignored if dst is a null pointer.

454) This allows implementation to attempt converting the multibyte string before discovering the terminating null character where not occur required.

# §K.3.9.3.2.2 Bounds-checking interfaces

649