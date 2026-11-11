
Some examples of the usage of logical expressions are:

- `if (age > 55 && salary < 1000)`
- `if (number < 0 || number > 100)`

We shall see more of them when we discuss decision statements.

**Table 5.3** *Truth Table*

| op-1 | op-2 | Value of the expression: `op-1 && op-2` | Value of the expression: `op-1 \|\| op-2` |
|---|---|---|---|
| Non-zero | Non-zero | 1 | 1 |
| Non-zero | 0 | 0 | 1 |
| 0 | Non-zero | 0 | 1 |
| 0 | 0 | 0 | 0 |

> **Note** *Relative precedence of the relational and logical operators is as follows:*
>
> Highest `!`  
> `>` `>=` `<` `<=`  
> `==` `!=`  
> `&&`  
> Lowest `||`
>
> *It is important to remember this when we use these operators in compound expressions.*

## 5.5 ASSIGNMENT OPERATORS

![](img/11b034a94fc590add0a7808250a38792_167_0.png)

Assignment operators are used to assign the result of an expression to a variable. We have seen the usual assignment operator, `=`. In addition, C has a set of ‘shorthand’ assignment operators of the form

```
v op= exp;
```

Where *v* is a variable, *exp* is an expression and *op* is a C binary arithmetic operator. The operator `op=` is known as the shorthand assignment operator.

The assignment statement

```
v op= exp;
```

is equivalent to

```
v = v op (exp);
```

with *v* evaluated only once. Consider an example

```
x += y+1;
```

This is same as the statement

```
x = x + (y+1);
```

The shorthand operator `+=` means ‘add y+1 to x’ or ‘increment x by y+1’. For y = 2, the above statement becomes

```
x += 3;
```

and when this statement is executed, 3 is added to x. If the old value of x is, say 5, then the new value of x is 8. Some of the commonly used shorthand assignment operators are illustrated in Table 5.4.

### Rules for ++ and -- Operators

- Increment and decrement operators are unary operators and they require variable as their operands.
- When postfix ++ (or --) is used with a variable in an expression, the expression is evaluated first using the original value of the variable and then the variable is incremented (or decremented) by one.
- When prefix ++(or --) is used in an expression, the variable is incremented (or decremented) first and then the expression is evaluated using the new value of the variable.
- The precedence and associativity of ++ and -- operators are the same as those of unary + and unary -.

## 5.7 CONDITIONAL OPERATOR

LO 5.1

A ternary operator pair "?:" is available in C to construct conditional expressions of the form

```
exp1 ? exp2 : exp3
```

where `exp1`, `exp2`, and `exp3` are expressions.

The operator `? :` works as follows: `exp1` is evaluated first. If it is nonzero (true), then the expression `exp2` is evaluated and becomes the value of the expression. If `exp1` is false, `exp3` is evaluated and its value becomes the value of the expression. Note that only one of the expressions (either `exp2` or `exp3`) is evaluated. For example, consider the following statements:

```
a = 10;
b = 15;
x = (a > b) ? a : b;
```

In this example, x will be assigned the value of b. This can be achieved using the if-else statements as follows:

```
if (a > b)
    x = a;
else
    x = b;
```

## 5.8 BITWISE OPERATORS

LO 5.2

C has a distinction of supporting special operators known as *bitwise operators* for manipulation of data at bit level. These operators are used for testing the bits, or shifting them right or left. Bitwise operators may not be applied to *float* or *double*. Table 5.5 lists the bitwise operators and their meanings.

*Table 5.5 Bitwise Operators*

| Operator | Meaning |
|---|---|
| & | bitwise AND |
| \| | bitwise OR |
| ^ | bitwise exclusive OR |
| << | shift left |
| >> | shift right |

## 5.9 SPECIAL OPERATORS

![](img/11b034a94fc590add0a7808250a38792_171_0.png)

