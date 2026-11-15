| Precedence | Operator | Associativity |
|---|---|---|
| 1 | Parentheses: ( ) | Innermost first |
| 2 | Unary operators: + - (type) | Right to left |
| 3 | Binary operators: * / % | Left to right |
| 4 | Binary operators: + - | Left to right |

Because multiplication and division have the same precedence level, and because the associativity (the order for grouping the operations) is from left to right, this expression will be evaluated as if it contained the following:

```
(a*b) + ((b/c)*d)
```

The precedence order does not specify whether a*b is evaluated before (b/c)*d; the order of evaluation of these terms is system-dependent (but does not affect the final value).

The spacing within an arithmetic expression is a style issue. Some people prefer to put spaces around each operator. We prefer to put spaces only around binary addition and subtraction, because they are evaluated last. Choose the spacing style that you prefer, but then use it consistently.

Assume that we want to compute the area of a trapezoid and that we have declared four double variables: base, height_1, height_2, and area. Assume further that the variables base, height_1 and height_2 already have values. A statement to correctly compute the area of the trapezoid is

```
area = 0.5*base*(height_1 + height_2);
```

Suppose that we omitted the parentheses in the expression:

```
area = 0.5*base*height_1 + height_2;
```

The statement would be executed as if it were this statement:

```
area = ((0.5*base)*height_1) + height_2;
```

Note that although an incorrect answer has been computed, there is no error message to alert us to the error. Therefore, it is important to be very careful when converting expressions into C. In general, use parentheses to indicate the order of operations in a complicated expression; this will avoid confusion and make sure that the expression is evaluated in the desired manner.

You may have noticed that there is no operator for exponentiation to compute values such as x^4. A special mathematical function will be discussed later in this chapter to perform exponentiations. Of course, exponentiations with integer exponents, such as a^2, can be computed with repeated multiplications.

The evaluation of long expressions should be broken into several statements. For example, consider the following equation:

```
f = \frac{x^3 - 2x^2 + x - 6.3}{x^2 + 0.05005x - 3.14}
```