Here is the sample output:

```
Some number limits for this system:
Biggest int: 2147483647
Smallest long long: -9223372036854775808
One byte = 8 bits on this system.
Largest double: 1.797693e+308
Smallest normal float: 1.175494e-38
float precision = 6 digits
float epsilon = 1.192093e-07
```

The C preprocessor is a useful, helpful tool, so take advantage of it when you can. We’ll show you more applications as you move along through this book.

# Exploring and Exploiting printf() and scanf()

The functions printf() and scanf() enable you to communicate with a program. They are called input/output functions, or I/O functions for short. They are not the only I/O functions you can use with C, but they are the most versatile. Historically, these functions, like all other functions in the C library, were not part of the definition of C. C originally left the implementation of I/O up to the compiler writers; this made it possible to better match I/O to specific machines. In the interests of compatibility, various implementations all came with versions of scanf() and printf(). However, there were occasional discrepancies between implementations. The C90 and C99 standards describe standard versions of these functions, and we’ll follow that standard.

Although printf() is an output function and scanf() is an input function, both work much the same, each using a control string and a list of arguments. We will show you how these work, first with printf() and then with scanf().

# The printf() Function

The instructions you give printf() when you ask it to print a variable depend on the variable type. For example, we have used the %d notation when printing an integer and the %c notation when printing a character. These notations are called conversion specifications because they specify how the data is to be converted into displayable form. We’ll list the conversion specifications that the ANSI C standard provides for printf() and then show how to use the more common ones. Table 4.3 presents the conversion specifiers and the type of output they cause to be printed.

Table 4.3 Conversion Specifiers and the Resulting Printed Output

| Conversion | Output Specification |
|------------|----------------------|
| %a | Floating-point number, hexadecimal digits and p-notation (C99/C11). |
| %A | Floating-point number, hexadecimal digits and P-notation (C99/C11). |