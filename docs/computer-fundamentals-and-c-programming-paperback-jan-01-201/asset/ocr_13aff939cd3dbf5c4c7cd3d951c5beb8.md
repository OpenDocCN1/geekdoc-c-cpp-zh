**Note:** While integer division causes truncation of the fractional component, the truncated portion can be obtained by using the % operator. You then need two operations to get both quotient and remainder.

# 6.6 AUTOMATIC OR IMPLICIT TYPE CONVERSION

When numbers of different data types are used in an expression, the compiler converts a lower type to a higher type using the concept of *implicit promotion*. C finally converts the type of the expression itself to the highest type it finds there. Consider this simple expression that involves an assignment:

```
float pi = 22 / 7.0;
```

Here, the three variables and constants have three different data types. Recall that 7.0 has the type double and 22 is of type int (5.13.1). The compiler doesn’t think that the types are incompatible and proceeds with type conversion in the following sequence:

+   - It looks at the operands of the / operator and finds 7.0 to have a higher type than 22. It converts 22 to double as well, so the resultant expression also has the type double. This means that `sizeof(22 / 7.0) = sizeof(double)`.
+   - It then looks at the operand on the left of the =. This is a variable of type float, which has a lower type than double. But since C can’t change the type of a variable that has been declared with a specific type, it *demotes* the type of the entire expression on the right to float. This can sometimes lead to loss of information but it won’t happen here.

The preceding example featured a simple expression, but for complex expressions containing multiple data types, the compiler uses the following sequence for conversion:

+   1. All char and short operands are converted to int or unsigned int, if considered necessary.
+   2. For the remaining operands of every operator, if they have two different types, the lower type is converted to the higher type using the following sequence:
+   
+      `long double → double → long long → long → int`
+   
+      This means the compiler first looks for long double, and if it finds one, it converts its matching operand to long double. It repeats this exercise for the next lower type (double) and continues until all operands have been examined. The scanning cannot go beyond int because char and short have already been converted.
+   3. Eventually, the entire expression is converted to the highest type found. And if the expression is assigned to a variable, the type of the expression is changed to match the type on the left of the =. This can lead to either promotion or demotion (loss of information).

The term “conversion” is a misnomer because type changes are made only to the *copies* of the operands. Also, in the process of conversion, if the default (signed) type cannot hold the data even after promotion, then the unsigned type is chosen.