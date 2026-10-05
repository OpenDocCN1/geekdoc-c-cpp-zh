white-space characters are the following: space (' '), form feed ('\f'), new-line ('\n'), carriage return ('\r'), horizontal tab ('\t'), and vertical tab ('\v'). In the "C" locale, isspace returns true only for the standard white-space characters.

# 7.4.1.1 The isupper function

Synopsis

```
#include <ctype.h>
int isupper(int c);
```

Description

The isupper function tests for any character that is an uppercase letter or is one of a locale-specific set of characters for which none of iscntrl, isdigit, ispunct, or isspace is true. In the "C" locale, isupper returns true only for the uppercase letters (as defined in 5.2.1).

# 7.4.1.12 The isxdigit

Synopsis

```
#include <ctype.h>
int isxdigit(int c);
```

Description

The isxdigit function tests for any hexadecimal-digit character (as defined in 6.4.4.1).

# 7.4.2 Character case mapping functions

# 7.4.2.1 The tollower function

Synopsis

```
#include <ctype.h>
int tollower(int c);
```

Description

The tollower function converts an uppercase letter to a corresponding lowercase letter.

Returns

If the argument is a character for which isupper is true and there are one or more corresponding characters, as specified by the current locale, for which lower is true, the tollower function returns one of the corresponding characters (always the same one for any given locale); otherwise, the argument is returned unchanged.