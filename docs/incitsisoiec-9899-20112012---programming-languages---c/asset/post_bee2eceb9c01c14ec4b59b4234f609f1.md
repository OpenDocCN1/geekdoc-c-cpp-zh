
## 7.29.4.6 Miscellaneous functions

### 7.29.4.6.1 The wcslen function

Synopsis

```
#include <wchar.h>
size_t wcslen(const wchar_t *s);
```

Description
The wcslen function computes the length of the wide string pointed to by s.

Returns

The wcslen function returns the number of wide characters that precede the terminating null character.

### 7.29.4.6.2 The wmemset function

Synopsis

```
#include <wchar.h>
wchar_t *wmemset(wchar_t *s, wchar_t c, size_t n);
```

Description
The wmemset function copies the value of c into each of the first n wide characters of the object pointed to by s.

Returns

The wmemset function returns the value of s.

## 7.29.5 Wide character conversion functions

### 7.29.5.1 The wcsftime function

Synopsis

```
#include <time.h>
#include <wchar.h>
size_t wcsftime(wchar_t * restrict s,
size_t maxsize,
const wchar_t * restrict format,
const struct tm * restrict timeptr);
```

Description
The wcsftime function is equivalent to the strftime function, except that:

- The argument s points to the initial element of an array of wide characters into which the generated output is to be placed.

The argument maxSize indicates the limiting number of wide characters.

The argument format is a wide string and the conversion specifiers are replaced by corresponding sequences of wide characters.

The return value indicates the number of wide characters.

Returns

If the total number of resulting wide characters including the terminating null character is not more than maxSize, the wcsftime function returns the number of wide characters placed into the array pointed by s not including the terminating wide character. Otherwise, zero is returned and the contents of the array are indeterminate.

## 7.29.6 Extended multibyte/wide character conversion utilities

The header <wchar.h> declares an extended set of functions for conversion between multibyte characters and wide characters.

Most of the functions — those that are listed as “restartable”, 7.29.6.3 and 7.29.6.4 — take as a last argument pointer to an object of type mbstate_t that is used to describe the current conversion state from a particular multibyte sequence to (the reverse) under the rules of a particular setting for the LC_CTYPE category of the current locale.

On entry, each function takes the described conversion state (either internal or pointed to by an argument) as argument. The conversion state described by the referenced object is altered as needed to track the shift state, and the position within a multibyte character, for the associated multibyte character sequence.

> 348 Thus, a particular mbstate_t object can be used, for example, with both the mbrtowc and mbrtowcs functions as long as they are used to step sequentially through the same multibyte character string.

### 7.29.6.1 Single-byte/wide character conversion functions

### 7.29.6.1.1 The btowc function

Synopsis

```
#include <wchar.h>
wint_t btowc(int c);
```

Description

The btowc function determines whether c constitutes a valid single-byte character in the initial shift state.

Returns

The btowc function returns EOF if c has the value EOF or if (unsigned char) c does not constitute a valid single-byte character in the initial shift state. Otherwise, it returns the wide character representation of that character.

### 7.29.6.1.2 The wctob function

Synopsis

```
#include <wchar.h>
wctob(wint_t c);
```

Description

The wctob function determines whether c corresponds to a member of the extended character set whose multibyte character representation is a single byte when in the initial shift state.

Returns

The wctob function returns EOF if c does not correspond to a multibyte character with length one in the initial shift state. Otherwise, it returns the single-byte representation of that as an unsigned char converted to an int.

### 7.29.6.2 Conversion state functions

### 7.29.6.2.1 The mbsisinit function

Synopsis

```
#include <wchar.h>
mbsisinit(const mstate_t *ps);
```

Description
If ps is not a null pointer, the mbsisinit function determines whether the referenced mstate_t object describes an initial conversion state.

The mbsinit function returns nonzero if ps is a null pointer or if the referenced object describes an initial Restartable conversion state; otherwise, it returns zero.

### 7.29.6.3 multibyte/wide character functions

