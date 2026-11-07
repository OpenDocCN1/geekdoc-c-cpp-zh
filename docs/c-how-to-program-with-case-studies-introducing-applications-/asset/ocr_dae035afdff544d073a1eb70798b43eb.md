| Prototype | Function description |
|---|---|
| `int isblank(int c);` | Returns a true value if c is a blank character that separates words in a line of text; otherwise, it returns 0 (false). |
| `int isdigit(int c);` | Returns a true value if c is a digit; otherwise, it returns 0 (false). |
| `int isalpha(int c);` | Returns a true value if c is a letter; otherwise, it returns 0 (false). |
| `int isalnum(int c);` | Returns a true value if c is a digit or a letter; otherwise, it returns 0 (false). |
| `int isxdigit(int c);` | Returns a true value if c is a hexadecimal digit character; otherwise, it returns 0 (false). (See online Appendix E for a detailed explanation of binary numbers, octal numbers, decimal numbers and hexadecimal numbers.) |
| `int islower(int c);` | Returns a true value if c is a lowercase letter; otherwise, it returns 0 (false). |
| `int isupper(int c);` | Returns a true value if c is an uppercase letter; otherwise, it returns 0 (false). |
| `int tolower(int c);` | If c is an uppercase letter, `tolower` returns c as a lowercase letter; otherwise, it returns the argument unchanged. |
| `int toupper(int c);` | If c is a lowercase letter, `toupper` returns c as an uppercase letter; otherwise, it returns the argument unchanged. |
| `int isspace(int c);` | Returns a true value if c is a whitespace character—newline (`'\n'`), space (`' '`), form feed (`'\f'`), carriage return (`'\r'`), horizontal tab (`'\t'`) or vertical tab (`'\v'`)—otherwise, it returns 0 (false). |
| `int iscntrl(int c);` | Returns a true value if c is a control character—horizontal tab (`'\t'`), vertical tab (`'\v'`), form feed (`'\f'`), alert (`'\a'`), backspace (`'\b'`), carriage return (`'\r'`), newline (`'\n'`) and others—otherwise, it returns 0 (false). |
| `int ispunct(int c);` | Returns a true value if c is a printing character other than a space, a digit, or a letter—such as $, #, (, ), [, ], {, }, ;, : or %—otherwise, it returns 0 (false). |
| `int isprint(int c);` | Returns a true value if c is a printing character (i.e., a character that’s visible on the screen) including a space; otherwise, it returns 0 (false). |
| `int isgraph(int c);` | Returns a true value if c is a printing character other than a space; otherwise, it returns 0 (false). |

# 8.3.1 Functions isdigit, isalpha, isalnum and isxdigit

Figure 8.1 demonstrates functions **isdigit, isalpha, isalnum** and **isxdigit**. Function **isdigit** determines whether its argument is a digit (0–9). Function **isalpha** determines whether its argument is an uppercase (A–Z) or lowercase letter (a–z). Function **isalnum** determines whether its argument is an uppercase letter, a lowercase letter or a digit. Function **isxdigit** determines whether its argument is a hexadecimal digit (A–F, a–f, 0–9).