# ISO/IEC 9899:2011 (E)

4 The subject sequence is defined as the longest initial subsequence of the input wide string, starting with the first non-space-wide wide character, that is of the expected form. The subject sequence contains no wide characters if the input string is empty or consists entirely of white space, or if the first non-space-wide wide character is other than a sign or a permissible letter or digit.

5 If the subject sequence has the expected form and the value of base is zero, the sequence of wide characters starting with the first digit is interpreted as an integer constant according to the rules of 6.4.4.1. If the subject sequence has the expected form and the value of base is between 2 and 36, it is used as the base for conversion, assigning to each letter its value as given above. If the subject sequence begins with a minus sign, the value is negated (in the return type). A pointer to the wide string is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

6 In other than the "C" locale, additional locale-specific sequence forms may be accepted.

7 If the subject sequence is empty or does not have the expected form, no conversion is performed; the value of nptr is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

# Returns

8 The wcstoul, wcstoll, wcstoul, and wcstoll return the converted value, if any. If no conversion could be performed, zero is returned. If the correct value is outside the range of representable values, LONG_MIN, LONG_MAX, LLONG_MIN, LLONG_MAX, ULONG_MAX, or ULONG_MAX is returned (according to the return type) sign of the value, and the value of the macro ERANGE is stored in errno.

# 7.29.4.2 Wide string copying functions

# 7.29.4.2.1 The wcscpy function

# Synopsis

```
#include <wchar.h>
wchar_t *wcscpy(wchar_t restrict s1,
               const wchar_t * restrict s2);
```

# Description

2 The wcscpy function copies the wide string pointed to by s2 (including the terminating null character) into the array pointed by s1.

# Returns

3 The wcscpy function returns the value of s1.