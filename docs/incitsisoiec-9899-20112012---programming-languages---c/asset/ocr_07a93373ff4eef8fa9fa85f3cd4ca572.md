# 72.21.1.3 The stod, strtof, and strtol functions

Synopsis

```
#include <stdlib.h>
double strtod(const char * restrict nptr,
    char ** restrict endptr);
float strtof(const char * restrict nptr,
    char ** restrict endptr);
long double strtod(const char * restrict nptr,
    char ** restrict endptr);
```

Description

The stod, strtof, and strtol functions convert the initial portion of the string pointed to by nptr to double, float, and long double representation, respectively. First, they decompose the input string into three parts: an initial, possibly empty, sequence of white-space characters (as specified by the isspace function), a subject sequence resembling a floating-point constant or representing an infinity or NaN; and a final string of one or more unrecognized characters, including the terminating character of the input string. Then, they attempt to convert the subject sequence to a floating-point number, and return the result.

The expected form of the subject sequence is an optional plus or minus sign, then one of the following:

+   - a nonempty sequence of decimal digits optionally containing a decimal-point character, an optional exponent part as defined in 6.4.4.2;
- a 0x or 0X, a nonempty sequence of hexadecimal digits optionally containing a decimal-point character, an optional exponent part as defined in 6.4.4.2;
- INF or INFINITY, ignoring case
- NAN or NAN (n-char-sequence_opt), ignoring case in the NAN part, where:
  n-char-sequence:
    digit
    nondigit
    n-char-sequence digit
    n-char-sequence nondigit

The subject sequence is defined as the longest subsequence of the input string, starting with the first non-white-space character, and that is of the expected form. The subject sequence contains no characters if the input string is not of the expected form.

If the subject sequence has the expected form for a floating-point number, the sequence of characters starting with the first digit or the decimal-point character (whichever occurs first) is interpreted as a floating constant according to the rules of 6.4.4.2, except that the