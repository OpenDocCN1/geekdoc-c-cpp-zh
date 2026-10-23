*operations.* We give a short introduction to these topics in order to prepare for more advanced topics and applications in later chapters.

In general, a conversion may occur in an expression where a value of a different type is expected, for example:

+   - **A1:** In the assignment operator; the value of the right-hand operand is converted to the unqualified type of the left-hand operand.
+   - **A2:** Scalar initialisation; the value of the initialiser expression is converted to the unqualified type of the left-hand operand.
+   - **A3:** Calling a function with argument types different from those in the function prototype declaration.
+   - **A4:** The value of the operand in a function’s return statement is converted to an object having the return type of the function.

Some simple code to show what we mean by these examples is:

```
double func(double d)
{
    return d*d;
}

double func()
{  // Return type (an int) convert to double

    int result = 1'000'000;
    return result;
}

void ImplicitConversions()
{  // Simple examples of conversions

    // Assignment
    int i = 1L;                       // Convert long to int
    int j = 3.14;                     // Truncate a double

    // Scalar initialisation
    double d2 = 2.4;
    int i2 = 3;
    double d3 = i2*d2;

    // Function call expression
    int i3 = 5;
    std::cout << func(i3) << '\n';

    // Function return type
    int i4 = func(3.14);
    std::cout << i4 << '\n';

    std::cout << func() << '\n';
}
```