User-defined functions in C++ are classified into two categories:

+   - **Value-returning functions**—functions that have a return type. These functions return a value of a specific data type using the `return` statement, which we will explain shortly. Note that the function `main` has used a `return` statement to return the value 0 in every program we’ve seen so far.
+   - **Void functions**—functions that do not have a return type. These functions *do not* use a `return` statement to return a value.

We will first discuss value-returning functions. Many of the concepts discussed in regard to value-returning functions also apply to void functions.

# Value-Returning Functions

The previous section introduced some predefined C++ functions, such as `pow`, `abs`, `islower`, and `toupper`. These are examples of value-returning functions. To use these functions in your programs, you must know the name of the header file that contains the functions’ specification. You need to include this header file in your program using the include statement and know the following items:

+   1. The name of the function
+   2. The **parameters**, if any
+   3. The data type of each parameter
+   4. The data type of the value computed (that is, the value returned) by the function, called the type of the function

Because a value-returning function returns only one value, the natural thing for you to do is to use the value in one of three ways:

+   - Save the value for further calculation. For example, `x = pow(3.0, 2.5);`
+   - Use the value in some calculation. For example, `area = PI * pow(radius, 2.0);` or
+   - Print the value. For example, `cout << abs(-5) << endl;`

This suggests that a value-returning function is used

+   - In an assignment statement.
+   - As a parameter in a function call.
+   - In an output statement.

That is, a value-returning function is used (called) in an expression. Before we look at the syntax of a user-defined, value-returning function, let us consider the things associated with such functions. In addition to the four properties described previously, one more thing is associated with functions (both value-returning and void):