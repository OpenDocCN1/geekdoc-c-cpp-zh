# LESSON 4 The Pieces of a C Program: Statements, Expressions, and Operators

# Input

LISTING 4.5 Relational.c: Evaluating Relational Expressions

```
1:   /* Demonstrates the evaluation of relational expressions */
2:
3:   #include <stdio.h>
4:
5:   int a;
6:
7:   int main()
8:{
9:     a = (5 == 5);               /* Evaluates to 1 */
10:    printf("\na (5 == 5)\na = %d", a);
11:
12:    a = (5 != 5);               /* Evaluates to 0 */
13:    printf("\na (5 != 5)\na = %d", a);
14:
15:    a = (12 == 12) + (5 != 1); /* Evaluates to 1 + 1 */
16:    printf("\na (12 == 12) + (5 != 1)\na = %d\n", a);
17:
    return 0;
18:}
```

# Output

a = (5 == 5)
a = 1
a = (5 != 5)
a = 0
a = (12 == 12) + (5 != 1)
a = 2

# Analysis

The output from this list might seem a little confusing at first. Remember, the most common mistake people make when using the relational operators is to use a single sign—the assignment operator—instead of a double equal sign. The following expression evaluates to 5 (and also assigns the value 5 to x):

x = 5

In contrast, the following expression evaluates to either 0 or 1 (depending on whether x is equal to 5) and doesn’t change the value of x:

x == 5

If by mistake you write

```
if (x = 5)
    printf("x is equal to 5");
```