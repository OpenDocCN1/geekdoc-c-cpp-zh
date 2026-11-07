The character-handling library includes several functions that perform useful tests and manipulations of character data. Each function receives a character—represented as an int—or EOF as an argument. *Characters are often manipulated as integers.* Remember that EOF normally has the value -1 and that some hardware architectures do not allow negative values to be stored in char variables. Therefore, the character-handling functions manipulate characters as integers. Figure 22.17 summarizes the functions of the character-handling library. When using functions from the character-handling library, include the `<ctype>` header.

| Prototype | Description |
|---|---|
| `int isdigit( int c )` | Returns 1 if c is a *digit* and 0 otherwise. |
| `int isalpha( int c )` | Returns 1 if c is a *letter* and 0 otherwise. |
| `int isalnum( int c )` | Returns 1 if c is a *digit or a letter* and 0 otherwise. |
| `int isxdigit( int c )` | Returns 1 if c is a *hexadecimal digit* character and 0 otherwise. (See Appendix D for a detailed explanation of binary, octal, decimal and hexadecimal numbers.) |
| `int islower( int c )` | Returns 1 if c is a *lowercase letter* and 0 otherwise. |
| `int isupper( int c )` | Returns 1 if c is an *uppercase letter*; 0 otherwise. |
| `int tolower( int c )` | If c is an *uppercase letter*, tolower returns c as a *lowercase letter*. Otherwise, tolower returns the argument *unchanged*. |
| `int toupper( int c )` | If c is a *lowercase letter*, toupper returns c as an *uppercase letter*. Otherwise, toupper returns the argument *unchanged*. |
| `int isspace( int c )` | Returns 1 if c is a *whitespace character*—newline ('\\n'), space (' '), form feed ('\\f'), carriage return ('\\r'), horizontal tab ('\\t'), or vertical tab ('\\v')—and 0 otherwise. |
| `int isctrl( int c )` | Returns 1 if c is a *control character*, such as newline ('\\n'), form feed ('\\f'), carriage return ('\\r'), horizontal tab ('\\t'), vertical tab ('\\v'), alert ('\\a'), or backspace ('\\b')—and 0 otherwise. |
| `int ispunct( int c )` | Returns 1 if c is a *printing character other than a space, a digit, or a letter* and 0 otherwise. |
| `int isprint( int c )` | Returns 1 if c is a *printing character including space* (' ') and 0 otherwise. |
| `int isgraph( int c )` | Returns 1 if c is a *printing character other than space* (' ') and 0 otherwise. |

**Fig. 22.17** | Character-handling library functions.

Figure 22.18 demonstrates functions `isdigit`, `isalpha`, `isalnum` and `isxdigit`. Function `isdigit` determines whether its argument is a digit (0–9). Function `isalpha` determines whether its argument is an *uppercase letter* (A–Z) or a *lowercase letter* (a–z). Function `isalnum` determines whether its argument is an *uppercase letter, a lowercase letter or a digit*. Function `isxdigit` determines whether its argument is a *hexadecimal digit* (A–F, a–f, 0–9).