
## 27.9.6.3.2 The mbrtowc function

### Synopsis

```
#include <wchar.h>
size_t mbrtowc(wchar_t * restrict pwc,
const char * restrict s,
size_t n,
mbstate_t * restrict ps);
```

### Description

If s is a null pointer, the mbrtowc function is equivalent to the call:
mbrtowc(NULL, "", 1, ps)
In this case, the values of the parameters pwc and n are ignored.

If s is not a null pointer, the mbrtowc function inspects at n bytes beginning with the byte pointed by s to determine the number of bytes needed to complete the next multibyte character (including any shift sequences). If the function determines the next multibyte character is complete and determines the value of the corresponding wide character and, if pwc is not a null pointer, stores in the object pointed by pwc. If the corresponding wide character is the wide wide character, the resulting state described is the initial conversion state.

### Returns

The mbrtowc function returns the first of the following that applies (given the current conversion state):

- 0 if the n or fewer bytes the multibyte character corresponds to the null wide character (which is the value stored).
- between 1 and n if the n or fewer bytes complete a valid multibyte character (which is the value stored); the value returned is the number of bytes that complete the multibyte character.
- (size_t) -2 if the n bytes contribute to an incomplete (but potentially valid) multibyte character, and all n bytes have been processed (no value is stored).³⁹
- (size_t) -1 if an encoding error occurs, in which case the n or fewer bytes do not contribute to a complete and valid multibyte character (no value is stored); the value of the macro EILSEQ is stored in errno, and the conversion is unspecified.

## ISO/IEC 9899:2011 (E)

## 7.29.6.3.3 The wctomb function

### Synopsis

```
#include <wchar.h>
size_t wctomb(char * restrict s,
wchar_t wc,
mbstate_t * restrict ps);
```

### Description

If s is a null pointer, the wctomb function is equivalent to the call
wctomb(buf, L'0', ps)
where buf is an internal buffer.

If s is not a null pointer, the wctomb function determines the number of bytes needed
to represent the multibyte character that corresponds to the wide character given by wc
(including any shift sequences), and stores the multibyte representation in the
array whose first element is pointed to s. At most MB_CUR_MAX bytes are stored. If wc is a wide character, a null byte is stored, preceded by any shift sequence
to restore the initial shift state; the resulting state is the initial conversion state.

### Returns

The wctomb function returns the number of bytes stored in the array object (including
any shift sequences). When wc is not a valid wide character, an encoding error occurs:
the function stores the value of the macro EILSEQ in errno and returns
(size_t)1; the conversion is unspecified.

## 7.29.6.4 Restartable multibyte/wide string conversion functions

These functions differ from the corresponding multibyte string functions of 7.22.8
owcs and mbctombs that they have an extra parameter, ps, pointer to
mbstate_t which points to an object that can completely describe the current conversion
state of the associated multibyte character sequence. If ps is a null pointer, each function
uses its own internal mbstate_t object instead, which is initialized at program startup
to the initial conversion state; the functions are not required to avoid data races with other
calls to the same function in this. The implementation behaves as if no library
function calls these functions with a null pointer for ps.

Also unlike their counterparts, the conversion source parameter, src, has a pointer-to-pointer type. When the function is storing the results of conversions (that is, when dst is not a null pointer), the object pointed to by this parameter is updated to reflect the amount of the source processed by that invocation.

### 7.29.6.4.1 The mbsrtowcs function

### Synopsis

```
#include <wchar.h>
size_t mbsrtowcs(wchar_t * restrict dst,
               const char ** restrict src,
               size_t len,
mbstate_t * restrict ps);
```

### Description

The mbsrtowcs function converts a sequence of multibyte characters that begins in the conversion state described by the object pointed to by ps, from the array indirectly pointed by src into a sequence of corresponding wide characters. If dst is not a null pointer, the converted characters are stored in the array pointed to by dst. Conversion continues up and including a terminating null character, which is also stored. Conversion stops earlier in two cases: when a sequence of bytes is encountered that does not form a valid multibyte character, or (if dst is not a null pointer) when len wide characters have been stored into the array pointed to by dst.³ Each conversion takes place as if it were a call to the mbsrtowcs function.

If dst is not a null pointer, the object pointed to by src is assigned either a null pointer (if conversion stopped due to reaching a terminating null character) or the address just past the last multibyte character converted (if any). If conversion stopped due to reaching a terminating null character and if dst is not a null pointer, the resulting state described is the initial conversion state.

### Returns

If the input contains a sequence of bytes that do not form a valid multibyte character, an encoding error occurs: the mbsrtowcs function returns the value of the macro EILSEQ in errno and returns (size_t)-1; the conversion is unspecified. Otherwise, it returns the number of multibyte characters successfully converted, not including the null character (if any).⁵⁰, the value of len is ignored if dst is a null pointer.

## 7.29.6.4.2 The wcsrtombs function

### Synopsis

```
#include <wchar.h>
size_t wcsrtombs(char * restrict dst,
               const wchar_t ** restrict src,
               size_t len,
               mbstate_t * restrict ps);
```

### Description

The wcsrtombs function converts a sequence of wide characters from the array indirectly pointed by src into a sequence of multibyte characters that begins in the conversion by the object pointed to by ps. If dst is not a null pointer, the converted characters are then stored into the array pointed by dst. Conversion continues up and including a terminating null character, which is also stored. Conversion stops earlier in two cases: when a wide character is reached that does not correspond to a multibyte character, or if dst is not a null pointer when next multibyte character would exceed the limit of bytes to be stored into the array pointed by dst.

If dst is not a null pointer, the object pointed to by src is either a null pointer (if conversion stopped due to reaching a terminating null character) or the address just past the last wide character converted (if any). If conversion stopped due to reaching a terminating null character, the resulting state described is the initial conversion state.

### Returns

If conversion stops because a wide character is reached that does not correspond to a multibyte character, an encoding error occurs: the wcsrtombs function stores the value of the macro EISSEQ in errno and returns (size_t)1; the conversion is unspecified. Otherwise, it returns the number of bytes in the multibyte sequence, not including the null character (if any).³¹ If conversion stops because a terminating null character has been reached, the bytes stored include those necessary to reach the initial state before the null byte.

## 7.30 Wide character classification and mapping utilities <wctype.h>

### 7.31 Introduction

- 1 The header <wctype.h> defines one macro, and declares three data types and many functions. ⁵²
- 2 The types declared are
wint_t
described in 7.29.1;
wctrans_t
which is a scale type that can hold values which represent locale-specific character mappings; and
wctype_t
which is a scale type that can hold values which represent locale-specific character classifications.
- 3 The macro defined is WEOF (described in 7.29.1).
- 4 The functions declared are grouped as follows:
— Functions that provide wide character classification;
— Extensible functions that provide wide character case mapping;
— Extensible functions that provide wide character mapping.
- 5 For all functions described in this subclass that accept an argument of type wint_t, the value should be representable as a wchar_t or equal the value of the macro WEOF. If this argument has any other value, the behavior is undefined.
- 6 The behavior of these functions is affected by the LC_CTYPE category of the current locale.

> ⁵² See “future library directions” (7.31.17).
