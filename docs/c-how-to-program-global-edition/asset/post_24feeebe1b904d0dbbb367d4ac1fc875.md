
```c
printf("\n%s\n%s%s\n%s%s\n", "According to isdigit: ",
    isdigit('8') ? "8 is a " : "8 is not a ", "digit",
    isdigit('#') ? "# is a " : "# is not a ", "digit");

printf("\n%s\n%s%s\n%s%s\n%s%s\n",
    "According to isalpha:",
    isalpha('A') ? "A is a " : "A is not a ", "letter",
    isalpha('b') ? "b is a " : "b is not a ", "letter",
    isalpha('&') ? "& is a " : "& is not a ", "letter",
    isalpha('4') ? "4 is a " : "4 is not a ", "letter");

printf("\n%s\n%s%s\n%s%s\n",
    "According to isalnum:",
    isalnum('A') ? "A is a " : "A is not a ",
    "digit or a letter",
    isalnum('8') ? "8 is a " : "8 is not a ",
    "digit or a letter",
    isalnum('#') ? "# is a " : "# is not a ",
    "digit or a letter");

printf("\n%s\n%s%s\n%s%s\n%s%s\n%s%s\n%s%s\n",
    "According to isxdigit:",
    isxdigit('F') ? "F is a " : "F is not a ",
    "hexadecimal digit",
    isxdigit('J') ? "J is a " : "J is not a ",
    "hexadecimal digit",
    isxdigit('7') ? "7 is a " : "7 is not a ",
    "hexadecimal digit",
    isxdigit('$') ? "$ is a " : "$ is not a ",
    "hexadecimal digit",
    isxdigit('f') ? "f is a " : "f is not a ",
    "hexadecimal digit");
}
```

```text
According to isdigit:
8 is a digit
# is not a digit

According to isalpha:
A is a letter
b is a letter
& is not a letter
4 is not a letter

According to isalnum:
A is a digit or a letter
8 is a digit or a letter
# is not a digit or a letter

According to isxdigit:
F is a hexadecimal digit
J is not a hexadecimal digit
7 is a hexadecimal digit
$ is not a hexadecimal digit
f is a hexadecimal digit
```

Figure 8.2 uses the conditional operator (?:) to determine whether the string " is a " or the string " is not a " should be printed in the output for each character tested. For example, the expression

```c
isdigit('8') ? "8 is a " : "8 is not a "
```

indicates that if '8' is a digit, the string "8 is a" is printed, and if '8' is not a digit (i.e., isdigit returns 0), the string "8 is not a" is printed.

### 8.3.2 Functions islower, isupper, tolower and toupper

Figure 8.3 demonstrates functions islower, isupper, tolower and toupper. Function islower determines whether its argument is a lowercase letter (a-z). Function isupper determines whether its argument is an uppercase letter (A-Z). Function tolower converts an uppercase letter to a lowercase letter and returns the lowercase letter. If the argument is *not* an uppercase letter, tolower returns the argument *unchanged*. Function toupper converts a lowercase letter to an uppercase letter and returns the uppercase letter. If the argument is *not* a lowercase letter, toupper returns the argument *unchanged*.

```c
// Fig. 8.3: fig08_03.c
// Using functions islower, isupper, tolower and toupper
#include <stdio.h>
#include <ctype.h>

int main(void)
{
   printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n",
      "According to islower:",
      islower('p') ? "p is a " : "p is not a ",
      "lowercase letter",
      islower('P') ? "P is a " : "P is not a ",
      "lowercase letter",
      islower('5') ? "5 is a " : "5 is not a ",
      "lowercase letter",
      islower('!') ? "! is a " : "! is not a ",
      "lowercase letter");

   printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n",
      "According to isupper:",
      isupper('D') ? "D is an " : "D is not an ",
      "uppercase letter",
      isupper('d') ? "d is an " : "d is not an ",
      "uppercase letter",
      isupper('8') ? "8 is an " : "8 is not an ",
      "uppercase letter",
      isupper('$') ? "$ is an " : "$ is not an ",
      "uppercase letter");

   printf("%s%c\n%s%c\n%s%c\n",
      "u converted to uppercase is ", toupper('u'),
      "'7' converted to uppercase is ", toupper('7'),
33        "$ converted to uppercase is ", toupper('$') );
34     printf("%s%c\n", "L converted to lowercase is ", tolower('L') );
35  }
```

Fig. 8.3 | Using functions islower, isupper, tolower and toupper. (Part 1 of 2.)

