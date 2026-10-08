The rounding rule is the usual 4/5 rule: 0 to 4 round down (toward zero) and 5 to 9 round up (away from zero). Note that floating-point formatting applies only to floating-point numbers, so
**1234567** prints as **1234567** (because it’s an integer)
**1234567.0** prints as **1.23457e+006**

In the latter case, the **ostream** determines that **1234567.0** cannot be printed using the **fixed** format using only six digits and switches to **scientific** format to preserve the most accurate representation. Basically the **defaultfloat** format chooses between **scientific** and **fixed** formats to present the user with the most accurate representation of a floating-point value within the precision of the **defaultfloat** format, which defaults to six total digits.

# TRY THIS

Write some code to print the number **1234567.89** three times, first using **defaultfloat**, then **fixed**, then **scientific**. Which output form presents the user with the most accurate representation? Explain why.

A programmer can set the precision using the manipulator **setprecision()**. For example:

```
cout << 1234.56789 << '\t' << fixed << 1234.56789 << '\t' << scientific << 1234.56789 << '\n';
cout << defaultfloat << setprecision(5)
     << 1234.56789 << '\t'
     << fixed << 1234.56789 << '\t'
     << scientific << 1234.56789 << '\n';
cout << defaultfloat << setprecision(8)
     << 1234.56789 << '\t'
     << fixed << 1234.56789 << '\t'
     << scientific << 1234.56789 << '\n';
```

This prints (note the rounding)

**1234.57**         **1234.567890**      **1.234568e+003**
**1234.6**  **1234.56789**    **1.23457e+003**
**1234.5679**     **1234.56789000**    **1.23456789e+003**

The precision is defined as: