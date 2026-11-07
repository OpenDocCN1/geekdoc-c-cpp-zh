
Figure 8.1 uses the conditional operator (`?`) to determine whether the string " is a " or the string " is not a " should be printed in the output for each character tested. For example, the expression

`isdigit('8') ? "8 is a " : "8 is not a "`

indicates that if '8' is a digit, the string "8 is a " is printed, and if '8' is not a digit (i.e., `isdigit` returns 0), the string "8 is not a " is printed.

### 8.3.2 Functions `islower`, `isupper`, `tolower` and `toupper`

Figure 8.2 demonstrates functions `islower`, `isupper`, `tolower` and `toupper`. Function `islower` determines whether its argument is a lowercase letter (a–z). Function `isupper` determines whether its argument is an uppercase letter (A–Z). Function `tolower` converts an uppercase letter to a lowercase letter and returns the lowercase letter. If the argument is not an uppercase letter, `tolower` returns the argument unchanged. Function `toupper` converts a lowercase letter to an uppercase letter and returns the uppercase letter. If the argument is not a lowercase letter, `toupper` returns the argument unchanged.

```c
// fig08_02.c
// Using functions islower, isupper, tolower and toupper
#include <ctype.h>
#include <stdio.h>

int main(void) {
    printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n", "According to islower:",
        islower('p') ? "p is a " : "p is not a ", "lowercase letter",
        islower('P') ? "P is a " : "P is not a ", "lowercase letter",
        islower('5') ? "5 is a " : "5 is not a ", "lowercase letter",
        islower('!') ? "! is a " : "! is not a ", "lowercase letter");

    printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n", "According to isupper:",
        isupper('D') ? "D is an " : "D is not an ", "uppercase letter",
        isupper('d') ? "d is an " : "d is not an ", "uppercase letter",
        isupper('8') ? "8 is an " : "8 is not an ", "uppercase letter",
        isupper('$') ? "$ is an " : "$ is not an ", "uppercase letter");

    printf("%s%c\n%s%c\n%s%c\n%s%c\n",
        "u converted to uppercase is ", toupper('u'),
        "7 converted to uppercase is ", toupper('7'),
        "$ converted to uppercase is ", toupper('$'),
        "L converted to lowercase is ", tolower('L'));
}
```

![](img/43d318ad505997c339a3ea78d716d162_448_0.png)

Fig. 8.2 | Using functions `islower`, `isupper`, `tolower` and `toupper`. (Part 1 of 2.)

```
According to isupper:
D is an uppercase letter
d is not an uppercase letter
8 is not an uppercase letter
$ is not an uppercase letter

u converted to uppercase is U
7 converted to uppercase is 7
$ converted to uppercase is $
L converted to lowercase is l
```

Fig. 8.2 | Using functions `islower`, `isupper`, `tolower` and `toupper`. (Part 2 of 2.)

### 8.3.3 Functions isspace, iscntrl, ispunct, isprint and isgraph

Figure 8.3 demonstrates functions isspace, iscntrl, ispunct, isprint and isgraph. Function isspace determines whether a character is one of the following whitespace characters: space (' '), form feed ('\f'), newline ('\n'), carriage return ('\r'), horizontal tab ('\t') or vertical tab ('\v'). Function iscntrl determines whether a character is one of the following control characters: horizontal tab ('\t'), vertical tab ('\v'), form feed ('\f'), alert ('\a'), backspace ('\b'), carriage return ('\r') or newline ('\n'). Function ispunct determines whether a character is a printing character other than a space, a digit or a letter, such as $, #, (, ), [, ], {, }, ;, : or %. Function isprint determines whether a character can be displayed on the screen (including the space character). Function isgraph is the same as isprint, except that the space character is not included.

