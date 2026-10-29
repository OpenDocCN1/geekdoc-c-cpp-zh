# Table 2.5 Floating-Point Data Types

| Type | Storage | Absolute Range of Values (+ and -) |
|---|---|---|
| float | 4 bytes | 1.40129846432481707×10⁻⁴⁵ to 3.40282346638528860×10⁺³⁸ |
| double and long double | 8 bytes | 4.94065645841246544×10⁻³²⁴ to 1.79769313486231570×10⁺³⁰⁸ |

In compilers using the same amount of storage for double and long double numbers, these two data types are identical. (The sizeof() operator in Program 2.1 can always be used to determine the amount of storage your compiler reserves for these data types.) A float literal is indicated by appending an f or F to the number, and a long double is created by appending an l or L to the number. In the absence of these suffixes, a floating-point number defaults to a double. For example, take a look at the following:

+   9.234 indicates a double literal.
+   9.234F indicates a float literal.
+   9.234L indicates a long double literal.

The only difference in these numbers is the amount of storage the computer can use for them. Appendix D (available online) describes the binary storage format used for floating-point numbers and its impact on number precision.

# Exponential Notation

Floating-point numbers can also be written in exponential notation, which is similar to scientific notation and is commonly used to express both very large and very small values in compact form. The following examples show how numbers with decimals can be expressed in exponential and scientific notation:

| Decimal Notation | Exponential Notation | Scientific Notation |
|---|---|---|
| 162.5 | 1.625e2 | 1.625 × 10² |
| 63421. | 6.3421e4 | 6.3421 × 10⁴ |
| .00731 | 7.31e-3 | 7.31 × 10⁻³ |
| .000625 | 6.25e-4 | 6.25 × 10⁻⁴ |

In exponential notation, the letter e stands for "exponent." The number following the e represents a power of 10 and indicates the number of places the decimal point should be moved to obtain the standard decimal value. The decimal point is moved to the right if the number after the e is positive or moved to the left if the number after the e is negative. For example, the e2 in 1.625e2 means move the decimal place two places to the right, so the number becomes 162.5. The e-3 in 7.31e-3 means move the decimal point three places to the left, so 7.31e-3 becomes .00731.

Certain notations occur frequently enough in computer applications that they have their own symbols. Table 2.6 lists the most commonly used of these symbols.