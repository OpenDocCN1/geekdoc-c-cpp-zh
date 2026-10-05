# 7.29.4.1.2 The wcstol, wcstoll, wcstoul, and wcstull functions

# Synopsis

```
#include <wchar.h>
long int wcstol(
    const wchar_t * restrict nptr,
    wchar_t ** restrict endptr,
    int base);
long int wcstoll(
    const wchar_t * restrict nptr,
    wchar_t ** restrict endptr,
    int base);
ununsigned long int wcstoul(
    const wchar_t * restrict nptr,
    wchar_t ** restrict endptr,
    int base);
unsigned long int wcstull(
    const wchar_t * restrict nptr,
    wchar_t ** restrict endptr,
    int base);
```

# Description

The wcstol, wcstoll, wcstoul, and wcstull functions convert the initial portion of the wide string pointed to by nptr to long int, long long int, unsigned long int, and unsigned long int representation, respectively. First, they decompose the input string into three parts: an, possibly empty, sequence of white-space characters (as specified by the isspace function), a subject sequence resembling an integer in some radix defined by the value of base, and a final string of one or more unrecognized wide characters, including the terminating null character of the input wide string. Then, they attempt to convert the subject sequence to an integer, and return the result.

If the value of base is zero, the expected form of the subject sequence is that of an integer constant as described for the corresponding single-byte characters in 6.4.4.1, optionally preceded by a plus or minus sign, not including an integer suffix. If the value of base is between 2 and 36 (inclusive), the expected form of the subject sequence is a sequence of letters and digits representing an integer with the radix specified by base, optionally preceded by a plus or minus sign, not including an integer suffix. The letters from a (or A) through z (or Z) are assigned the values 10 through 35; only letters and digits whose values are less than that of base are permitted. If the value of base is 16, the wide characters 0x or 0X may optionally precede the sequence of letters and digits, following the sign if present.