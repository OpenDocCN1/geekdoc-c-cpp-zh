# ISO/IEC 9899:2011 (E)

If wc does not correspond to a valid multibyte character, an encoding error occurs: the wctomb_s function stores the value (size_t) (-1) into *retval and the conversion state is unspecified. Otherwise the wctomb_s function stores into *retval the number of bytes (including any shift sequences) stored in the array pointed to by s.

# Returns

The wctomb_s function returns zero if no runtime-constraint violation and no encoding error occurs. Otherwise, a nonzero value is returned.

# K.3.9.3.2 Restartable multibyte/wide string functions

+   Unlike mbsrtowcs and wctombs, mbsrtowcs_s and wctombs_s do not permit the ps parameter (the pointer to the conversion state) to be a null pointer.

# K.3.9.3.2.1 mbsrtowcs_s function

# Synopsis

```
#include <wchar.h>
nerno_t mbsrtowcs_s(size_t * restrict retval,
char_t * restrict dst, size_t dstmax,
const char ** restrict src, size_t len,
mbstate_t * restrict ps);
```

# Runtime-constraints

None of retval, *src, *oc shall be null pointers. If dst is not a null pointer, then neither nor dstmax shall be greater than RSIZE_MAX. If dst is a null pointer, then dstmax shall equal zero. If dst is not a null pointer, then dstmax shall not be less than equal, then no character shall occur after the first multibyte characters of the array pointed to by *src.

If there is a runtime-constraint violation, then mbsrtowcs_s sets *retval to (size_t) (-1). If dst is not a null pointer and dstmax is greater than zero and less than RSIZE_MAX, then mbsrtowcs_s sets dst [0] to the wide character.

# Description

The mbsrtowcs_s function converts a sequence of multibyte characters that begins in the conversion state described by the object pointed to by ps, from the array indexed by src. If dst is not a null pointer, the converted characters are stored into the array pointed to by dst. Conversion continues to and until reaching a terminating null character, which is also stored. Conversion stops earlier in cases: when a sequence of bytes is encountered not a valid multibyte character, or if dst is not a null pointer) when len

648

# Bounds-checking interfaces

# §K.3.9.3.2.1