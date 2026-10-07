ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.22.8.2 The wcstombs function

# Synopsis

+   1. #include <stdlib.h>
size_t wcstombs(char *restrict s,
const wchar_t * restrict pwcs,
size_t n);

# Description

+   2. The wcstombs function converts a sequence of wide characters from the array pointed to by pwcs into a sequence of corresponding multibyte characters that begins in the initial shift state, and stores these multibyte characters into the array pointed to by s, stopping if a multibyte character would exceed the limit of n total bytes or if a null character is stored. Each wide character is converted as if a call to the wcctombs function, except that the conversion state of the wcctombs function is not affected.

+   3. No more than n bytes will be modified in the array pointed to by s. If copying takes place between objects that overlap, the behavior is undefined.

# Returns

+   4. If a wide character is encountered that does not correspond to a valid multibyte character, the wcstombs function returns (size_t) (-1). Otherwise, the wcstombs function returns the number of bytes modified, not including a terminating null character, if any.306