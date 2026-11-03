# Example:

This is same as the statement, x=x+(y+1);

X+=y+1;

Statement with simple assignment operator    statement with shorthand operator

| Statement with simple assignment operator | statement with shorthand operator |
|---|---|
| A=a+1 | a+=1 |
| A=a-1 | a-=1 |
| A=a*(n+1) | a*=n+1 |
| A=a/(n+1) | a/=n+1 |
| A=a%b | a%=b |

The use of shorthand assignment operators has three advantages:

+   1. What appears on the left hand side need not be repeated. Therefore, it becomes easier to write.
+   2. The statement is more concise and easier to red.
+   3. The statement is more efficient.

(d) The ternary operator is also called as conditional operator.

Syntax:

```
Exp1?exp2:exp3;
```

Where exp1, exp2 and exp3 are expressions.

# Operation of Ternary Conditional Operator:

The value of exp1 is evaluated first. If it is true, value of exp2 is evaluated, otherwise exp3 is evaluated.

# Example:

```
Int a=5,b=10,c=15;
Y=(a>b)?b:c;
```

In the above statement, the expression a>b is evaluated. Since it is false, value of c will be assigned to y.

So, the value of y will be 15.

```
Y=(a<b)?b:c;
```

Here a<b is true so value of b is assignment to y.

So, value of y will be 100.

# Program:

```
/* Write a program to find the largest of three input numbers using ternary operator */
#include<stdio.h>
#include<conio.h>

Main ()
{
    Int a,b,c,largest;
    Clrsor();
    Printf("enter the values of a,b,c:\n");
    Scanf("%d%d%d", &a, &b, &c);
```