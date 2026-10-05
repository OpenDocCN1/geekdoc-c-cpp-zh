# K.3.9.2.3 Wide string search functions

# K.3.9.2.3.1 The wcstok_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
wchar_t *wcstok(wchar_t * restrict s1,
size_t * restrict slmax,
const wchar_t * restrict s2,
wchar_t ** restrict ptr);
```

Runtime-constraints

None of slmax, s2, or ptr will be a null pointer. If s1 is a null pointer, then *ptr shall not a null pointer. The value of *slmax shall not be greater than RSIZE_MAX. The end of the token shall occur within the first *slmax wide characters of s1 for the first call, and shall occur within the first *slmax wide characters of searching resumes on subsequent calls.

If there is a runtime-constraint violation, the wcstok_s function does not indirect through the s1 or s2 pointers, and does not store a value in the object pointed to by ptr.

Description

A sequence of calls to the wcstok_s function breaks the wide string pointed to by s1 into a sequence of tokens, each of which is delimited by a wide character from the wide string pointed to by s2. The fourth argument points to a caller-provided wchar_t pointer into which the wcstok_s function stores information necessary for it to continue scanning the wide string.

The first call in a sequence has a non-null first argument and slmax points to an object whose value is the number of elements in the wide character array pointed to by the first argument. The call stores an initial value in the object pointed to by ptr and updates the value pointed to by slmax to reflect the number of elements that remain in relation to ptr. Subsequent calls in the sequence have a null first argument and the objects pointed to by slmax and ptr are required to have the values stored by the previous call in the sequence, which are then updated. The separator wide string pointed to by s2 may be different from call to call.

The first call in the sequence searches the wide string pointed to by s1 for the first wide character that is not contained in the current separator wide string pointed to by s2. If such wide character is found, then there are no tokens in the wide string pointed to by s1 and the wcstok_s function returns a null pointer. If such a wide character is found, it is the start of the first token.