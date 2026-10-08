# 5.10 Formulating Algorithms: Sentinel-Controlled Iteration

it would lose the fractional part of the quotient before the result of the division was used to initialize average.

# Cast Operator

To perform a floating-point calculation with integers in this example, you first create a temporary floating-point value using the unary cast operator. Line 34 uses the (double) unary operator—which has higher precedence than the arithmetic operators—to create a temporary copy of its operand total, which appears to the right of the operator. The value stored in total is still an integer. Using a cast operator in this manner is explicit conversion.

# Promotions

After the cast operation, the compilation consists of temporary copy of total divided by the integer counter. For arithmetic, the compiler knows how to evaluate only expressions in which the operands are identical. To ensure this, the compiler performs an operation (also called implicit conversion) on an expression containing values of int and double, the compiler promotes int to double values. So, in line 34, the compiler creates a temporary copy of gradeCounter's value double, then performs the floating-point division. Finally, average is initialized with the floating-point value. Section 7.6.1 discusses the allowed-simple promotions.

# Cast Operators for Any Type

We discuss cast operators for other types in Chapter 12. The cast is formed by placing parentheses around the name of a type. This operator is a unary operator—it takes only one operand. C# also supports unary versions of the plus (+) and minus (-) operators—so you can write expressions like +5 or -7. Cast operators have the second precedence. (See the operator chart in Appendix A.)

# 5.10.7 Formatting Floating-Point Numbers

Line 39

```
Console.WriteLine("average is {average:F}");
```

outputs the class average. In this example, we decided that we'd like to display the average rounded to the nearest hundredth and output the average with exactly two digits to the right of the decimal. The format specifier F in the interpolation expression

```
{average:F}
```

typically formats average's value with two digits to the right of the decimal point—again, the Windows culture settings on the user's machine determine the actual format, including the digits to the right of the decimal point, whether commas or periods are used for separating thousands, millions, etc.

# Rounding Floating-Point Numbers

When the F specifier is used to format a floating-point value, the formatted value is rounded to a specific decimal position, although in memory remains un-