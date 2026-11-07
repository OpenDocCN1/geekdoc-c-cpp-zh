**NOTE** You should be careful when evaluating the mod operator with negative integer operands. You might not get the answer you expect. For example, −34 % 5 = −4, because in the division −34 / 5, the quotient is −6 and the remainder is −4. Similarly, 34 % −5 = 4, because in the division 34 / −5, the quotient is −6 and the remainder is 4. Also −34 % −5 = −4, because in the division −34 / −5, the quotient is 6 and the remainder is −4.

# ## Expressions

There are three types of arithmetic expressions in C++:

+   - **Integral expressions**—all operands in the expression are integers. An integral expression yields an integral result.
+   - **Floating-point (decimal) expressions**—all operands in the expression are floating-points (decimal numbers). A floating-point expression yields a floating-point result.
+   - **Mixed expressions**—the expression contains both integers and decimal numbers.

Looking at some examples will help clarify these definitions.

# ### EXAMPLE 2-6

Consider the following C++ integral expressions:

```
2 + 3 * 5
3 + x − y / 7
x + 2 * (y − z) + 18
```

In these expressions, x, y, and z are variables of type `int`.

# ### EXAMPLE 2-7

Consider the following C++ floating-point expressions:

```
12.8 * 17.5 − 34.50
x * 10.5 + y − 16.2
```

Here, x and y are variables of type `double`.