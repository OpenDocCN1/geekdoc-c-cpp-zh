# Converting Between Fundamental Types Explicitly and Implicitly

The variable average is declared to be of type double (line 48 of Fig. 4.13) to capture the fractional result of our calculation. However, total and gradeCounter are both integer variables. Recall that dividing two integers results in integer division, in which any fractional part of the calculation is lost (i.e., truncated). In the following statement:

```
average = total / gradeCounter;
```

the division occurs first—the result’s fractional part is lost before it’s assigned to average. To perform a floating-point calculation with integers, we must create temporary floating-point values. C++ provides the unary cast operator to accomplish this task. Line 74 uses the cast operator static_cast<double>(total) to create a temporary floating-point copy of its operand and returns—total. Using a cast operator in this manner is called explicit conversion. The value stored in total is still an integer.

The calculation now consists of a floating-point value (the temporary double version of total) divided by the integer gradeCounter. The compiler knows how to evaluate only expressions in which the operand types are identical. To ensure that the operands are of the same type, the compiler performs an operation called promotion (also called implicit conversion) on selected operands. For example, in an expression containing values of data types int and double, C++ promotes int operands to double values. In our example, we are treating total as a double (by using the unary cast operator), so the compiler promotes gradeCounter to double, allowing the calculation to be performed—the result of the floating-point division is assigned to average. In Chapter 6, Functions and an Introduction to Recursion, we discuss all the fundamental data types and their order of promotion.

> **Common Programming Error 4.13**
> 
> The cast operator can be used to convert between fundamental numeric types, such as int and double, and between related class types (as we discuss in Chapter 13, Object-Oriented Programming: Polymorphism). Casting to the wrong type may cause errors.

![](bbox=[0.161, 0.529, 0.219, 0.583])

Cast operators are available for use with every data type and with class types as well. The static_cast operator is formed by following keyword static_cast with angle brackets (< and >) around a data-type name. The cast operator is a unary operator—an operator that takes only one operand. In Chapter 2, we studied the binary arithmetic operators. C++ also supports unary versions of the plus (+) and minus (−) operators, so that you can write such expressions as −7 or +5. Cast operators have higher precedence than other unary operators, such as unary + and unary −. This precedence is higher than that of the multiplicative operators *, /, and %, and lower than that of parentheses. We indicate the cast operator with the notation static_cast<type>() in our precedence charts.

# Formatting for Floating-Point Numbers

The formatting capabilities in Fig. 4.13 are discussed here briefly and explained in depth in Chapter 15, Stream Input/Output. The call to setprecision in line 79 (with an argument of 2) indicates that double variables are available should be printed with two digits of precision to the right of the decimal point (e.g., 92.37). This call is referred to as a parameterized stream manipulator (because of the 2 in parentheses). Programs that use these calls must contain the preprocessor directive (line 5)

```
#include <iomanip>
```