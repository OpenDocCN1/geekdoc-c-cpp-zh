# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# Runtime-constraints

+   12 None of retrieval, *src, or ps* shall be null pointers. If *dst* is not a null pointer, then neither *len* nor *dstmax* shall be greater than *RSIZE_MAX*. If *dst* is a null pointer, then *dstmax* shall equal zero. If *dst* is not a null pointer and *len* is not less than *dstmax*, then the conversion shall have stopped (see below) because a terminating null character was reached or because an encoding error occurred.

+   13 If there is a runtime-constraint violation, then *wcsrtomp_s* does the following. If *retval* is not a null pointer, then *wcsrtomp_s* sets *retval* to *(size_t) (-1). If *dst* is not a null pointer and *dstmax* is greater than zero and less than *RSIZE_MAX*, *wcsrtomp_s* sets *dst* [0] to the null character.

# Description

+   14 *wcsrtomp_s* function converts a sequence of wide characters from the array indirectly pointed to by *src* to a sequence of multibyte characters that begins in the state described by the object pointed to by *ps*. If *dst* is not a null pointer, the converted characters are stored into the array pointed to by *dst*. Conversion continues up and including a terminating null character, which is also stored. Conversion stops earlier in two cases:

+   * when a character is reached that does not correspond to a multibyte character;

+   * (*dst* is not a null pointer) when the next multibyte character would exceed the limit of *n* bytes to be stored into the array pointed to by *dst*. If the wide character being converted is the null character, then *n* is the lesser of *len* or *dstmax*. Otherwise, *n* is the lesser of *len* or *dstmax*.

If the conversion stops without converting a null character and *dst* is not a null pointer, then a character is stored into the array pointed to by *dst* immediately following any multibyte characters already stored. Each conversion takes place as if by a call to *wcsrtomb* function.⁴⁵⁵

+   15 If *dst* is not a null pointer, the object pointed to by *src* is assigned a null pointer (if conversion stopped due to reaching a terminating null character) or the address just past the last wide character converted (if any). If conversion stopped to reaching a terminating null character, the resulting state is the initial conversion state.

> ⁵If conversion stops because a terminating null character has been reached, the bytes stored include those necessary to reach the initial shift state immediately before the null byte. However, if the conversion stops before a terminating null character has been reached, the result will be null terminated, but not end in the initial shift state.

650

Bounds-checking interfaces

§K.3.9.3.2.2