# More on True/False Values

You've seen that C's relational expressions evaluate to 0 to represent false and to 1 to represent true. It's important to be aware, however, that any numeric value is interpreted as either true or false when it is used in a C expression or statement that is expecting a logical value (that is, a true or false value). The rules for this are as follows:

+   - A value of zero represents false.
- Any nonzero value represents true.

This is illustrated by the following example, in which the value of x is printed:

```
x = 125;
if (x)
    printf("%d", x);
```

Because x has a nonzero value, the if interprets the expression (x) as true. You can further generalize this because, for any C expression, writing

```
(expression)
```

is equivalent to writing

```
expression != 0
```

Both evaluate to true if expression is nonzero and to false if expression is 0. Using the (!) operator, you can also write

```
(expression == 0)
```

which is equivalent to

# Precedence of Operators

As you might have guessed, C's logical operators also have a precedence order, among themselves and in relation to other operators. The ! operator has a precedence equal to the unary mathematical operators ++ and --. Thus, ! has a higher precedence than all the relational operators and all the binary mathematical operators.

In contrast, the && and || operators have much lower precedence, lower than all the mathematical and relational operators, although && has a higher precedence than ||. As with all C's operators, you can use parentheses to modify the evaluation order when using the logical operators. Consider the following example:

You want to write a logical expression that makes three individual comparisons: