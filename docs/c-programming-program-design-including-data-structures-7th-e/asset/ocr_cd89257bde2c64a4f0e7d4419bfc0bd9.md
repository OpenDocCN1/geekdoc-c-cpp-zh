Now, suppose that `num = 20`. Then:

| Expression | Evaluation | Explanation |
|---|---|---|
| `0 <= num <= 10` | `= 0 <= 20 <= 10` | |
| | `= (0 <= 20) <= 10` | (Because relational operators are evaluated from left to right) |
| | `= 1 <= 10` | (Because `0 <= 20` is **true**, `0 <= 20` evaluates to 1) |
| | `= 1` (**true**) | |

Now, you can see why the expression evaluates to **true** when `num` is 20. Similarly, if `num` is −10, the expression `0 <= num <= 10` evaluates to **true**. In fact, this expression will always evaluate to **true**, no matter what `num` is. This is due to the fact that the expression `0 <= num` evaluates to either 0 or 1, and `0 <= 10` is **true** and `1 <= 10` is **true**. So what is wrong with the expression `0 <= num <= 10`? It is missing the logical operator `&&`. A correct way to write this expression in C++ is:

```
0 <= num && num <= 10
```

Using the precedence of operators, the expression `0 <= num && num <= 10` is the same as `(0 <= num) && (num <= 10)`.

You must take care when formulating logical expressions. When creating a complex logical expression, you must use the proper logical operators.

# Avoiding Bugs by Avoiding Partially Understood Concepts and Techniques

The debugging sections in Chapters 2 and 3 illustrated how to understand and fix syntax and logic errors. In this section, we illustrate how to avoid bugs by avoiding partially understood concepts and techniques.

The programs that you have written until now should have illustrated that a small error such as the omission of a semicolon at the end of a variable declaration or using a variable without properly declaring it can prevent a program from successfully compiling. Similarly, using a variable without properly initializing it can prevent a program from running correctly. Recall that the condition associated with an `if` statement must be enclosed in parentheses. Therefore, the following expression will result in a syntax error:

```
if score >= 90
```

Example 4–12 illustrates that an unintended semicolon following the condition of the following `if` statement:

```
if (hours > 40.0);
```

can prevent successful compilation or correct execution.