
```c
if (a == 0 && b == 0) {
    printf("Both integers are zero\n");
    return 1;
}
```

*Intelligent use of return value*

A compound expression can include more than one logical operator. The following expression evaluates to true when all of the relational expressions also evaluate to true:

```c
a <= 0 && b <= 0 && c <= 0
```

Compound expressions like the one above are useful only when we don’t want to know the precise reason of failure; it’s either a, b or c, that’s all we care to know. Sometimes, you may need to make separate decisions for each of three possible outcomes. In that case, you need to use a separate if statement with each expression.

### 6.16.2 The ! Operator

The next logical operator we examine is the unary ! representing the NOT operation. This operator negates the logical value of its operand. True becomes false and vice versa as is the case with the NOT gate (Fig. 3.4). For instance, the two expressions on the following lines negate each other:

```
!(a > 0)        a > 0
!(b == 1)       b == 1
```

The ! has a higher precedence than the relational and logical operators (Table 6.2). Without the parentheses, !a would represent the logical negation of a.

Table 6.5 presents some constructs that use the ! alongside their equivalent constructs that don’t use it. The expression !(a > 0) signifies “a not greater than 0”, which is the same as (a <= 0). Normally, an expression without the ! is easier to read than one with it, so you should avoid using it to the extent you can.

**TABLE 6.5**  Use of Relational Operators with and without !

| With Logical ! | Without Logical ! |
|---|---|
| `if (!(a > 0))` | `if (a <= 0)` |
| `if (!(a >= 1))` | `if (a < 1)` |
| `while (!(a == 0))` | `while (a != 0)` |
| `if (a !> 0)` | Error; !> is an invalid operator |
| `if (!a == 1)` | Not an error; but not what you meant |

## 6.17 THE CONDITIONAL OPERATOR

C supports the only ternary operator—the *conditional operator*—which uses the symbols ? and :. These two symbols are used with three expressions to implement a rudimentary form of decision making. The operator uses the following formal syntax:

```
exp1 ? exp2 : exp3
```

*Entire line is an expression*

`exp1`, `exp2` and `exp3` represent three expressions, where `exp1` is generally a relational one. The composite expression evaluates to `exp2` if `exp1` evaluates to true, or `exp3` otherwise. Here’s how you can use this operator to make a simple decision:

```c
rate = total > 1000 ? 0.95 : 0.90;
```

If total is greater than 1000, then 0.95 is assigned to rate, otherwise 0.90 is assigned. Nothing could be simpler than that!

The ternary conditional operator has a very low precedence—just above the assignment operators. It has R-L associativity. This operator is taken up again in Section 7.14 for displaying messages using the expression property of `printf`.

## 6.18 `binary_outcomes.c`: RELATIONAL, LOGICAL AND CONDITIONAL OPERATORS AT WORK

Program 6.7 demonstrates the use of the operators that evaluate expressions to logical values. It accepts three integers as user input, and in the first two parts, conducts relational and logical tests on them. The final part features the conditional operator which uses the `printf` function as two operands. The program is invoked twice and the output is shown side by side.

The first two sections feature the `>`, `<` and `==` relational operators along with the `&&` and `||` logical operators. Observe that the expressions evaluate to either 0 or 1.

The third section uses the ternary operator `?` in two ways. In the first invocation, `i4` is assigned either of two values (50 or 100) depending on the outcome of the expression `i1 > i2`. The same relation is used in the second invocation simply to evaluate two `printf` expressions. Note that both the side effect and return value of `printf` have been printed by another `printf`!

PROGRAM 6.7: **binary_outcomes.c**

```c
/* binary_outcomes.c: Uses operators that work with logical values. */
#include <stdio.h>

int main(void)
{
    int i1, i2, i3, i4;

    printf("Enter three integers: ");
    scanf("%d %d %d", &i1, &i2, &i3);

    /* 1. Relational Operators */
    printf("i1 = %d, i2 = %d, i3 = %d\n", i1, i2, i3);
    printf("i1 > i2 = %d\n", i1 > i2);
    printf("i2 < i3 = %d\n", i2 < i3);
    printf("i2 == i3 = %d\n", i2 == i3);

    /* 2. Logical Operators */
    printf("i1 > i2 && i2 == i3 = %d\n", i1 > i2 && i2 == i3);
    printf("i1 < i2 || i2 != i3 = %d\n", i1 < i2 || i2 != i3);

    /* 3. Conditional Operator */
    i4 = i1 > i2 ? 50 : 100;
    printf("i1 > i2 ? 50 : 100 -- has value %d\n", i4);
    printf("%d\n",
        i1 > i2 ? printf("Note i1 > i2\n") : printf("Note i1 <= i2\n"));
    return 0;
}
```

