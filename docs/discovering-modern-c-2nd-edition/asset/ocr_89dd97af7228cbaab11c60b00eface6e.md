+   - An `int` is implicitly convertible to a `rational`;
+   - Values are always stored in normalized way:
+     - The denominator is always positive and
+     - Numerator and denominator are coprime.
+   - The basic operations are implemented:
+     - Addition;
+     - Subtraction;
+     - Multiplication; and
+     - Division.
+   
+   The result of each operation is normalized.
+   
+   - A compound operation (like +=) is provided for each basic one; and
+   - An output operator for `ostream` is realized.
+   
+   Further functionality is optional.

# ## 2.8.3 Move Assignment

Write a move assignment operator for the polynomial in Exercise 2.8.1. Define the copy constructor as `default`. To test whether your assignment is used write a function `polynomial f(double c2, double c1, double c0)` that takes three coefficients and returns a polynomial. Print out a message in your move assignment or use a debugger to make sure your assignment is used.

# ## 2.8.4 Initializer List

Expand the program from Exercise 2.8.1 with a constructor and an assignment operator for an initializer list. The degree of the polynomial should be the length of the initializer list minus 1 afterward.

# ## 2.8.5 Resource Rescue