These functions differ from the corresponding multibyte character functions of 7.2.27 (mblen, mbtowc, and wctom) in that they have an extra parameter, ps, of type pointer to mbstate_t to an object that can completely describe the current conversion state of the associated multibyte sequence. If ps is a null pointer, each function uses its own internal mbstate_t object instead, which is initialized at program startup to the initial conversion state; the functions are not required to avoid data races with other calls to the same function in this case. The implementation behaves as if no library function calls the same function with a null pointer for ps.

Also unlike its corresponding functions, the return value does not represent whether the encoding is state-dependent.

### 7.29.6.3.1 The mbrlen function

Synopsis

```
#include <wchar.h>
size_t mbrlen(const char * restrict s,
    size_t n,
    mbstate_t * restrict ps);
```

Description

The mbrlen function is equivalent to the call:
brtowc(NULL, s, n, ps != NULL ? ps : &internal)
where internal is the mbstate_t object for the mbrlen function, except that the expression designated by ps is evaluated only once.

Returns

The mbrlen function returns a value between zero and n, inclusive, (size_t)-2, or (size_t)(-1).

Forward references: the mbtowc function (7.29.6.3.2).

### 7.29.6.3.2 The mbrtowc function

Synopsis

```
#include <char.h>
size_t mbrtowc(wchar_t * restrict pwc,
const char * restrict s,
size_t n,
mbstate_t * restrict ps);
```

Description
If s is a null pointer, the mbrtowc function is equivalent to the call:
mbrtowc(NULL, "", 1, ps)
In this case, the values of pwc and n are ignored.

If s is not a null pointer, the mbrtowc function inspects at most n bytes beginning with s to determine the number of bytes needed to complete the multibyte character (including any shift sequences). If the function determines that the next multibyte character is complete and valid, it stores that value in the object pointed to by pwc. The resulting state is the initial conversion state.

Returns

The mbrtowc function returns the first of the following that applies (given the current state):

- 0 the next n or fewer bytes complete the null wide character
- between 1 and n inclusive if the next n or fewer bytes complete a multibyte character (which is value stored)
- (size_t)-2 if the next bytes contribute to an incomplete (but potentially valid) multibyte character, and all n bytes have been processed
- (size_t)(-1) if an encoding error occurs: the function stores the value of the macro EILSEQ in errno and the conversion is unspecified.

### 7.29.6.3.3 The wcertomb function

Synopsis

```
#include <wchar.h>
size_t wcertomb(char * restrict s,
wchar_t wc,
mbstate_t * restrict ps);
```

Description
If s is a null pointer, the wcertomb function is equivalent to the call:
wcertomb(buf, L'\0', ps)
where buf is an internal buffer.

If s is not a null pointer, the wcertomb function determines the number of bytes needed to represent the multibyte character given by wc (including any shift sequences), and stores the multibyte character representation in the array whose first element is pointed to by s. At most MB_CUR_MAX bytes are stored. If wc is a null wide character, a null byte is stored, any shift sequence pointed to restore the internal state; the resulting state is described as the initial conversion state.

Returns

The wcertomb function returns the number of bytes stored in the array object (including any shift sequences). When wc is not a valid wide character, an encoding error occurs: the function stores the value of the macro EILSEQ in errno and returns ((size_t) -1);

### 7.29.6.4 Restartable multibyte/wide string functions

These functions differ from the corresponding multibyte string functions of 7.2.8 (mbstowcs and wcstombs) in that they have an extra parameter, ps, of type pointer to mbstate_t that points to an object that can completely describe the current conversion state of the multibyte sequence. If s is a null pointer, each function uses its internal mbstate_t object instead, which is initialized at program startup to the initial conversion state; the functions are not required to avoid races with other calls to the same function in this case.

Also unlike their corresponding functions, the conversion source parameter, src, has a pointer-to-pointer type. When the function is storing the results of conversions (that is, when dst is not a null pointer), the pointer object pointed to by this parameter is updated to reflect the amount of the source processed by invocation.
