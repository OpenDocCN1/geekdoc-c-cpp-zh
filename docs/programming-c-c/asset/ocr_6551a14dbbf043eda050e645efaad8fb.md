# Introduction to C Language, Variables, Data Types and Operators

While representing decimal form, you must include the decimal point, the exponent, or both; and while representing exponential form, you must include the integer part, the fractional part, or both. The signed exponent is introduced by e or E.

Here are some examples of floating-point literals.

| 3.14159 | /* Legal */ |
| 314159-SL | /* Legal */ |
| 510E | /* Illegal: incomplete exponent */ |
| 210f | /* Illegal: no decimal or exponent */ |
| .55 | /* Illegal: missing integer or fraction */ |

# Character Constants

Character literals are enclosed in single quotes, e.g., 'x' can be stored in a simple variable of char type.

A character literal can be a plain character (e.g., 'x'), an escape sequence (e.g., '\t'), or a universal character (e.g., '\u02C0').

There are certain characters in C that represent special meaning when preceded by a backslash for example, newline(\n) or tab (	).

Following is the example to show a few escape sequence characters.

```
#include <stdio.h>

int main() {
    printf("Hello\tWorld\n\n");
    return 0;
}
```

When the code is compiled and executed, it produces the following result:

Hello World

# String Literals

String literals or constants are enclosed in double quotes " \ A string contains characters that are similar to character literals: plain characters, escape sequences, and universal characters.