```
```
----------
else if (condition_n)
{
Statements_n_Block;
}
else
Statements_x;
```
```

# Programming Problems

# Problem 1

Write a program to input three numbers and then print the maximum number between them with the help of if else if else.

# Solution

```
```c
#include <stdio.h>
#include<conio.h>
void main()
{
int a,b,c;
clrscr();
printf("\n enter the values of a b and c");
scanf("%d %d %d",&a,&b,&c);
if(a>b && a>c)
printf("\n the maximum no is %d",a);
else if(b>c)
printf("\n the maximum number is %d",b);
else
printf("\n the maximum number is %d",c);
getch();
}
```
```

The execution of the above code is as follows:

Here, the conditions are evaluated in order from top to bottom. As soon as any condition evaluates to true, then the statement associated with the given condition is executed and control is transferred to Statements_x skipping the rest of the conditions following it. But if all conditions evaluate false, then the statement following a final else is executed followed by the execution of Statements_x.

The flow chart of the if else if else statement is as follows:

![](bbox=[0.068, 0.498, 0.934, 0.912])