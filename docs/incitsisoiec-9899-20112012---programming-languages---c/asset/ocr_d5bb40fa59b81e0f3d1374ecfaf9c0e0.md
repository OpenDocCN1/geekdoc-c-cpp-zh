# Runtime-commands

None of retval, src, *src, or ps are null pointers. If dst is not a null pointer, then neither len nor dmax shall be greater than RSIZE_MAX. If dst is a null pointer, then dmax shall equal zero. If dst is not a null pointer and len is not less than dmax, the conversion will have been stopped (see below) because a terminating null character was reached or because of an encoding error occurred.

+   13  If there is a runtime-constraint violation, the wcsrtombs_s does the following. If retval is not a null pointer, then wcsrtombs_s sets *retval to (size_t)(-1). If dst is not a null pointer and dmax is greater than zero and less than RSIZE_MAX, then wcsrtombs_s sets dst [0] to the null character.

# Description

+   14  The wcsrtombs_s function converts a sequence of wide characters from the array indirectly pointed to by src into a sequence of corresponding multibyte characters that begins in the conversion state described by the object pointed to by ps. If dst is not a null pointer, the converted characters are then stored into the array pointed to by dst. Conversion continues up to and including a terminating null character, which is also stored. Conversion stops earlier in two cases:

+   - when a character is reached that does not correspond to a valid multibyte character;
- (if dst is not a null pointer) when the next multibyte character would exceed the limit of n bytes to be stored in the array pointed to by dst. If the character being converted is the null wide character, then n is the lesser of len or dmax. Otherwise, n is the lesser of len or dmax-1.
If the conversion stops without converting a null character and dst is not a null pointer, then a null character is stored into the array pointed to by dst immediately following any multibyte characters already stored. Each conversion takes place as if a call to the wcsrtomb function.455

+   15  If dst is not a null pointer, the object pointed to by src is assigned either a null pointer (if conversion stopped due to reaching a terminating null character) or the address just past the last wide character converted (if any). If conversion stopped due to reaching a terminating wide character, the resulting state described is the initial conversion state.

> 455 If conversion stops because a terminating null character has been reached, the bytes stored include those necessary to reach the initial shift state before the null byte. However, if the conversion stops before a terminating null wide character has been reached, the result will be null terminated, but might not end in the initial shift state.