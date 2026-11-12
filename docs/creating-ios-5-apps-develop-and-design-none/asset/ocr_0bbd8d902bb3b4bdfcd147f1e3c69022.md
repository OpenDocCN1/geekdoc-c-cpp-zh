operands with that value, forming a new expression. This is then evaluated until we reduce the expression to a single value.

```
```text
5 + 6 / 3 * (2 + 5)   // Initial expression.
5 + 6 / 3 * 7         // Operand in parentheses evaluated first.
5 + 2 * 7             // When two operators have the same precedence,
                      // evaluate from left to right.
5 + 14                // Perform multiplication before addition.
19                    // Final value.
```
```

Here are a couple of rules of thumb: Any expressions inside a function’s or method’s arguments are evaluated before the function call or method call is performed. Similarly, any expression inside an array’s subscript is performed before looking up the value. Function calls, method calls, and array indexing all occur before most other operators. Assignment occurs after most (but not all) other operators. Some examples are given here:

```
```text
a = 2 * max(2 + 5, 3);    // max() returns the largest value among its
                           // arguments. Variable a is set to 14.
a[2 + 3] = (6 + 3) * (10 - 7); // The value at index 5 is set to 27.
a = ((1 + 2) * (3 + 4)) > ((5 + 6) * (7 + 8)); // Variable a is set
                                                // to false.
```
```

# FUNCTIONS

Functions are the primary procedural workhorse for the C programming language. A C program largely consists of defining data structures and then writing functions to manipulate those structures.

We will typically use functions in conjunction with structs, especially when dealing with the lower-level frameworks. However, you will find some functions that are explicitly designed to work with Objective-C objects. In fact, we saw a function like this in Chapter 1: UIApplicationMain().

Unlike operators, functions can be defined by the programmer. This allows us to encapsulate a series of procedural steps so that those steps can be easily repeated.