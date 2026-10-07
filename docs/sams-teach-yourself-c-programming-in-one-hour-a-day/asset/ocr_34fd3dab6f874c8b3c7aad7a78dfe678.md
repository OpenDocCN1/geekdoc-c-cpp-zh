# The Assignment Operator

The assignment operator is the equal sign (=). Its use in programming is somewhat
different from its use in regular math. If you write

```
x = y;
```

In a C program, it doesn't mean "x is equal to y." Instead, it means "Assign the value of
y to x." In a C assignment statement, the right side can be any expression, and the left
side must be a variable name. Thus, the form is as follows:

```
variable = expression;
```

When executed, expression is evaluated, and the resulting value is assigned to
variable.

# The Mathematical Operators

C's mathematical operators perform mathematical operations such as addition and
subtraction. C has two unary mathematical operators and five binary mathematical
operators.

# The Unary Mathematical Operators

The unary mathematical operators are named because they take a single operand. C
has two unary mathematical operators, which are listed in Table 4.1.

TABLE 4.1 C's Unary Mathematical Operators

| Operator | Symbol | Action | Examples |
| --- | --- | --- | --- |
| Increment | ++ | Increments the operand by one | ++x, x++ |
| Decrement | -- | Decrements the operand by one | -x, x-- |

The increment and decrement operators can be used only with variables, not
constants. The operation performed is to add one to or subtract one from the operand.
other words, the statements

```
++x;
--y;
```

are the equivalent of these statements:

```
x = x + 1;
y = y - 1;
```