
# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

+   (01–53). [tm_year, tm_wday, tm_wday]
%w is replaced by the wday as a decimal number (0–6), where Sunday is 0.
[tm_wday]
%W is replaced by the week number of the year (the first Monday as the first day of week 1) as a decimal number (00–53). [tm_year, tm_wday, tm_wday]
%x is replaced by the locale’s appropriate date representation. [all specified in 7.27.1]
%X is replaced by the locale’s appropriate time representation. [all specified in 7.27.1]
%y is replaced by the last 2 digits of the year as a decimal number (00–99).
[tm_year]
%Y is replaced by the year as a decimal number (e.g., 1997). [tm_year]
%z is replaced by the offset from UTC in the ISO 8601 format “–0430” (meaning 4 hours 30 minutes behind UTC, west of Greenwich), or by no characters if time is determined. [tm_isdst]
%Z is replaced by the locale’s time zone name or abbreviation, or by characters if no time is determined. [tm_isdst]
%% is replaced by %.

+   4 Some conversionifiers can be modified by the inclusion of an E or O modifier character to indicate an alternative format or specification. If the alternative format or specification does not exist for the current locale, the modifier is ignored.
%Ec is replaced by the locale’s date and time representation.
%EC is replaced by the name of the base year (period) in the locale’s alternative representation.
%Ex is replaced by the locale’s alternative date representation.
%EX is replaced by the locale’s alternative time representation.
%Ey is replaced by the offset from %EC (year only) in the locale’s alternative representation.
%EY is replaced by the locale’s full alternative year representation.
%Od is replaced by the day of the month, using the locale’s alternative numeric symbols (filled as leading zeros, or with leading spaces if there is no alternative symbol for zero).
%Oe is replaced by the day of the month, using the locale’s alternative numeric symbols (filled with leading spaces).
%OH is replaced by the hour (24-hour clock), using the locale’s alternative numeric symbols.
%OI is replaced by the hour (12-hour clock), using the locale’s alternative numeric symbols.
%Om is replaced by the month, using the locale’s alternative numeric symbols.
%OM is replaced by the minutes, using the locale’s alternative numeric symbols.
%OS is replaced by the seconds, using the locale’s alternative numeric symbols.
%Ou is replaced by the ISO 8601 weekday as a number in the locale’s alternative representation, where Monday is 1.

%OU is replaced by the week number, using the locale's alternative numeric symbols.
%OV is replaced by the ISO 8601 week number, using the locale's alternative numeric symbols.
%Ow is replaced by the weekday as a number, using the locale's alternative numeric symbols.
%OW is replaced by the week number of the year, using the locale's alternative numeric symbols.
%Oy is replaced by the last 2 digits of the year, using the locale's alternative numeric symbols.

+   5. %G, and %V give values according to the ISO 8601 week-based year. In this system, weeks begin on Monday and 1 of the year is the week that includes January 4th, which is also the week that includes the first Thursday of the month, and is also the week that contains at least four days in it. If the first Monday of January is the 2nd, 3rd, or 4th, the preceding days are part of the last of the preceding week; thus, for Saturday 2nd January 1999, %G is replaced by 1998 and %V is replaced by 53. If December 29th, 30th, or 31st is a Monday, and any following days are part of week 1 of the following year. Thus, for 30th December 1997, %G is replaced by 1998 and %V is replaced by 01.

+   6. If a conversion is not one of the above, the behavior is undefined.

+   7. In the "C" locale, the E and O modifiers are ignored and the replacement strings for the following specifications are:
%a the first three characters of %A.
%A one of "Sunday", "Monday", ..., "Saturday".
%b the first three characters of %B.
%B one of "January", "February", ..., "December".
%c equivalent to %a %b %e %T %Y.
%p one of "AM" or "PM".
%r equivalent to %I:%M:%S %p.
%x equivalent to %m/%d/%y.
%X equivalent to %T.
%Z implementation-defined.

# Returns

+   8. If the number of resulting characters including the terminating null character is not more than maxsize, the str function returns the number of characters placed into the array by s not including the terminating null character. Otherwise, the returned and contents of the array are indeterminate.

# 7.28 Unicode utilities <uchar.h>

+   1. The header <uchar.h> declares types and functions for manipulating Unicode characters.

+   2. The types declared are mbstate_t (described in 7.29.1) and size_t (described in 7.19);

```
char16_t
```

which is an unsigned integer type used for 16-bit characters and is the same type as uint_least16_t (described in 7.20.1.2); and

```
char32_t
```

which is an unsigned integer type used for 32-bit characters and is the same type as uint_least32_t (also described in 7.20.1.2).

# 7.28 Unicode utilities <uchar.h>

+   1. These functions have a parameter, ps, of type mbstate_t that points to an object that can describe the current state. If ps is a null pointer, the function uses its internal mbstate_t object, which is initialized at program startup to the initial state.

# 7.28.1 The mbrtoc16 function

Synopsis

```
#include <uchar.h>
size_t mbrtoc16(char16_t *restrict pc16, const char *restrict s, size_t n, mbstate_t *restrict ps);
```

Description

+   2. If s is a null pointer, the mbrtoc16 function is equivalent to the following:
mbrtoc16(NULL, "", 1, ps)

In this case, the parameters pc16 and n are ignored.

+   3. If s is not a null pointer, the mbrtoc16 function inspects n bytes beginning with s to determine the number of bytes needed to complete the multibyte character (including any shifts). If the function determines that the next multibyte character is complete and valid, it, if pc16 is not a null pointer, stores the value of the first character store successive wide characters without consuming any input.

# Returns

The mbrtoc16 function returns the first of the following that applies (given the current state):

0 if the n or fewer bytes complete the multibyte character that corresponds to the null character (which is stored)
between 1 and n inclusive if the n or fewer bytes complete a valid character (which is stored); the value returned is the number of bytes that complete the multibyte.

(size_t) (-3) if the next character resulting from a previous call has been stored (no bytes from the input have been consumed by this).

(size_t) (-2) if the n bytes contribute to an incomplete (but potentially valid) multibyte character, and all n bytes have been processed (no value is stored).

(size_t) (-1) if an encoding error occurs, in which case the n or fewer bytes do not contribute to a complete and valid multibyte character (no value is stored); the value of the macro EISEQ is stored in errno, and the conversion state is unspecified.

# 7.28.1.2 The c16rtomb function

Synopsis

```
#include <uchar.h>
size_t c16rtomb(char *restrict s, char16_t c16, mbstate_t *restrict ps);
```

Description

+   If s is a null pointer, the c16rtomb function is equivalent to the call
c16rtomb(buf, L'\0', ps)

where buf is an internal buffer.

+   If s is not a null pointer, the c16rtomb function determines the number of bytes needed to represent the wide character given by c16 (including any shift sequences), and stores the multibyte representation in the s. When n has at least the value of the MB_CUR_MAX, this case can only occur if s points at a sequence of redundant shift sequences (for implementations with state-dependent encodings).
