# EXAMPLE 2-6

Consider the following C++ integral expressions:

```
2 + 3 * 5
3 + x - y / 7
x + 2 * (y - z) + 18
```

In these expressions, x, y, and z are variables of type int.

# EXAMPLE 2-7

Consider the following C++ floating-point expressions:

```
12.8 * 17.5 - 34.50
x * 10.5 + y - 16.2
```

Here, x and y are variables of type double.

Evaluating an integral or a floating-point expression is straightforward. As before, when operators have the same precedence, the expression is evaluated from left to right. You can always use parentheses to group operands and operators to avoid confusion.

Next, we discuss mixed expressions.

# Mixed Expressions

An expression that has operands of different data types is called a **mixed expression**. A mixed expression contains both integers and floating-point numbers. The following expressions are examples of mixed expressions:

```
2 + 3.5
6 / 4 + 3.9
5.4 * 2 - 13.6 + 18 / 2
```

In the first expression, the operand + has one integer operand and one floating-point operand. In the second expression, both operands for the operator / are integers, the first operand of + is the result of 6 / 4, and the second operand of + is a floating-point number. The third example is an even more complicated mix of integers and floating-point numbers. The obvious question is: How does C++ evaluate mixed expressions?

Two rules apply when evaluating a mixed expression:

+   1. When evaluating an operator in a mixed expression:
+      a. If the operator has the same types of operands (that is, either both integers or both floating-point numbers), the operator is evaluated according to the type of operands. Integer operand thus yield