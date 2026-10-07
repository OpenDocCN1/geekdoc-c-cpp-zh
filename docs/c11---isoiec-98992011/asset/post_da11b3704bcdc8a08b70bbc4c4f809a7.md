
## 72.29.4.2.2 The wscncpy function

Synopsis

```
#include <wchar.h>
wchar_t *wscncpy(wchar_t * restrict s1,
const wchar_t * restrict s2,
size_t n);
```

Description

The wscncpy function copies not more than n wide characters (those that follow a null wide character are not copied) from the array pointed to by s2 to the array pointed to by s1.

If the array pointed to by s2 is a wide string that is shorter than n wide characters, null wide characters are appended to the copy in the array pointed to by s1, until n wide characters have all been written.

Returns

The wscncpy function returns the value of s1.

## 72.29.4.2.3 The wmemcpy function

Synopsis

```
#include <wchar.h>
wchar_t *wmemcpy(wchar_t * restrict s1,
const wchar_t * restrict s2,
size_t n);
```

Description

The wmemcpy function copies n wide characters from the object pointed to by s2 to the object pointed to by s1.

Returns

The wmemcpy function returns the value of s1.

## 7.29.4.2.4 The wmemmove function

Synopsis

```
#include <wchar.h>
wchar_t *wmemmove(wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wmemmove function copies n wide characters from the object pointed to by s2 to the object pointed to by s1. Copying takes place if the n wide characters from the object pointed to by s2 are first copied into a temporary array of n wide characters that does not overlap the objects pointed to by s1 or s2, and the n wide characters from the temporary array are copied into the object pointed to by s1.

Returns

The wmemmove function returns the value of s1.

## 7.29.4.3 Wide string concatenation functions

### 7.29.4.3.1 The wscat function

Synopsis

```
#include <wchar.h>
wchar_t *wscat(wchar_t * restrict s1,
wchar_t * restrict s2);
```

Description

The wscat function appends a copy of the wide string pointed to by s2 (including the terminating null character) to the end of the wide string pointed to by s1. The initial wide character of s2 overwrites the null character at the end of s1.

Returns

The wscat function returns the value of s1.

### 7.29.4.3.2 The wscncat function

Synopsis

```
#include <wchar.h>
wchar_t *wscncat(wchar_t * restrict s1,
wchar_t * restrict s2,
size_t n);
```

Description

The wscncat function appends more than n wide characters (a null wide character and those that follow are not appended) from the array pointed to by s2 to the end of the wide string pointed to by s1. The initial wide character of s2 overwrites the null wide character at the end of s1. A terminating null character is always appended to the result.

Returns

- The wscncat returns the value of s1.

## 7.29.4.4 Wide string comparison functions

- Unless explicitly stated otherwise, the functions described in this subclause order two wide characters the same way as those of the underlying integer type designated by wchar_t.

### 7.29.4.1 The wscmp function

Synopsis

```
#include <wchar.h>
int wscmp(const wchar_t *s1, const wchar_t *s2);
```

Description

- The wscmp function compares the wide string pointed to by s1 to the wide string pointed to by s2.

Returns

- The wscmp function returns an integer greater than, equal to, or less than zero, accordingly as the wide string pointed to by s1 is greater than, equal to, or less than the wide string pointed to by s2.

### 7.29.4.4.2 The wscoll function

Synopsis

```
#include <wchar.h>
int wscoll(const wchar_t *s1, const wchar_t *s2);
```

Description

- The wscoll function compares the wide string pointed to by s1 to the wide string pointed to by s2, both interpreted as appropriate to the LC_COLLATE category of the current locale.

Returns

- The wscoll function returns an integer greater than, equal to, or less than zero, accordingly as the wide string pointed to by s1 is greater than, equal to, or less than the wide string pointed to by s2. Thus, the maximum number of wide characters that can be used in the array pointed to by s1 is wcslen(s1)+n.

### 7.29.4.4.3 The wcsncmp function

Synopsis

```
#include <wchar.h>
int wcsncmp(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcsncmp function compares not more than n characters (those that follow a null character are not compared) from the array pointed to by s1 to the array pointed to by s2.

Returns

The wcsncmp returns an integer greater than, equal to, or less than zero, as the possibly null-terminated array pointed to by s1 is greater than, equal to, or less than the wide string pointed to by s2.

### 7.29.4.4.4 The wcsnrnc function

Synopsis

```
#include <wchar.h>
int wcsnrnc(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcsnrnc function compares not more than n characters (those that follow a null character are not compared) from the array pointed to by s1 to the array pointed to by s2.

Returns

The wcsnrnc function returns an integer greater than, equal to, or less than zero, accordingly as the possibly null-terminated array pointed to by s1 is greater than, equal to, or less than the wide string pointed to by s2.

### 7.29.4.4.5 The wcswcmp function

Synopsis

```
#include <wchar.h>
int wcswcmp(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcswcmp function compares not more than n characters (those that follow a null character are not compared) from the array pointed to by s1 to the array pointed to by s2.

Returns

The wcswcmp function returns an integer greater than, equal to, or less than zero, accordingly as the possibly null-terminated array pointed to by s1 is greater than, equal to, or less than the wide string pointed to by s2.

### 7.29.4.4.6 The wcsstrmp function

Synopsis

```
#include <wchar.h>
int wcsstrmp(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcsstrmp function compares not more than n characters (those that follow a null character are not compared) from the array pointed to by s1 to the array pointed to by s2.

Returns

The wcsstrmp function returns an integer greater than, equal to, or less than zero, accordingly as the possibly null-terminated array pointed to by s1 is greater than, equal to, or less than the wide string pointed to by s2.

### 7.29.4.4.7 The wcsspn function

Synopsis

```
#include <wchar.h>
size_t wcsspn(const wchar_t *s1, const wchar_t *s2);
```

Description

The wcsspn function computes the length of the maximum initial segment of the wide string pointed to by s1 which consists entirely of wide characters from the wide string pointed to by s2.

Returns

The wcsspn returns the length of the segment.

### 7.29.4.4.8 The wcspn function

Synopsis

```
#include <wchar.h>
size_t wcspn(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcspn function transforms the wide string pointed to by s2 and places not more than n characters into the array pointed to by s1.

Returns

The wcspn returns the length of the segment placed.

### 7.29.4.4.9 The wcsbrk function

Synopsis

```
#include <wchar.h>
size_t wcsbrk(wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcsbrk function transforms the wide string pointed to by s2 and places not more than n characters into the array pointed to by s1.

Returns

The wcsbrk returns the length of the segment placed.

### 7.29.4.4.10 The wcsspan function

Synopsis

```
#include <wchar.h>
size_t wcsspan(wchar_t *s1, const wchar_t *s2,
size_t n);
```

Description

The wcsspan transforms the wide string pointed to by s2 and places not more than n characters into the array pointed to by s1.

Returns

The wcsspan returns the length of the segment placed.
