# 7.21.6 Formatted input/output functions

+   The formatted input/output functions shall behave as if there is a sequence point after the actions associated with each specifier.²74)

# 7.21.6.1 The fprintf function

Synopsis

```
#include <stdio.h>
int fprintf(FILE * restrict stream,
const char * restrict format, ...);
```

Description

+   The fprintf function writes output to the stream pointed by stream, under control of the string pointed to format by which subsequent arguments are converted for output. If there are insufficient arguments for the format, the behavior is undefined. If the format is exhausted while arguments remain, the excess arguments are evaluated (as always) but are otherwise ignored. The fprintf function returns when the end of the format string is encountered.

+   The format is a multibyte sequence, beginning and ending in its initial shift state. The format is composed of zero or more directives: ordinary multibyte characters (not %), which are unchanged over the output stream; and conversion specifications, of which each results in fetching zero or more arguments, converting them, if applicable, according to the corresponding conversion specifier, and writing the result to the output stream.

+   Each conversion specification is introduced by the character %. After the %, the following appear in sequence:

+   Zero or more flags (in any order) that modify the meaning of the conversion specification.

+   An optional field width. If the converted value has fewer characters than the field, it is padded with spaces (default) on the left (or right, if the left adjustment flag, described later) to the field width. The field width takes the form of an asterisk (described later) or a nonnegative decimal integer²⁷⁵

+   An optional precision that gives the minimum number of digits to appear for the d, o, u, x, and X, the number of digits to appear after the decimal-point character for a, A, e, f, and F, the maximum number of significant digits for the g and G, or the maximum number of bytes to be written for

> ²⁷⁴ The fprintf function performs memory to write to the % specifier.

> ²⁷⁵ Note that 0 is not a flag, not as the beginning of a field width.