PROGRAM OUTPUT: **binary_outcomes.c**

| Input: 7 3 3 | Input: 5 7 9 |
|---|---|
| Enter three integers: 7 3 3<br>i1 = 7, i2 = 3, i3 = 3<br>i1 > i2 = 1<br>i2 < i3 = 0<br>i2 == i3 = 1<br>i1 > i2 && i2 == i3 = 1<br>i1 < i2 || i2 != i3 = 0<br>i1 > i2 ? 50 : 100 -- has value 50<br>Note i1 > i2<br>13 | Enter three integers: 5 7 9<br>i1 = 5, i2 = 7, i3 = 9<br>i1 > i2 = 0<br>i2 < i3 = 1<br>i2 == i3 = 0<br>i1 > i2 && i2 == i3 = 0<br>i1 < i2 || i2 != i3 = 1<br>i1 > i2 ? 50 : 100 -- has value 100<br>Note i1 <= i2<br>14 |

## 6.19 OTHER OPERATORS

We have completed our examination of the operators belonging to the well-defined families (arithmetic, relational and logical). Another family, comprising the bitwise operators, are discussed in Chapter 17. Before we draw the curtains on this chapter, let’s examine two more operators, one of which has been used before and is included here for completeness.

### 6.19.1 The Comma (,) Operator

The comma (,) is a binary operator that evaluates two or more expressions from left to right and returns the value of the right-most expression. The syntax is shown below:

```
exp1, exp2
exp1, exp2, exp3, ...
```

The comma operator used here is different from the comma separator used to delimit variable declarations or argument lists of functions. Here, the comma operates on `exp1`, `exp2`, and so forth, and discards every expression in the list except the last one. So, the following expression

```c
a = 3, b = 5
```

evaluates to 5. The evaluated value may be assigned to a variable in which case the parentheses are needed to override the low precedence of the comma (Table 6.2). As the following examples indicate, without parentheses, x would be assigned the first item in the list:

- `x = (3, 5);` — *x is 5*
- `x = 3, 5, 7;` — *x is 3—Wrong*
- `x = (3, 5, printf("Hello\n"))` — *x is 6; side effect prints message*

Like with the **goto** keyword, there is skepticism about the utility of this operator because C can do without it. However, the comma is useful in at least one situation where one of the expressions produces a side effect. Consider the following code that sums all integers input from the keyboard until 0 is input:

```c
while (scanf("%d", &x), x > 0)
    sum += x;
printf("Sum: %d\n", sum);
```

Loop terminates when x is 0

Statement outside the loop

The control expression used by **while** contains a comma-operated expression. Every time the loop iterates, the comma discards the return value of **scanf**, but the side effect of **scanf** reads the next integer from the keyboard. The loop terminates when the expression x > 0 (the right-most expression) becomes false.

### 6.19.2 The sizeof Operator

As we have seen on numerous occasions, this unary operator works at compile time to evaluate the size in bytes of any data type or expression. There are two possible syntaxes for this operator:

```c
sizeof(data type)
sizeof expression
```

Parentheses optional here

Table 6.6 shows the typical values obtained when **sizeof** is used with various data types and expressions. The last two entries need to be studied carefully. Because **sizeof** has a higher precedence than the arithmetic operators, parentheses are needed to allow the evaluation of 3.142 * 4 (a double) to take place first.

**sizeof** is very useful in situations where you want a chunk of memory to be allocated, say, for 20 integers of type int. Rather than assume 4 as the size of int and ask for 80 bytes, you can make your program portable by asking for 20 * sizeof(int) bytes instead. You’ll encounter **sizeof** in Chapter 16 when dynamically allocating memory using the **malloc** and **calloc** functions.

**TABLE 6.6** Determining Size of Data Types and Expressions with **sizeof**

| Statement | Prints | Remarks |
|---|---:|---|
| `printf("%d\n", sizeof(int));` | 4 | |
| `printf("%d\n", sizeof(float));` | 8 | |
| `printf("%d\n", sizeof 3.142);` | 8 | Real constant stored as double |
| `printf("%d\n", sizeof 'A');` | 4 | Character constant stored as int |
| `printf("%d\n", sizeof "Kitkat");` | 7 | Counts NUL character also |
| `printf("%d\n", sizeof 3.142 * 4);` | 32 | Wrong, parentheses needed even ... |
| `printf("%d\n", sizeof (3.142 * 4));` | 8 | ... though operand is an expression |
