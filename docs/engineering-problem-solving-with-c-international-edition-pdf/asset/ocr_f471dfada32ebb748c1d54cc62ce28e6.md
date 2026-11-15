type specifiers
system dependent

The **type specifiers** for signed integers are `short`, `int`, and `long`, for short integer, integer, and long integer, respectively. The specific ranges of values are **system dependent**, which means that the ranges may vary from one system to another. In the last system of this chapter, we present a program that you can use to determine the ranges of the numeric data types on your system. On many systems, the short integer data type range from –32,768 to 32,767, and the integer and long integer type often represents values from –2,147,483,648 to 2,147,483,647. (The unusual limits such as 32,767 and 2,147,483,647 relate to conversions of binary integers to decimal values.) C++ also allows an **unsigned** qualifier to be added to integer specifiers. An **unsigned** integer can represent only positive values. Signed and unsigned integers can represent the same number of values, but the ranges are different. For example, if an **unsigned short** has the range of values from 0 to 65,535, then a **short** integer has the range of values from –32,768 to 32,767; both data types can represent a total of 65,536 values.

| Declarations: | A type declaration statement defines new identifiers and allocates memory. An initial value may be assigned to the memory location at the time the identifier is defined. Modifiers may also be specified. |
|---|---|
| Syntax | `[modifier] type specifier identifier [= initial value] ; [modifier] type specifier identifier[(initial value)];` |
| Examples | `double x1, y1(0); int counter=0; const int MIN_SIZE=0; bool error(false); char comma(',');` |

The type specifiers for floating-point values are `float` (single precision), `double` (double precision), and `long double` (extended precision). The following statement from program `chapter1_1` thus defines seven objects that all contain double-precision floating-point values:

```
double x1(1), y1(5), x2(4), y2(7),
side1, side2, distance;
```

The difference between the `float`, `double`, and `long double` types relates to the precision (or accuracy) and the range of the values represented. The precision and range are system dependent. Table 2.2 contains precision and range information for integers and floating-point values used by the Microsoft Visual C++ compiler. A program given in Section 2.9 allows you to obtain this information for your computer system. On most systems, a `double` data type stores about twice as many decimal digits of precision as are stored with a `float` data type. In addition, a `double` value will have a wider range of exponent values than a `float` value. The `long double` value may have more precision and a still wider exponent range, but this is again system dependent. A floating-point constant such as 2.3 is as-