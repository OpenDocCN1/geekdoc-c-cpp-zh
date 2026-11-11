The truth table of OR operator is as follows

# || OPERATOR

| a | b | a \|\| b |
|---|---|---|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

The above table shows that if we impose the AND operator between any two conditions then the result of the final condition is true when either one condition is true or both the conditions are true.

# Example

```
((5 == 5) && (3 > 6)) // evaluates to false (true && false).
((5 == 5) || (3 > 6)) // evaluates to true (true || false).
```

The following table shows the operator precedence and associativity of logical operators in C language.

| Operator | Associativity |
|---|---|
| && | Right to left |
| \|\| | Left to right |

# CONDITIONAL OPERATOR

C language provides a conditional operator (?:) which is intimately related to the If/else structure. The conditional operator is C's only ternary operator—it takes three operands. The operands together with the conditional operator build a conditional expression. The first operand is a condition and the second represents the value of the entire conditional expression if the condition is true and the third operand is the value for the entire conditional expression if the condition is false.

The general syntax of conditional operator is as follows:

Condition? result1 : result2

If condition is true the expression will return result1, if it is not it will return result2.

# Example 1

```
x = (y<25)? 9: 10;
```

This means, if (y<25), then x = 9 else x = 10;

# Example 2

7==5+2? 4: 3 // returns 3, since 7 is not equal to 5.

# Example 3

(a>b)? printf ("a is greater than b \n"); printf ("b is greater than a \n");

If a is greater than b, then first printf statement is executed else second printf statement is executed.

# Example 4

7==5+2? 4 : 3 // returns 4, since 7 is equal to 5+2.

# Example 5

5>3? a : b // returns the value of a, because 5 is greater than 3.

# Programming Problem

The following program represents the concept of conditional operator.

| Program | Output |
|---|---|
| ```c
// conditional operator
#include<stdio.h>
#include<conio.h>
void main()
{
    int a,b,c;
    clrscr();
    a=2;
    b=7;
    c=(a>b)? a : b;
    printf("\n The value of c is %d",c);
    getch();
}
``` | 7 |

In this example a was 2 and b was 7, so the expression being evaluated (a>b) was not true, thus the first value specified after the question mark was discarded in favor of the second value (the one after the colon) which was b, with a value of 7.

# BITWISE OPERATORS

When you learn to program in a high-level language like C (although C is fairly low-level, as high-level languages go), the idea is to avoid worrying too much about the hardware. You want the power to present mathematical abstractions, such as sets, etc. and have high-