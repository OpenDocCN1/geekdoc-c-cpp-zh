
## 3.6.4 Multibyte/wide character conversion functions

The behavior of the multibyte character functions is affected by the LC_CTYPE category of the current locale. For a state-dependent encoding, each function is placed into its initial state by a call for which its character pointer argument, s is a null pointer. Subsequent calls with s other than a null pointer cause the internal conversion state of the function to be altered as necessary. A call with s as a null pointer causes these functions to set the int pointed to by their status argument to a nonzero value if encodings have state dependency, and zero otherwise. 413) Changing the LC_CTYPE category causes the conversion of these functions to be indeterminate.

## 3.6.4.1 wctomomb_s function

### Synopsis

```
#define _STDC_WANT_LIB_EXT1__ 
#include <stdlib.h>
errno_t wctomomb_s(int * restrict status,
char * restrict s,
size_t smax,
wchar_t wc);
```

### Runtime-constraints

If n is the number of bytes needed to represent the multibyte character corresponding to the wide character given by wc (including any shift sequences).

If s is not a null pointer, then s shall not be less than n, and smax shall not be greater than RSIZE_MAX. If s is a null pointer, then smax shall equal zero.

If there is a runtime-constraint violation, wctomomb_s does not modify the int pointed to by status, and if s is not a null pointer, no more than smax elements in the array pointed to by s will be accessed.

### Description

The wctomomb_s function determines n and stores the multibyte character representation of wc in the array whose first element is pointed to by s (if s is not a null pointer). The number of characters stored never exceeds MB_CUR_MAX or smax. If wc is a null character, a null byte is stored, preceded by any shift sequence needed to restore the initial state, and the function is in the initial conversion state.

The implementation shall behave as if no library function calls the wctomomb_s function.

> 413) If the locale employs special bytes to change the shift state, these bytes do not produce wide character codes, but are grouped with an adjacent multibyte character.

If s is a null pointer, the wctomomb_s function stores into the int pointed to by status nonzero or value, if multibyte character encodings, respectively, or do not have state-dependent dependencies.

If s is not a null pointer, the wctomomb_s function stores into the int pointed to by status n or -1 if wc, respectively, does or does not correspond to a valid multibyte character.

In no case will the int pointed to by status be set to a value greater than the MB_CUR_MAX macro.

### Returns

The wctomomb_s function returns zero if successful, and a nonzero value if there was a runtime-constraint violation or wc did not correspond to a valid multibyte character.

## K.3.6.5 Multibyte/wide string functions

The behavior of the multibyte string functions is affected by the LC_CTYPE category of the current locale.

## 3.6.5.1 The mbstowcs_s function

### Synopsis

```
#include <stdlib.h>
errno_t mbstowcs_s(size_t * restrict retval,
char * restrict dst, rsize_t dstmax,
const char * restrict src, rsize_t len);
```

### Runtime-constraints

Neither retval nor src shall be a null pointer. If dst is not a null pointer, neither len nor dstmax shall be greater than RSIZE_MAX. If dst is a null pointer, dstmax shall equal zero. If dst is not a null pointer, dstmax shall not equal zero. If dst is not a null pointer and len is less than dstmax, then null character shall occur within the first dstmax multibyte characters of the array pointed to by src.

If there is a runtime-constraint violation, mbstowcs_s does the following. If retval is not a null pointer, mbstowcs_s sets *retval to (size_t) (-1). If dst is not a null pointer and dstmax is greater than zero and less than RSIZE_MAX, mbstowcs_s sets dst[0] to the null wide character.

### Description

The mbstowcs_s function converts a sequence of multibyte characters that begins in the initial state from the array pointed to by src into a sequence of corresponding wide characters. If dst is not a null pointer, the converted characters are stored into the array pointed to by dst. Conversion continues up to including a terminating null character, which is also stored. Conversion stops earlier in two cases: when a sequence of bytes is counted that does not form a valid multibyte character, or if dst is not a null pointer when len characters have been stored in the array pointed to by dst. 44)) If dst is not a null pointer and no null wide character was stored in the array pointed to by dst, dst[len] is set to the null width character. Each conversion takes place as by a call to the mbstowcs function.

Regardless of whether dst is or not a null pointer, if the input conversion encounters a sequence of bytes that does not form a valid multibyte character, an encoding error occurs: the mbstowcs_s function stores the value (size_t) (-1) to *retval. Otherwise, the mbstowcs_s function stores into *retval the number of multibyte characters successfully converted, not including the terminating null character (if any).

All elements forming the terminating null wide character (if any) written by mbstowcs_s in the array of dstmax characters pointed to by dst take unspecified values when mbstowcs_s returns. 415)

If copying takes place between objects that overlap, the objects take on unspecified values.

### Returns

The mbstowcs_s function returns zero if no runtime-constraint violation and no encoding error occurred. Otherwise, a nonzero value is returned.

## K.3.6.5.2 The wcstows_s function

### Synopsis

```
#include <stdlib.h>
errno_t wcstows_s(size_t * restrict retval,
char * restrict dst, rsize_t dstmax,
const wchar_t * restrict src, rsize_t len);
```

### Runtime-constraints

Neither retval nor src shall be a null pointer. If dst is not a null pointer, then neither len nor dstmax shall be greater than RSIZE_MAX. If dst is a null pointer, then dstmax shall not equal zero. If dst is not a null pointer and len is not less than dstmax, then the conversion shall have been stopped (see below) because a terminating null character was reached or an encoding error occurred.

> 414) Thus, the value of len is ignored if dst is a null pointer.
> 415) This allows an implementation to convert the multibyte string before discovering a terminating null character where required.

If there is a runtime-constraint violation, wcstombs_s does the following. If retval is not a null pointer, wcstombs_s sets *retval (size_t) (-1). If dst is not a null pointer and dstmax is greater than zero and less than RSIZE_MAX, wcstombs_s sets dst[0] to the null character.

### Description

The wcstombs_s function converts a sequence of wide characters from the array pointed to by src into a sequence of corresponding multibyte characters that begins in the initial state. If dst is not a null pointer, the converted characters are stored into the array pointed to by dst. Conversion continues up to including a terminating null character, which is also stored. Conversion stops early in two cases:

- when a wide character is reached that does not correspond to a valid multibyte character;
- (if dst is not a null pointer) the next multibyte character would exceed the limit of n bytes to be stored in the array pointed by dst. If the character being converted is the null character, then n is the lesser of len or dstmax. Otherwise, n is the lesser of dstmax-1.

If the conversion stops without converting a wide character and dst is not a null pointer, then a null character is stored in the array pointed to dst immediately following any multibyte characters already stored. Each conversion takes place as if a call to the wcertmb function were made. 416

Regardless of whether dst is or not a null pointer, if the input encounters a wide character that does not correspond to a valid multibyte character, an encoding error occurs: the wcstombs_s function stores the value (size_t) (-1) into *retval. Otherwise, the wcstombs_s function stores into *retval the number of bytes in the resulting multibyte sequence, including the terminating null character (if any).

All elements following the terminating null character (if any) written by wcstombs_s in the array of dstmax elements pointed to by dst take unspecified values when wcstombs_s returns. 417

If copying takes place between objects that overlap, the objects take on unspecified values.

> 4⁶ If conversion stops because a terminating null character has been reached, the bytes include those necessary to reach the initial shift state immediately before the null byte. However, if the conversion stops before a terminating null character has been reached, the result will be null, but might not end in the initial shift state.
