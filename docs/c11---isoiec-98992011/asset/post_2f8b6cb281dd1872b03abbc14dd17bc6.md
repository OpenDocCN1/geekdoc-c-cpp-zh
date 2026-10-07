
# ISO/IEC 9899:2011 (E)

width, or precision) shall not appear in the wide string pointed to by format. Any argument to wprintf_s corresponding to a % specifier shall not be a null pointer.

If there is a runtime-constraint violation, the wprintf_s function does not attempt to produce further output, and it is unspecified to what extent wprintf_s produced output before discovering the runtime-constraint violation.

# Description

The wprintf_s function is equivalent to the printf function except for the explicit runtime-constraints listed above.

# Returns

The wprintf_s function returns the number of wide characters transmitted, or a negative value if an output error, encoding error, or runtime-constraint violation occurred.

# K.3.9.1.14

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int scanf_f(const wchar_t * restrict format, ...);
```

# Runtime-constraints

format shall not be a null pointer. Any argument indirect though in order to store converted input shall not be a null pointer.

If there is a runtime-constraint violation, the wscanf_s function does not attempt to perform further input, and it is unspecified to what extent wscanf_s performed input before discovering the runtime-constraint violation.

# Description

The wscanf_s function is equivalent to fwscanf_s with the argument stdin interspersed before the arguments to wscanf_s.

# Returns

The wscanf_s function returns the value of macro EOF if an input failure occurs before any conversion or if it is a runtime-constraint violation. Otherwise, the wscanf_s function returns the number of input items assigned, which can be fewer provided for, or even zero, in the event of an early matching failure.

# K.3.9.2 General string utilities

# K.3.9.2.1 Wide string copying functions

# K.3.9.2.1.1 The wcscpy_s function

# Synopsis

```
#define _STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
errno_t wcscpy_s(wchar_t * restrict s1,
rsize_t slmax,
const wchar_t * restrict s2);
```

# Runtime-constraints

- Neither sl1 nor s2 is a null pointer. slmax shall not be greater than RSIZE_MAX. slmax shall not equal zero. slmax shall be greater than wcslen_s (s2, slmax). Copying shall not take place between objects that overlap.
- If there is a runtime-constraint violation, if s1 is not a null pointer and slmax is greater than zero and not greater than RSIZE_MAX, then wcscpy_s sets s1[0] to the null character.

# Description

- The wcscpy_s function copies the wide string pointed to by s2 (including the terminating null character) into the array pointed to by s1.
- All elements following the null wide character (if any) written by wcscpy_s in the array of slmax wide characters pointed to by s1 take unspecified values when wcscpy_s returns.

# Returns

- The wcscpy_s function returns zero if there is no runtime-constraint violation. Otherwise, a nonzero value is returned.

> 442) This allows an implementation to copy wide characters if any of the wide characters are null. Such an approach might write a wide character to every element of s1 before discovering that the first element should be set to the null wide character.

> 443) A zero return value implies that all of the requested characters from the string pointed to by s2 fit within the array pointed to s1 and the result in s1 is null terminated.

# §K.3.9.2.1.1 Bounds-checking interfaces

# K.3.9.2.1.2 The wscncpy_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>

errno_t wscncpy_s(wchar_t * restrict s1,
rsize_t slmax,
const wchar_t * restrict s2,
rsize_t n);
```

# Runtime-constraints

- Neither s1 nor s2 be a null pointer. Neither slmax nor n shall be greater than RSIZE_MAX. slmax shall not be equal. If n is not less than slmax, then slmax shall be greater than wscnclen_s(s2, slmax). Copying shall not take place between objects that overlap.
- If there is a runtime-constraint violation, if s1 is not a null pointer and slmax is greater than zero and not greater than RSIZE_MAX, then wscncpy_s sets s1[0] to the null wide character.

# Description

- The wscncpy_s function copies not more than n wide characters (wide characters that follow a null wide character are not copied) from the array pointed to by s1. If no null wide character was copied from s2, s1[n] is set to a null wide character.
- All elements following the terminating null wide character (if any) written by wscncpy_s in the array of slmax wide characters pointed to by s1 take unspecified values when wscncpy_s returns.

