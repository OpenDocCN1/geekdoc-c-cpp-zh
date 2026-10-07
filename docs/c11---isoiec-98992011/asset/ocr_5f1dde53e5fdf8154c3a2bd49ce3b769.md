# 72.29.4.5.6 The wcsstr function

Synopsis

```
#include <wchar.h>
wchar_t *wcsstr(const wchar_t *s1, const wchar_t *s2);
```

Description

The wcsstr function locates the first occurrence in the wide string pointed to by s1 of the sequence of wide characters (excluding the terminating null character) in the wide string pointed to by s2.

Returns

The wcsstr function returns a pointer to the located wide string, or a null pointer if the wide string is not found. If s2 points to a wide string with zero length, the function returns s1.

# 7.29.4.5.7 The wctok function

Synopsis

```
#include <wchar.h>
wchar_t *wctok(wchar_t * restrict s1,
const wchar_t *restrict s2,
wchar_t **restrict ptr);
```

Description

A sequence of characters in the wctok function breaks the wide string pointed to by s1 into a sequence of tokens, each of which is delimited by a wide character from the wide string pointed to by s2. The third argument points to a caller-provided wchar_t * pointer into which the wctok function stores information for it to continue scanning the same wide string.

The first call in a sequence has a non-null first argument and stores an initial value in the object pointed to by ptr. Subsequent calls in the sequence have a first argument and the object pointed by ptr is required to hold the value stored by the previous call in the sequence, which is then updated. The separator wide string pointed to by s2 may be different from call to call.

The first call in the sequence searches the wide string pointed to by s1 for the first wide character that is not contained in the current separator wide string pointed to by s2. If no such wide character is found, then there are no tokens in the string pointed to by s1 and the wctok function returns a null pointer. If such a character is found, it is the start of the first token.