```text
According to islower:
p is a lowercase letter
P is not a lowercase letter
5 is not a lowercase letter
! is not a lowercase letter

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

Fig. 8.3 | Using functions islower, isupper, tolower and toupper. (Part 2 of 2.)

### 8.3.3 Functions isspace, iscntrl, ispunct, isprint and isgraph

Figure 8.4 demonstrates functions isspace, iscntrl, ispunct, isprint and isgraph. Function isspace determines whether a character is one of the following whitespace characters: space (' '), form feed ('\f'), newline ('\n'), carriage return ('\r'), horizontal tab ('\t') or vertical tab ('\v'). Function iscntrl determines whether a character is one of the following control characters: horizontal tab ('\t'), vertical tab ('\v'), form feed ('\f'), alert ('\a'), backspace ('\b'), carriage return ('\r') or newline ('\n'). Function ispunct determines whether a character is a printing character other than a space, a digit or a letter, such as $, #, (, [, ], {, }, :, ; or %. Function isprint determines whether a character can be displayed on the screen (including the space character). Function isgraph is the same as isprint, except that the space character is not included.

```c
1  // Fig. 8.4: fig08_04.c
2  // Using functions isspace, iscntrl, ispunct, isprint and isgraph
3  #include <stdio.h>
4  #include <ctype.h>
5
6  int main(void)
7  {
8      printf("\n%s\n%s%s%s\n%s%s%s\n%s%s\n",
9          "According to isspace:",
10         "Newline", isspace('\n') ? " is a " : " is not a ",
11         "whitespace character", "Horizontal tab",
12         isspace('\t') ? " is a " : " is not a ",
13         "whitespace character",
14         isspace('%') ? "% is a " : "% is not a ",
15         "whitespace character");
16
17     printf("%s\n%s%s%s\n%s%s\n", "According to iscntrl:",
18        "Newline", iscntrl('\n') ? " is a " : " is not a ",
19        "control character", iscntrl('$') ? "$ is a " :
20        "$ is not a ", "control character");
21
22     printf("%s\n%s%s\n%s%s\n%s%s\n",
23        "According to ispunct:",
24        ispunct(';') ? "; is a " : "; is not a ",
25        "punctuation character",
26        ispunct('Y') ? "Y is a " : "Y is not a ",
27        "punctuation character",
28        ispunct('#') ? "# is a " : "# is not a ",
29        "punctuation character");
30
31     printf("%s\n%s%s\n%s%s%s\n", "According to isprint:",
32        isprint('$') ? "$ is a " : "$ is not a ",
33        "printing character",
34        "Alert", isprint('\a') ? " is a " : " is not a ",
35        "printing character");
36
37     printf("%s\n%s%s\n%s%s%s\n", "According to isgraph:",
38        isgraph('Q') ? "Q is a " : "Q is not a ",
39        "printing character other than a space",
40        "Space", isgraph(' ') ? " is a " : " is not a ",
41        "printing character other than a space");
42  }
```

Fig. 8.4 | Using functions isspace, iscntrl, ispunct, isprint and isgraph. (Part 1 of 2.)

```text
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

Fig. 8.4 | Using functions isspace, iscntrl, ispunct, isprint and isgraph. (Part 2 of 2.)

## 8.4 String-Conversion Functions

This section presents the string-conversion functions from the general utilities library (`<stdlib.h>`). These functions convert strings of digits to integer and floating-point values. Figure 8.5 summarizes the string-conversion functions. The C standard also includes `strtoll` and `strtoull` for converting strings to `long long int` and `unsigned long long int`, respectively. Note the use of `const` to declare variable `nPtr` in the function headers (read from right to left as “nPtr is a pointer to a character constant”); `const` specifies that the argument value will not be modified.

| Function prototype | Function description |
|---|---|
| `double strtod(const char *nPtr, char **endPtr);` | Converts the string `nPtr` to `double`. |
| `long strtol(const char *nPtr, char **endPtr, int base);` | Converts the string `nPtr` to `long`. |
| `unsigned long strtoul(const char *nPtr, char **endPtr, int base);` | Converts the string `nPtr` to `unsigned long`. |

Fig. 8.5 | String-conversion functions of the general utilities library.

### 8.4.1 Function strtod

Function `strtod` (Fig. 8.6) converts a sequence of characters representing a floating-point value to `double`. The function returns 0 if it’s unable to convert any portion of its first argument to `double`. The function receives two arguments—a string (`char *`) and a pointer to a string (`char **`). The string argument contains the character sequence to be converted to `double`—any whitespace characters at the beginning of the string are ignored. The function uses the `char **` argument to modify a `char *` in the calling function (`stringPtr`) so that it points to the location of the first character after the converted portion of the string or to the entire string if no portion can be converted. Line 11 indicates that `d` is assigned the `double` value converted from `string`, and `stringPtr` is assigned the location of the first character after the converted value (51.2) in `string`.

```c
1  // Fig. 8.6: fig08_06.c
2  // Using function strtod
3  #include <stdio.h>
4  #include <stdlib.h>
5
6  int main(void)
7  {
8      const char *string = "51.2% are admitted"; // initialize string
9      char *stringPtr; // create char pointer
10
11     double d = strtod(string, &stringPtr);
12
```

Fig. 8.6 | Using function strtod. (Part 1 of 2.)
