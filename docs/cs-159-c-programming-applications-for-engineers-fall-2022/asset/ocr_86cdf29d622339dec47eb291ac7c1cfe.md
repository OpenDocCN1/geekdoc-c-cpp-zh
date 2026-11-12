What does it mean to be implicit? The computer does it without the programmer explicitly asking for the conversion to be done! The rules for implicit data type conversions are illustrated in the image above.

+   - Are there explicit data type conversions? And, if so, how is an explicit type conversion implemented?

Example requiring explicit type conversion: I want to calculate 3 / 2, but I need the answer to be 1.5!

We saw in the mixed type expression that the integer was promoted on the data type hierarchy to a float implicitly. We can request a type conversion explicitly on one of the two operands in the division expression forcing the division to involve a floating-point and an integer. The quotient will then be generated as a floating-point value because the expression is now a mixed type expression and the second operand (the denominator in the example below) is changed implicitly.

```
(float) 3 / 2 = 1.5
```

# Try the following:

| Expression | Evaluation |
|---|---|
| 3 / (float) 2 | |
| (float) 3 / (float) 2 | |
| (float) (3 / 2) | |

What do the results of the expressions above say about the precedence of the explicit type conversion?

# Another Math Review: Rounding of numbers is a common task in problem solving. You must keep in mind the rules regarding rounding as we program this semester or better yet be able to conduct various tests to identify how rounding is taking place with your values.

+   - Sometimes an “extreme” form of rounding takes place called truncation. Truncation is removing of the entire decimal value and giving no consideration to rounding of the integer that remains.
+   - The floor function (found in math.h, but also a commonly used function in MATLAB and Excel) will remove a remainder and reduce the number to the next smaller integer value. Note how its behavior is similar to that of the conversion of float to int.

| Expression | Evaluation | Expression | Evaluation |
|---|---|---|---|
| floor (6.99) | | (int) 6.99 | |
| floor (6.5) | | (int) 6.5 | |
| floor (6.0) | | (int) 6.0 | |
| floor (6.75 + 0.5) | | (int) (6.75 + 0.5) | |