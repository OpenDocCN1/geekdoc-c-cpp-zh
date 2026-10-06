# 2.2 Basic Data Types and Expressions — 33

Integer constants can use the suffix L (or l) to denote a long integer type, the suffix U (or u) to denote an unsigned type, or the suffix letters of L and U to denote an unsigned integer type.
For example: 123, 0123, -0x5af are all legal constant forms.

# 2. Real Constants

Real constants are represented in the form of literals, and they have two representations: the general form and index form.
General form: for example: 12.5, -12.5 and so on.
Index form: for example, 0.345E+2 denotes 0.345×100² and -34.4E-3 denotes -34.4×10⁻³. Here the letter E is case insensitive. When using the index form to denote a number, its integral part or the decimal fraction can be omitted, although they cannot be omitted. For example: 123E-1, 1.E 2, and 1.E-3 are all correct forms, but E-3 is wrong.
The default type of real constants is double, and the suffix F (or f) can convert a real constant into a float type. For example: 12.3f.

# 3. Character Constants

A character is one enclosed by single quotes, such as: 'a', 'D', '?', or '\$'.
In addition, there are some characters that cannot be displayed or printed by keyboard, such as ring, newline, tab, etc. How does one write these characters into a program? C++ provides a set of escape sequences to represent these characters. The predefined escape sequences and nonprintable characters in C++ and their meanings are shown in Table 2.2.
Both general characters and nonprintable characters can be represented by octal or hexadecimal ASCII.

```
\nnn octal
\nn hexadecimal
```

nnn denotes a sequence of at most three octal or hexadecimal numbers.

Tab. 2.2: C++ Predefined Escape Characters.
| Character constant form | ASCII code (hexadecimal) | Meaning |
|---|---||
| \a | 07 | Ring |
| \n | 0A | Newline |
| \t | 09 | Horizontal tab |
| \v | 0B | Vertical tab |
| \b | 08 | Backspace |
| \\ | 0D | Carriage Return |
| \\ | 5C | Character "\" |
| \" | 22 | Double quote |
| \' | 27 | Single quote |