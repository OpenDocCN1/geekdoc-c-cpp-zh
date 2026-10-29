# Counting

The **counting statement**, which is an assignment statement similar to the accumulating statement, has the following form:

```
variable = variable + fixedNumber;
```

Examples of counting statements are as follows:

```
i = i + 1;
n = n + 1;
count = count + 1;
j = j + 2;
m = m + 2;
kk = kk + 3;
```

In these examples, the same variable is used on both sides of the equals sign. After the statement is executed, the variable’s value is increased by a fixed amount. In the first three examples, the variables i, n, and count have been increased by 1. In the next two examples, the variables have been increased by 2, and in the final example, the variable kk has been increased by 3.

For a variable that’s increased or decreased by only 1, C++ provides two unary operators: increment and decrement operators. Using the **increment operator**, ++, the expression `variable = variable + 1` can be replaced by the expression `variable++` or the expression `++variable`. Here are examples of the increment operator:

| Expression | Alternative |
|---|---|
| `i = i + 1` | `i++` or `++i` |
| `n = n + 1` | `n++` or `++n` |
| `count = count + 1` | `count++` or `++count` |

Program 3.4 illustrates the use of the increment operator. It displays the following output:

```
The initial value of count is 0
    count is now 1
    count is now 2
    count is now 3
    count is now 4
```