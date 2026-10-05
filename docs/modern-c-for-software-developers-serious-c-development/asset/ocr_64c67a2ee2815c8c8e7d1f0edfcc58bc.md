# Hexadecimal And Octal Literals

Hexadecimal and octal literals are literals of integer type.

A hexadecimal literal, begins with the prefix 0x or 0X and is followed by a sequence of digits in the range`0 through 9, a-f, A-F` . For example:

```
0x23A, 0xB4C, 0XFEA, 0DEAD, 0x5
```

Hexadecimal literals have base 16.

An octal literal, begins with 0 and is followed by a sequence of digits in the range 0-7. For example:

```
045, 076, 06210
```

Octal literals have base 8.

# Floating Point Literals

Floating point literals represent real numbers. A real number has a real part, a fractional part and an optional exponential part:

```
9.87654
987.654
9.87654e+006
9.87654e-005
```

e is the irrational number 2.718218...

Valid floating point literals have the following properties:

+   - In decimal form, the number must include either the decimal point or an exponent part or both.
- In exponential form, the number must include an exponential part.