The wcstok function searches for there a wide character that is contained in the current separator wide strip. If no wide character is found, the current token extends to the end of the wide string pointed to by s1, and subsequent searches in the same wide string for a token return a null pointer. If such a wide character is found, it is overwritten by a null wide character, which terminates the token.

In all cases, the wcstok function returns sufficient information in the pointer pointed to by ptr so subsequent calls, with a null pointer for s1 and the unmodified pointer value for ptr, will start searching just past the element overwritten by a null wide character (if any).

# Returns

The wcstok function returns a pointer to the first wide character of a token, or a null pointer if there is no token.

# EXAMPLE

```
#include <wchar.h>
static wchar_t str1[] = L"??b,b,"#c"
static wchar_t str2[] = L"\t \t"
wchar_t *t, *ptr1, *ptr2;

t = wcstok(str1, L"??", &ptr1); // t points to the token L""
t = wcstok(NULL, L",", &ptr1); // t points to the token L"??b"
t = wcstok(str2, L"\t", &ptr2); // t is a null pointer
t = wcstok(NULL, L"#", &ptr1); // t points to the token L"c"
t = wcstok(NULL, L"?", &ptr1); // t is a null pointer
```

# ## 7.29.4.5.8 The wmemchr function

# Synopsis

```
#include <wchar.h>
wchar_t *wmemchr(const wchar_t *s, wchar_t c,
size_t n);
```

# Description

The wmemchr function locates the first occurrence of c in the initial n wide characters of the object pointed to by s.

# Returns

The wmemchr function returns a pointer to the located wide character, or a null pointer if the wide character does not occur in the object.