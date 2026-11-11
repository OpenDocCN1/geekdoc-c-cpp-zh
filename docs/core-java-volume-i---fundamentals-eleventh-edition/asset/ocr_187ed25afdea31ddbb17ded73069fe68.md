# 3.5.3 Conversions between Numeric Types

It is often necessary to convert from one numeric type to another. Figure 3.1 shows the legal conversions.

![](bbox=[0.229, 0.25, 0.861, 0.543])

Figure 3.1  Legal conversions between numeric types

The six solid arrows in Figure 3.1 denote conversions without information loss. The three dotted arrows denote conversions that may lose precision. For example, a large integer such as 123456789 has more digits than the float type can represent. When the integer is converted to a float, the resulting value has the correct magnitude but loses some precision.

```
int n = 123456789;
float f = n; // f is 1.23456792E8
```

When two values are combined with a binary operator (such as n + f where n is an integer and f is a floating-point value), both operands are converted to a common type before the operation is carried out.

+   - If either of the operands is of type `double`, the other one will be converted to a `double`.
+   - Otherwise, if either of the operands is of type `float`, the other one will be converted to a `float`.