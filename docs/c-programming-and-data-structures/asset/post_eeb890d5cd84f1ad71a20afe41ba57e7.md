
In while loops:

```
while (c = getchar(), c != '\n')
```

Exchanging values:

```
t = x, x = y, y = t;
```

## 1.52.2 The sizeof Operator

The `sizeof` is a compile-time operator and, when used with an operand, it returns the number of bytes the operand occupies. The operand may be a variable, a constant or a data type qualifier.

Examples:

```
m = sizeof(sum);
n = sizeof(long int);
k = sizeof(235L);
```

The `sizeof` operator is normally used to determine the lengths of arrays and structures when their sizes are not known to the programmer. It is also used to allocate memory space dynamically to variables during execution of a program.

**EXAMPLE 1.36** In Fig. 1.89, the program employs different kinds of operators. The results of their evaluation are also shown for comparison.

Notice the way the increment operator `++` works when used in an expression. In the statement

```
c = ++a - b;
```

The new value of a (= 16) is used thus giving the value 6 to c. That is, a is incremented by 1 before it is used in the expression. However, in the statement

```
d = b++ + a;
```

The old value of b (=10) is used in the expression. Here, b is incremented by 1 after it is used in the expression.

We can print the character % by placing it immediately after another % character in the control string. This is illustrated by the statement

```
printf("a%%b = %d\n", a*b);
```

The program also illustrates that the expression `c > d ? 1 : 0` assumes the value 0 when c is less than d and 1 when c is greater than d.

```
Program
main()
{
    int a, b, c, d;
    a = 15;
    b = 10;
    c = ++a - b;
    printf("a = %d b = %d c = %d\n", a, b, c);
    d = b++ + a;
    printf("a = %d b = %d d = %d\n", a, b, d);
    printf("a/b = %d\n", a/b);
    printf("a%%b = %d\n", a*b);
    printf("a * b = %d\n", a*b);
    printf("%d\n", (c > d) ? 1 : 0);
    printf("%d\n", (c < d) ? 1 : 0);
}
```

```
Output
a = 16  b = 10  c = 6
a = 16  b = 11  d = 26
a/b = 1
a%b = 5
a * b = 176
0
1
```

Fig. 1.89 Further illustration of arithmetic operators

## 1.53 ARITHMETIC EXPRESSIONS

An arithmetic expression is a combination of variables, constants, and operators arranged as per the syntax of the language. We have used a number of simple expressions in the examples discussed so far. C can handle any complex mathematical expressions. Some of the examples of C expressions are shown in Table 1.23. Remember that C does not have an operator for exponentiation.

Table 1.23 Expressions

| Algebraic expression | C expression |
|---|---|
| a × b - c | `a * b - c` |
| (m+n) × (x + y) | `(m+n) * (x + y)` |
| $\frac{ab}{c}$ | `a * b/c` |
| 3x² + 2x + 1 | `3 * x * x + 2 * x + 1` |
| $\left(\frac{x}{y}\right)+c$ | `x/y + c` |

## 1.54 EVALUATION OF EXPRESSIONS

Expressions are evaluated using an assignment statement of the form:

```
variable = expression;
```

Variable is any valid C variable name. When the statement is encountered, the expression is evaluated first and the result then replaces the previous value of the variable on the left-hand side. All variables used in the expression must be assigned values before evaluation is attempted.

Examples of evaluation statements are

```
x = a * b - c;
y = b / c * a;
z = a - b / c + d;
```

The blank space around an operator is optional and adds only to improve readability. When these statements are used in a program, the variables a, b, c, and d must be defined before they are used in the expressions.

**EXAMPLE 1.37** The program in Fig. 1.90 illustrates the use of variables in expressions and their evaluation. Output of the program also illustrates the effect of presence of parentheses in expressions. This is discussed in the next section.

```
Program
main()
{
    float a, b, c, x, y, z;
    a = 9;
    b = 12;
    c = 3;
    x = a - b / 3 + c * 2 - 1;
    y = a - b / (3 + c) * (2 - 1);
    z = a - (b / (3 + c) * 2) - 1;
    printf("x = %f\n", x);
    printf("y = %f\n", y);
    printf("z = %f\n", z);
}
```

```
Output
x = 10.000000
y = 7.000000
z = 4.000000
```

Fig. 1.90 Illustrations of evaluation of expressions

## 1.55 PRECEDENCE OF ARITHMETIC OPERATORS

An arithmetic expression without parentheses will be evaluated from left to right using the rules of precedence of operators. There are two distinct priority levels of arithmetic operators in C:

- High priority: `* / %`
- Low priority: `+ -`

The basic evaluation procedure includes 'two' left-to-right passes through the expression. During the first pass, the high priority operators (if any) are applied as they are encountered. During the second pass, the low priority operators (if any) are applied as they are encountered.

