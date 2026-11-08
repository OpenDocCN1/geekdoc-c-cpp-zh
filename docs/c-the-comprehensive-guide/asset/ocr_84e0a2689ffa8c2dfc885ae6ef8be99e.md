![](bbox=[0.143, 0.1, 0.543, 0.183])

**Figure 4.1** All subexpressions in one expression.

In **Listing 4.1** and **Listing 4.2**, you will find all kinds of expressions, of which I can only list a few here:

+   - `100` is a *number literal*—a number that is written directly into the source code.
+   - `"Divisors of "` is a *text literal*—a text directly in the source code.
+   - `std::cout << "Divisors of "` is an expression that outputs to the screen (or writes to a file).
+   - `value % divider` calculates the remainder of the division `value / divider`.
+   - `value % divider == 0` checks whether this remainder was 0, and therefore divider is a divisor of value.
+   - `0` as part of `return 0;` is an expression that “calculates” the return of `main()`.

In a few places, we have something other than an expression, and I will briefly discuss this here. `int value = 100` is not an expression, but a *declaration* (`int value`) with an *initialization* (`= 100`). However, the initialization to the right of `=` must be an expression. `Return 0` is also not an expression, but a *statement*. It consists of the special word (*keyword*) `return` and, in this case, the expression `0`.

One of the main characteristics of expressions is that each one has a well-defined *type*, and this also applies to each subexpression. Because types are very important in C++, understanding the types of expressions is also an important step toward success with C++.

# More about Statements and Expressions

Because statements and expressions are such elementary language elements, we dedicate a later chapter to them (**Chapter 8**). Here you have been given an initial introduction and an overview.

# 4.2.8  Allocations

One of the most important expressions in C++ is the *assignment*. I did not mention assignment in the list of statements. That was not an oversight.