# Returns

- The wscncpy_s function returns zero if there was no runtime-constraint violation. Otherwise, a nonzero value is returned.
- The wscncpy_s function can be used to copy a wide string without the danger that the result will not null terminated or that wide characters will be written past the end of the destination array.

> 444) This allows an implementation to copy wide characters from s2 while simultaneously checking any of those wide characters are null. Such an approach writes a wide character to every element of s1 before deciding the first element should be set to the null wide character.
> 445) A zero return value implies that all of the requested characters from the string pointed to by s2 fit within the array pointed to s1 and the result in s1 is null terminated.

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
/* */
wchar_t src1[100] = L"hello";
wchar_t src2[7] = {L'G', L'o', L'o', L'd', L'y', L'e'};
wchar_t dst1[6], dst2[5], dst3[5];
int r1, r2, r3;
r1 = wcscpy_s(dst1, src1, 100);
r2 = wcscpy_s(dst2, src2, 7);
r3 = wcscpy_s(dst3, src2, 5);
```

The first call will assign r1 to dst1 the sequence of characters hello.
The second call will assign r2 to dst2 the sequence of characters \0.
The third call will assign r3 to dst3 the sequence of characters \0.

# K.3.9.2.1.3 wmemcpy_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
errno_t wmemcpy_s(wchar_t * restrict s1,
                  size_t slmax,
                  const wchar_t * restrict s2,
                  size_t n);
```

# Runtime-constraints

Neither s1 nor s2 shall be a null pointer. slmax nor n shall be greater than RSIZE_MAX n shall not be greater than slmax. Copying shall not take place between objects that overlap.

If there is a runtime-constraint violation, the wmemcpy_s function stores zeros in the first slmax characters of the object pointed to by s1 if s1 is not a pointer and slmax is not greater than RSIZE_MAX.

# Description

The wmemcpy_s function copies successive characters from the object pointed to by s2 into the object pointed to by s1.

# Returns

The wmemcpy_s function returns zero if there is no runtime-constraint violation. Otherwise, a nonzero value is returned.

# K.3.9.2.1.4 The wmemmove_s function

# Synopsis

```
#define __WCHAR_WANT_LIB_EXT1__ 1
#include <wchar.h>
errno_t wmemmove_s(wchar_t *s1, size_t rsize,
                   const wchar_t *s2, size_t n);
```

# Runtime-constraints

Neither s1 nor n shall be a null pointer. Neither smax nor n shall be greater than RSIZE_MAX shall not be greater than smax.

If there is a runtime-constraint violation, the wmemmove_s function stores zeros in the first smax wide characters of the object pointed to by s1 if s1 is not a null pointer and smax is not greater than RSIZE_MAX.

# Description

The wmemmove_s function copies n successive wide characters from the object pointed to by s2 into s1. This copying takes place as the n wide characters from the object pointed to by s2 are first copied into a temporary array of n wide characters that do not overlap the objects pointed to by s1 or s2, and then the n wide characters from the temporary array are copied into the object pointed to by s1.

# Returns

The wmemmove_s function returns zero if there was no runtime-constraint violation. Otherwise, a nonzero value is returned.

# K.3.9.2.2 Wide string concatenation functions

# K.3.9.2.2.1 The wcscat_s function

# Synopsis

```
#define __WCHAR_WANT_LIB_EXT1__ 1
#include <wchar.h>
errno_t wcscat_s(wchar_t * restrict s1,
                   size_t smax,
                   const wchar_t * restrict s2);
```

# Runtime-constraints

Let m denote the value smax - wcsllen_s(s1, smax) upon entry to wcscat_s.

Neither s1 nor s2 shall be a null pointer. smax shall not be greater than RSIZE_MAX. smax shall not be equal zero. m shall be greater than be greater than wcsllen_s(s2, m). Copying shall not place objects over objects that.