Consider the following evaluation statement

```
x = a - b/3 + c * 2 - 1
```

![](img/fe6da5f61b1e2c77309bbee135b45e35_120_0.png)

Fig. 1.91 Illustration of hierarchy of operations

When a = 9, b = 12, and c = 3, the statement becomes

```
x = 9 - 12/3 + 3 * 2 - 1
```

and is evaluated as follows:

First pass:

- Step 1: `x = 9 - 4 + 3 * 2 - 1`
- Step 2: `x = 9 - 4 + 6 - 1`

Second pass:

- Step 3: `x = 5 + 6 - 1`
- Step 4: `x = 11 - 1`
- Step 5: `x = 10`

These steps are illustrated in Fig. 1.91. The numbers inside parentheses refer to step numbers. However, the order of evaluation can be changed by introducing parentheses into an expression. Consider the same expression with parentheses as shown below:

```
9 - 12/(3 + 3) * (2 - 1)
```

### Rules for Evaluation of Expression

- First, parenthesized sub-expressions from left to right are evaluated.
- If parentheses are nested, the evaluation begins with the innermost sub-expression.
- The precedence rule is applied in determining the order of application of operators in evaluating sub-expressions.
- The associativity rule is applied when two or more operators of the same precedence level appear in a sub-expression.
- Arithmetic expressions are evaluated from left to right using the rules of precedence.
- When parentheses are used, the expressions within parentheses assume highest priority.

## 1.56 SOME COMPUTATIONAL PROBLEMS

When expressions include real values, then it is important to take necessary precautions to guard against certain computational errors. We know that the computer gives approximate values for real numbers and the errors due to such approximations may lead to serious problems. For example, consider the following statements:

```
a = 1.0/3.0;
b = a * 3.0;
```

We know that `(1.0/3.0) * 3.0` is equal to 1. But there is no guarantee that the value of b computed in a program will equal 1.

Another problem is division by zero. On most computers, any attempt to divide a number by zero will result in an abnormal termination of the program. In some cases such a division may produce meaningless results. Care should be taken to test the denominator that is likely to assume zero value and avoid any division by zero.

The third problem is to avoid overflow or underflow errors. It is our responsibility to guarantee that operands are of the correct type and range, and the result may not produce any overflow or underflow.

**EXAMPLE 1.38** Output of the program in Fig. 1.92 shows round-off errors that can occur in computation of floating point numbers.

```
Program
/*---------- Sum of n terms of 1/n ----------*/
main()
{
    float sum, n, term;
    int count = 1;
    sum = 0;
    printf("Enter value of n\n");
    scanf("%f", &n);
    term = 1.0/n;
    while( count <= n )
    {
        sum = sum + term;
        count++;
    }
    printf("Sum = %f\n", sum);
}
```

```
Output
Enter value of n
99
Sum = 1.000001
Enter value of n
143
Sum = 0.999999
```

Fig. 1.92 Round-off errors in floating point computations

We know that the sum of n terms of `1/n` is 1. However, due to errors in floating point representation, the result is not always 1.

## 1.57 TYPE CONVERSIONS IN EXPRESSIONS

### 1.57.1 Implicit Type Conversion

C permits mixing of constants and variables of different types in an expression. C automatically converts any intermediate values to the proper type so that the expression can be evaluated without losing any significance.

This automatic conversion is known as implicit type conversion.

During evaluation it adheres to very strict rules of type conversion. If the operands are of different types, the 'lower' type is automatically converted to the 'higher' type before the operation proceeds. The result is of the higher type. A typical type conversion process is illustrated in Fig. 1.93.

Given below is the sequence of rules that are applied while evaluating expressions.

- All `short` and `char` are automatically converted to `int`; then
  - 1. if one of the operands is `long double`, the other will be converted to `long double` and the result will be `long double`;
  - 2. else, if one of the operands is `double`, the other will be converted to `double` and the result will be `double`;
  - 3. else, if one of the operands is `float`, the other will be converted to `float` and the result will be `float`;
  - 4. else, if one of the operands is `unsigned long int`, the other will be converted to `unsigned long int` and the result will be `unsigned long int`;
  - 5. else, if one of the operands is `long int` and the other is `unsigned int`, then
    - (a) if `unsigned int` can be converted to `long int`, the `unsigned int` operand will be converted as such and the result will be `long int`;
    - (b) else, both operands will be converted to `unsigned long int` and the result will be `unsigned long int`;
  - 6. else, if one of the operands is `long int`, the other will be converted to `long int` and the result will be `long int`;
  - 7. else, if one of the operands is `unsigned int`, the other will be converted to `unsigned int` and the result will be `unsigned int`.

![](img/fe6da5f61b1e2c77309bbee135b45e35_123_0.png)

Fig. 1.93 Process of implicit type conversion
