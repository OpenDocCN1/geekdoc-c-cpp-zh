# 6.2. Floating-Point Numbers

| Escape Character | Output |
| \n | Newline |
| \t | Horizontal tab |
| \r | Carriage return |
| \b | Backspace |
| \f | Form feed |
| \" | Double quote |
| \' | Single quote |
| \\ | Backslash |
| \theta | Null character (ASCII value 0) |
| \a | Alert/bell |
| \v | Vertical tab |
| \xhh | Hexadecimal |
| \000 | Octal |

# 6.1.6 Examples

Here are some examples demonstrating how to use printf to format output in various scenarios.

```
printf("%d\n", alpha);      // use 2 columns
printf("%5d\n", alpha);     // 3 leading spaces
printf("%%-5d\n", alpha);    // 3 trailing space
printf("%%05d\n", alpha);    // 3 leading zeroes
```

Result output:

| 25 |
| 25 | |
| 25 |
| 00025 | |

# 6.2 Printing Floating-Point Numbers

The following are the format specifiers to print floating-point numbers in C:

| Format Specifier | Purpose |
| %%f | Single-precision |
| %%lf | Double-precision |
| %.n | n is the number of digits after decimal point |
| %%e or %%E | Scientific notation "*" |
| %.w | w is the field width |
| %%g | %f or %e, whichever is shorter |

In C, floating-point numbers can be represented using either the float or double data types. Floats typically have a precision of 6-7 decimal digits, while doubles have a precision of 15-16 decimal digits.