C supports some special operators of interest such as comma operator, sizeof operator, pointer operators (& and *) and member selection operators (. and ->). The comma and sizeof operators are discussed in this section while the pointer operators are discussed in Chapter 13. Member selection operators which are used to select members of a structure are discussed in Chapters 12 and 13. ANSI committee has introduced two preprocessor operators known as “string-izing” and “token-pasting” operators (# and ##).

### 5.9.1 The Comma Operator

The comma operator can be used to link the related expressions together. A comma-linked list of expressions are evaluated left to right and the value of right-most expression is the value of the combined expression. For example, the statement

```
value = (x = 10, y = 5, x+y);
```

first assigns the value 10 to x, then assigns 5 to y, and finally assigns 15 (i.e. 10 + 5) to value. Since comma operator has the lowest precedence of all operators, the parentheses are necessary. Some applications of comma operator are:

- In `for` loops: `for (n = 1, m = 10; n <= m; n++, m++)`
- In `while` loops: `while (c = getchar(), c != '\n')`
- Exchanging values: `t = x, x = y, y = t;`

### 5.9.2 The sizeof Operator

The sizeof is a compile time operator and, when used with an operand, it returns the number of bytes the operand occupies. The operand may be a variable, a constant or a data type qualifier. Examples:

```
m = sizeof (sum);
n = sizeof (long int);
k = sizeof (235L);
```

The sizeof operator is normally used to determine the lengths of arrays and structures when their sizes are not known to the programmer. It is also used to allocate memory space dynamically to variables during execution of a program.

### WORKED-OUT PROBLEM 5.3

In Fig. 5.3, the program employs different kinds of operators. The results of their evaluation are also shown for comparison.

Notice the way the increment operator ++ works when used in an expression. In the statement

```
c = ++a - b;
```

new value of a (= 16) is used thus giving the value 6 to c. That is, a is incremented by 1 before it is used in the expression. However, in the statement

```
d = b++ + a;
```

the old value of b (=10) is used in the expression. Here, b is incremented by 1 after it is used in the expression.

We can print the character % by placing it immediately after another % character in the control string. This is illustrated by the statement

```
printf("a%%b = %d\n", a%b);
```

The program also illustrates that the expression

```
c > d ? 1 : 0
```

assumes the value 0 when c is less than d and 1 when c is greater than d.

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
    printf("a%%b = %d\n", a%b);
    printf("a *= b = %d\n", a*=b);
    printf("%d\n", (c>d) ? 1 : 0);
    printf("%d\n", (c<d) ? 1 : 0);
}

Output

a = 16 b = 10 c = 6
a = 16 b = 11 d = 26
a/b = 1
a%b = 5
a *= b = 176
0
1
```

*Fig. 5.3 Further illustration of arithmetic operators*

## 5.10 ARITHMETIC EXPRESSIONS

An arithmetic expression is a combination of variables, constants, and operators arranged as per the syntax of the language. We have used a number of simple expressions in the examples discussed so far. C can handle any complex mathematical expressions. Some of the examples of C expressions are shown in Table 5.6. Remember that C does not have an operator for exponentiation.

**Table 5.6** *Expressions*

| Algebraic expression | C expression |
| --- | --- |
| a × b - c | a * b - c |
| (m+n) (x+y) | (m+n) * (x+y) |
| (ab/c) | a * b/c |
| 3x² + 2x + 1 | 3 * x * x + 2 * x + 1 |
| (x/y) + c | x/y + c |

## 5.11 EVALUATION OF EXPRESSIONS

Expressions are evaluated using an assignment statement of the form:

*variable = expression;*

Variable is any valid C variable name. When the statement is encountered, the expression is evaluated first and the result then replaces the previous value of the variable on the left-hand side. All variables used in the expression must be assigned values before evaluation is attempted. Examples of evaluation statements are

```
x = a * b - c;
y = b / c * a;
z = a - b / c + d;
```

The blank space around an operator is optional and adds only to improve readability. When these statements are used in a program, the variables a, b, c, and d must be defined before they are used in the expressions.

### WORKED-OUT PROBLEM 5.4

The program in Fig. 5.4 illustrates the use of variables in expressions and their evaluation.

Output of the program also illustrates the effect of presence of parentheses in expressions. This is discussed in the next section.

```
Program

main()
{
    float a, b, c, x, y, z;
    a = 9;
    b = 12;
    c = 3;
```
