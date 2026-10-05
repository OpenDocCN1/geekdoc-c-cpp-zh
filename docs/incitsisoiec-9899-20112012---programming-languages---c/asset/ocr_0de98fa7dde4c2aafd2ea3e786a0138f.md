The subject sequence is defined as the longest subsequence of the input wide string, starting with the first non-white-space character, that is of the expected form. The subject sequence contains no wide characters if the input wide string is empty, or if the first non-white-space character is other than a sign or a permissible letter or digit.

If the subject sequence has the expected form and the value of base is zero, the sequence of wide characters starting with the first digit is interpreted as an integer constant according to the rules of 6.4.4.1. If the subject sequence has the expected form and the value of base is between 2 and 36, it is used as the base for conversion, assigning to each letter its value as given above. If the subject sequence uses a minus sign, the value resulting from the conversion is negated (in the return type). A pointer to the final wide string is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

In other than "C" locale, additional locale-specific subject sequences may be accepted.

If the subject sequence is empty or does not have the expected form, no conversion is performed; the value of nptr is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

# Returns

The wcstol, wcstoll, wcstoul, and wcstoul return the converted value, if any. If no conversion could be performed, zero is returned. If the correct value is outside the range of representable values, LONG_MIN, LONG_MAX, LLONG_MIN, LLONG_MAX, ULONG_MAX, or ULONG_MAX is returned (according to the return type sign of value, if any), and the value of the macro ERANGE is stored in errno.

# 7.29.4.2 Wide string copying functions

# 7.29.4.2.1 The wcscpy function

# Synopsis

```
#include <wchar.h>
char_t *wcscpy(wchar_t * restrict s1,
const wchar_t * restrict s2);
```

# Description

The wcscpy function copies the wide string pointed to by s2 (including the terminating null wide character) into the array pointed to by s1.

# Returns

The wcscpy function returns the value of s1.