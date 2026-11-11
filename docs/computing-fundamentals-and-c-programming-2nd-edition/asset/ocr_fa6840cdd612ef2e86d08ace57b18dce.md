+   6. else, if one of the operands is **long int**, the other will be converted to **long int** and the result will be **long int**;
+   7. else, if one of the operands is **unsigned int**, the other will be converted to **unsigned int** and the result will be **unsigned int**.

# **Conversion Hierarchy**

Note that, C uses the rule that, in all expressions except assignments, any implicit type conversions are made from a lower size type to a higher size type as shown below:

![](bbox=[0.294, 0.275, 0.706, 0.51])

Note that some versions of C automatically convert all floating-point operands to double precision.

The final result of an expression is converted to the type of the variable on the left of the assignment sign before assigning the value to it. However, the following changes are introduced during the final assignment.

+   1. **float to int** causes truncation of the fractional part.
+   2. **double to float** causes rounding of digits.
+   3. **long int to int** causes dropping of the excess higher order bits.

# **5.14.2 Explicit Conversion**

We have just discussed how C performs type conversion automatically. However, there are instances when we want to force a type conversion in a way that is different from the automatic conversion. Consider, for example, the calculation of ratio of females to males in a town.

```
```
ratio = female_number/male_number
```
```

Since **female_number** and **male_number** are declared as integers in the program, the decimal part of the result of the division would be lost and **ratio** would represent a wrong figure. This problem can be solved by converting locally one of the variables to the floating point as shown below:

```
```
ratio = (float) female_number/male_number
```
```

The operator **(float)** converts the **female_number** to floating point for the purpose of evaluation of the expression. Then using the rule of automatic conversion, the division is performed in floating point mode, thus retaining the fractional part of result.

Note that in no way does the operator **(float)** affect the value of the variable **female_number**. And also, the type of **female_number** remains as int in the other parts of the program.