```c
// fig08_03.c
// Using functions isspace, iscntrl, ispunct, isprint and isgraph
#include <ctype.h>
#include <stdio.h>

int main(void) {
    printf("%s\n%s%s%s\n%s%s%s\n%s%s\n", "According to isspace:",
        "Newline", isspace('\n') ? " is a " : " is not a ",
        "whitespace character",
        "Horizontal tab", isspace('\t') ? " is a " : " is not a ",
        "whitespace character",
        isspace('%') ? "% is a " : "% is not a ", "whitespace character");

    printf("%s\n%s%s%s\n%s%s\n", "According to iscntrl:",
        "Newline", iscntrl('\n') ? " is a " : " is not a ",
        "control character",
        iscntrl('$') ? "$ is a " : "$ is not a ", "control character");

    printf("%s\n%s%s\n%s%s\n%s%s\n", "According to ispunct:",
        ispunct(';') ? "; is a " : "; is not a ", "punctuation character",
        ispunct('Y') ? "Y is a " : "Y is not a ", "punctuation character",
        ispunct('#') ? "# is a " : "# is not a ", "punctuation character");

    printf("%s\n%s%s\n%s%s%s\n\n", "According to isprint:",
        isprint('$') ? "$ is a " : "$ is not a ", "printing character",
        "Alert", isprint('\a') ? " is a " : " is not a ",
        "printing character");

    printf("%s\n%s%s\n%s%s%s\n", "According to isgraph:",
        isgraph('Q') ? "Q is a " : "Q is not a ",
        "printing character other than a space",
        "Space", isgraph(' ') ? " is a " : " is not a ",
        "printing character other than a space");
}
```

Fig. 8.3 | Using functions isspace, iscntrl, ispunct, isprint and isgraph. (Part 1 of 2.)

```
According to isspace:
Newline is a whitespace character
Horizontal tab is a whitespace character
% is not a whitespace character

According to iscntrl:
Newline is a control character
$ is not a control character

According to ispunct:
; is a punctuation character
Y is not a punctuation character
# is a punctuation character

According to isprint:
$ is a printing character
Alert is not a printing character

According to isgraph:
Q is a printing character other than a space
Space is not a printing character other than a space
```

Fig. 8.3 | Using functions isspace, iscntrl, ispunct, isprint and isgraph. (Part 2 of 2.)

## Self Check

- 1 (Multiple Choice) Which function is described by “Returns a true value if the argument character is a digit or a letter; otherwise, returns 0 (false)”?
  - a) isalnum.
  - b) isdigit.
  - c) isalpha.
  - d) isxdigit.

Answer: a.

- 2 (Code) What does the following printf print?

```c
printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n", "According to isalpha:",
    isalpha('X') ? "X is a " : "X is not a ", "letter",
    isalpha('m') ? "m is a " : "m is not a ", "letter",
    isalpha('$') ? "$ is a " : "$ is not a ", "letter",
    isalpha('7') ? "7 is a " : "7 is not a ", "letter");
```

Answer:

```
According to isalpha:
X is a letter
m is a letter
$ is not a letter
7 is not a letter
```

## 8.4 String-Conversion Functions

This section presents the string-conversion functions from the general utilities library (<stdlib.h>). These functions convert strings of digits to integer and floating-point values. The following table summarizes the string-conversion functions. The C standard also includes strtoll and strtoull for converting strings to long long int and unsigned long long int, respectively.

| Function prototype | Function description |
|---|---|
| `double strtod(const char *nPtr, char **endPtr);` | Converts the string nPtr to double. |
| `long strtol(const char *nPtr, char **endPtr, int base);` | Converts the string nPtr to long. |
| `unsigned long strtoul(const char *nPtr, char **endPtr, int base);` | Converts the string nPtr to unsigned long. |

### 8.4.1 Function strtod

Function strtod (Fig. 8.4) converts a sequence of characters representing a floating-point value to double. The function returns 0 if it’s unable to convert part of its first argument to double. The function receives two arguments—a string (char *) and a pointer to a string (char **). The string argument contains the character sequence to be converted to double. Whitespace characters at the beginning of the string are ignored. The function uses the char ** argument to aim a char * in the caller (stringPtr) at the first character after the converted portion of the string. If nothing can be converted, the function aims the pointer at the beginning of the string. Line 10 assigns the double value converted from string and aims stringPtr at the % in string.

```c
// fig08_04.c
// Using function strtod
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    const char *string = "51.2% are admitted";
    char *stringPtr = NULL;
```

Fig. 8.4 | Using function strtod. (Part 1 of 2.)
