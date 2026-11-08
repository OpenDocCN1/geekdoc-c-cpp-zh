What is the output of the following statements?

a. `cout << funcExp(sales, 7) << endl;`

b. `cout << funcExp(names, 6) << endl;`

+   31. Write the definition of the function template that swaps the contents of two variables.

+   32.
+   
+      a. Overload the operator `+` for the class `newString` to perform string concatenation. For example, if `s1` is "Hello" and `s2` is "there", the statement:
+   
+         `s3 = s1 + s2;`
+   
+         should assign "Hello there" to `s3`, in which `s1`, `s2`, and `s3` are `newString` objects.
+   
+      b. Overload the operator `+=` for the class `newString` to perform the following string concatenation. Suppose that `s1` is "Hello" and `s2` is "there". Then, the statement:
+   
+         `s1 += s2;`
+   
+         should assign "Hello there" to `s1`, in which `s1` and `s2` are `newString` objects.

# PROGRAMMING EXERCISES

+   1. This chapter uses the class `rectangleType` to illustrate how to overload the operators `+`, `*`, `==`, `!=`, `>`, `>>`, and `<<`. In this exercise, first redefine the class `rectangleType` so that the instance variables are protected and then overload additional operators as defined in parts a to c.

+   a. Overload the pre- and post-increment and decrement operators to increment and decrement, respectively, the length and width of a rectangle by one unit. (Note that after decrementing the length and width, they must be positive.)

+   b. Overload the binary operator `-` to subtract the dimensions of one rectangle from the corresponding dimensions of another rectangle. If the resulting dimensions are not positive, output an appropriate message and do not perform the operation.

+   c. The operators `==` and `!=` are overloaded by considering the lengths and widths of rectangles. Redefine the functions to overload the relational operator by considering the areas of rectangles as follows: Two rectangles are the same, if they have the same area; otherwise, the rectangles are not the same. Similarly, rectangle `yard1` is greater than rectangle `yard2` if the area of `yard1` is greater than the area of `yard2`. Overload the remaining relational operators using similar definitions.