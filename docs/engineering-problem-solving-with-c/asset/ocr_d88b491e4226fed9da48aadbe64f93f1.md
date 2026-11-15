is equivalent to the execution of this pair of statements:

```
x = x + 1;
w = x - y;
```

Similarly, the statement

```
w = x++ - y;
```

is equivalent to the pair of statements

```
w = x - y;
x = x + 1;
```

When executing either Equation (2.1) or Equation (2.2), if we assume that the value of x is equal to 5 and the value of y is equal to 3, then the value of x increases to 6. However, after executing Equation (2.1), the value of w is 3, but after executing Equation (2.2), the value of w is 2.

The increment and decrement operators have the same precedence as the other unary operators. If several unary operators are in an expression, they are associated from right to left. When using postfix notation, the value of the object will be incremented by the time the end of the statement is reached. Exactly when the increment occurs is system dependent. For this reason, the value of the object being modified is not definite from the point at which the postfix operator is applied to the end of the statement.

![](bbox=[0.12, 0.4, 0.2, 0.48])

# Abbreviated Assignment Operators

C++ allows simple assignment statements to be abbreviated. For example, each of the following pair of statements contains equivalent statements:

| Abbreviated Assignment Operator | Equivalent Statement |
| :--- | :--- |
| `x += 3;` | `x = x + 3;` |
| `sum += x;` | `sum = sum + x;` |
| `d /= 4.5;` | `d = d / 4.5;` |
| `r %= 2;` | `r = r % 2;` |

In fact, any statement of the form

```
identifier = identifier operator expression;
```

can be written in the form

```
identifier operator = expression;
```

Earlier in this section, we used the following multiple-assignment statement:

```
x = y = z = 0;
```

The interpretation of this statement is clear, but the interpretation of the following statement is not as evident:

```
a = b += c + d;
```

multiple-assignment