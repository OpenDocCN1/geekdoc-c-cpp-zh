The wcsok_s function searches from there for the first wide character in s1 that is contained in the current wide string. If no such wide character is found, the current token extends to the end of the wide string pointed to by s1, and subsequent searches in the same wide string for a token return a null pointer. If such a character is found, it is overwritten by a null character, which terminates the current token.

In all cases, the wcsok_s function stores sufficient information in the pointer pointed to ptr so that subsequent calls, with a null pointer for s1 and the unmodified pointer value ptr, shall start searching past the element overwritten by a wide character (if any).

# Returns

The wcsok_s function returns a pointer to the first wide character of a token, or a null pointer if there is no token or a runtime-constraint violation.

# EXAMPLE

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
static wchar_t str[1] = L"??b,"c";
static wchar_t str2[2] = L"\t \t"
wchar_t *t, *ptr1, *ptr2;
size_t max1 = wcslen(str1+1)
size_t max2 = wcslen(str2+2)

t = wcsok_s(str1, max1, "", &ptr1); // t points to the token "a"
t = wcsok_s(str1, max1, ",\,", &ptr1); // t points to the token "??b"
t = wcsok_s(str2, max2, "\t", &ptr2); // t is a null pointer
t = wcsok_s(NULL, max1, "##", &ptr1); // t points to the token "c"
t = wcsok_s(NULL, max1, "?", &ptr1); // t is a null pointer
```

# K.3.9.2.4 Miscellaneous functions

# K.3.9.2.4.1 The wcslen_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
size_t wcslen_s(const wchar_t *s, size_t maxsize);
```

# Description

The wcslen_s function computes the length of the wide string pointed to by s.

# Returns

If s is a null pointer,^{452} the wcslen_s function returns zero.

Otherwise, the wcslen_s function returns the number of wide characters that precede the terminating null character. If there is no null character in the first maxsize characters of s then wcslen_s returns maxsize. At most the first