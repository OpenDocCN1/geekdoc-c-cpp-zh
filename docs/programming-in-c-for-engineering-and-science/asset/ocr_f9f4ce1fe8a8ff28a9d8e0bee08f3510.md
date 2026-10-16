# Appendix D: Other C++ Features

# C LIBRARIES

Many of the C++ libraries were originally C libraries. The following describes some of the most useful items in the more commonly used libraries.

| Library/function | Description |
|---|---|
| `cassert` (Formerly `assert.h`) | |
| `void assert(bool expr)` | Tests the boolean expression expr and if it is true, allows execution to proceed. If it is false, execution is terminated and an error message is displayed. |
| `cctype` (Formerly `ctype.h`) | |
| `int isalnum(int c)` | Returns true if c is a letter or a digit, false otherwise |
| `int isalpha(int c)` | Returns true if c is a letter, false otherwise |
| `int iscntrl(int c)` | Returns true if c is a control character, false otherwise |
| `int isdigit(int c)` | Returns true if c is a decimal digit, false otherwise |
| `int isgraph(int c)` | Returns true if c is a printing character except space, false otherwise |
| `int islower(int c)` | Returns true if c is lowercase, false otherwise |
| `int isprint(int c)` | Returns true if c is a printing character including space, false otherwise |
| `int ispunct(int c)` | Returns true if c is a punctuation character (not a space, an alphabetic character, or a digit), false otherwise |