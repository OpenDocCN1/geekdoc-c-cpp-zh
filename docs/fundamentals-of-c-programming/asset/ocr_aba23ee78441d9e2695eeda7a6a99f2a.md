# 3.7 Other Numeric Types

C++ supports several other numeric data types:

+   long int—typically provides integers with a greater range than the int type; its abbreviated name is long. It is guaranteed to provide a range of integer values at least as large as the int type.

An integer literal with a L suffix, as in 19L, has type long. A lower case ell (l) is allowed as a suffix as well, but you should not use it because it is difficult for human readers to distinguish between l (lower case elle) and 1 (digit one). The L suffix is used for literal values only; you cannot change an int variable into a long by appending an L. Attempting to do so would change the name of the variable!

+   short int—typically provides integers with a smaller range than the int type; its abbreviated name is short. It is guaranteed that the range of ints is at least as big as the range of shorts.

+   unsigned int—is restricted to nonnegative integers; its abbreviated name is unsigned. While the unsigned type is limited in nonnegative values, it can represent twice as many positive values as the int type. (The name int is actually the short name for signed int and int can be written as signed.)

+   long double—can extend the range and precision of the double type.

While the C++ language standard specifies minimum ranges and precision for all the numeric data types, a particular C++ compiler may exceed the specified minimums.

C++ provides such a variety of numeric types for specialized purposes usually related to building highly efficient programs. We will have little need to use many of these types. Our examples will use mainly the numeric types int for integers, double for an approximation of real numbers, and, less frequently, unsigned when nonnegative integral values are needed.

# 3.8 Characters

The char data type is used to represent single characters: letters of the alphabet (both upper and lower case), digits, punctuation, and control characters (like newline and tab characters). Most systems support the American Standard Code for Information Interchange (ASCII) character set. Standard ASCII can represent 128 different characters. Table 3.4 lists the ASCII codes for various characters.

In C++ source code, characters are enclosed by single quotes ('), as in

```
char ch = 'A';
```

Standard (double) quotes ("") are reserved for strings, which are composed of characters, but strings and chars are very different. C++ strings are covered in Section 11.2.6. The following statement would produce a compiler error message:

```
ch = "A";
```

since a string cannot be assigned to a character variable.

Internally, chars are stored as integer values, and C++ permits assigning numeric values to char variables and assigning characters to numeric variables. The statement