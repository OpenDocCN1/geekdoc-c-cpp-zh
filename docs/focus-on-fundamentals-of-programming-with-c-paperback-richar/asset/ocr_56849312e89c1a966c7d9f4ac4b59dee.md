# Conditional Operator

The conditional operator, ?:, is the only ternary operator in C, i.e. requires 3 operands:

+   - the expression being tested
+   - the two alternative outcome expressions

Here's what the syntax of the conditional operator looks like:

```
// conditional1.c
condition ? expr1 : expr2;
```

The condition is a relational expression returning true or false (0 or non-zero). If true, then expr1 is evaluated, otherwise expr2 is evaluated. In fact, the conditional operator behaves very much like an if-else statement. The following code:

```
// conditional2.c
if (x > y) {
    max = x;
} else {
    max = y;
}
```

can be rewritten using the conditional operator:

```
// conditional3.c
max = x > y ? x : y;
```