
## Example

```c
for (i = 0; i<10; i = i+1)
{
printf("%d",i);
}
```

The for loop will be executed 10 times. Each time a value equal to the current value of i will be printed out.

Various forms of loop statements can be as follows

- (a) `for(condition;increment/decrement)`

    `body;`

    A blank first statement will mean no initialization.

- (b) `for(initialization;condition;)`

    `body;`

    A blank last statement will mean no running increment/decrement.

- (c) `for(initialization;increment/decrement)`

    `body;`

    A blank second conditional statement means no test condition to control the exit from the loop. So, in the absence of second statement, it is required to test the condition inside the loop otherwise it results in an infinite loop where the control never exits from the loop.

- (d) `for(;;increment/decrement)`

    `body;`

    Initialization is required to be done before the loop and test condition is checked inside the loop.

- (e) `for(initialization;;)`

    `body;`

    Test condition and control variable increment/decrement is to be done inside the body of the loop.

- (f) `for(;condition;)`

    `body;`

    Initialization is required to be done before the loop and control variable increment/decrement is to be done inside the body of the loop.

- (g) `for(;;)`

    `body;`

    Initialization is required to be done before the loop, test condition and control variable increment/decrement is to be done inside the body of the loop.

## Additional Features of for loop

1. More than one variable can be initialized at a time in the for statement.
   For example:
   `for (p=1,q=0; n<18; ++n)`

2. Like the initialization section, the increment section may also have more than one part.
   For example,
   `for (a=2,b=30; n <= m; n=n+1,m=m-1)`

   ```c
   {
   p = b/a;
   printf("%d",p);
   }
   ```

3. It is also permissible to use expressions in the assignment statements of initialization and increment sections.
   For example
   `for (w = (a+b); w>0; w=w/2) is valid.`

4. One or more sections in the for statement can be omitted, if necessary.
   For example,
   `e = 2;`
   `for (; e != 10 ;)`

   ```c
   {
   printf("%d",e);
   e = e + 2;
   }
   ```

Both the initialization and increment sections are omitted in the for statement. In such cases, the sections are left blank. However, the semicolons separating the sections must remain. If the test-condition is not present, the for statement sets up an infinite loop.

## Programming Problems

### Problem 1

Write a program to print only the numbers from 1 to 100 with the help of for loop.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
printf("%d\n",i);
getch();
}
```

```c
if(i%2==1)
printf("\n%d",i);
}
getch();
}
```

### Problem 2

Write a program to print the numbers from 100 to 1 with the help of for loop.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=100;i>=1;i--)
printf("\n%d",i);
getch();
}
```

### Problem 3

Write a program to print only the even numbers from 1 to 100 with the help of for loop.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
{
if(i%2==0)
printf("\n%d",i);
}
getch();
}
```

### Problem 4

Write a program to print only the odd numbers from 1 to 100 with the help of for loop.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
{
if(i%2==1)
printf("\n%d",i);
}
getch();
}
```

### Problem 5

Program for generating ‘N’ natural numbers using for loop.

### Solution

```c
#include < stdio.h >
void main()
{
int n, i; //Declare and initialize the variables
printf("Enter the upper limit number"); // Message to the user
scanf("%d", &n); //read and store the number
for(i=1;i<=n;i++)
printf("\n%d",i);
getch();
}
```

### Problem 6

Write a program to input a number and print number of digits of that number with the help of for loop.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,digit=0;
clrscr();
printf("\n enter the number");
scanf("%d",&n);
for(;n>0;n=n/10)
{
digit++;
}
printf("\n the number of digits are %d",digit);
getch ();
}
```

### Problem 7

Write a program to input a number and print sum of digits of that number with the help of for loop.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,sum=0,r;
clrscr();
printf("\n enter the number");
scanf("%d",&n);
for(;n>0;n=n/10)
{
r=n%10;
sum=sum+r;
}
printf("\n the sum is %d",sum);
getch();
}
```

### Example

Write a program to generate the following pattern given below:

- 1
- 1 2
- 1 2 3
- 1 2 3 4

```c
/* Program to print the pattern */
#include<stdio.h>
#include<conio.h>
void main()
{
int i,j;
clrscr();
for (i=1;i<=4;++i)
{
printf("%d \n",i);
for(j=1;j<=i;++j)
printf("%d ",j);
}
getch();
}
```

## The Nested Loop

These loops are the loops which contain another looping statement in a single loop. These types of loops are used to create matrix. Any loop can contain a number of loop statements in itself. If we are using loop within loop that is called nested loop. In this the outer loop is used for counting rows and the internal loop is used for counting columns.

The general syntax of Nested Loop is as follows:

```c
for (initializing ; test condition ; increment / decrement) //Outer Loop
{
statement;
for (initializing ; test condition ; increment / decrement) // Inner Loop
{
body of inner loop;
}
statement;
}
```

The execution of the nested loop is as follows:

Firstly the outer loop is executed and according to the outer loop the inner loop is executed and according to the inner loop the statements are executed. When the inner loop is terminated then the pointer is automatically goes to outer loop and when the outer loop is terminated then the complete loop is terminated.

Here, an *inner for loop* is written inside the *outer for loop*. For every value of *i*, *j* takes the value from 1 to i and then value of i is incremented and next iteration of outer loop starts ranging j value from 1 to i.

## Programming Problems

### Problem 1

Write a program to print the tables from 1 to 10.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i,j;
clrscr();
for(i=2;i<=10;i++)
{
for(j=1;j<=10;j++)
printf("\n%d",i*j);
}
getch();
}
```

```c
{
printf("%d ",i);
i=i+2;
if (i>=20)
goto outside;
}
outside : printf("over");
}
```

The output of the above code is as follows:
2 4 6 8 10 12 14 16 18 20 over

## THE BREAK STATEMENT

A *break statement* lets you end an *iterative (do, for, or while) statement* or a *switch statement* and exit from it at any point other than the logical end. A **break** may only come along on one of these statements.

A **break** statement has the form:

```c
break;
```

In an iterative statement, the **break** statement ends the loop and moves control to the next statement outside the loop. Within nested statements, the **break** instruction ends only the smallest enclosing **do, for, switch, or while** instruction.

In a **switch** instruction, the **break** passes control out of the **switch** body to the next statement outside the **switch** statement.

### Use of Break with Switch Statement

**break** is used with the conditional switch statement and with the do, for, and while loop statements. In a **switch** statement, **break** induces the program to execute the next statement after the **switch**. Without a **break** statement, every statement from the matched **case** label to the end of the **switch**, admitting the **default**, is executed.

The following example demonstrates the use of break with switch statement:

### Switch without Break

```c
switch(c)
{
case 1:printf("\n hello world");
case 2: printf("\n Hi");
case 3: printf("OOPs");
}
```

If we define c=1 then the output will be hello world Hi and Oops because we are not using the break statement.

using the break statement.

### Switch with break

```c
switch(c)
{
case 1:printf("\n hello world");
    break;
case 2: printf("\n Hi");
    break;
case 3: printf("OOPs");
    break;
}
```

If we define c=1 then the output will be hello world and switch is automatically terminated and if we define c=2 then the output will be Hi and switch is automatically terminated and if we define c=3 then the output will be Oops and switch is automatically terminated.

### Use of break with loops

In loops, **break** terminates execution of the nearest enclosing **do, for, or while** statement. Control passes to the statement that follows the finished statement, if any.

Within nested statements, the **break** statement ends only the **do, for, switch, or while** statement that instantly encloses it. You can use a **return** or **goto** statement to transfer control from within more intensely nested structures.

## Example

The following example demonstrates the use of break statement with for loop.

```c
#include <stdio.h>
void main()
{
int i;
for (i = 1; i < 10; i++)
{
printf("%d\n", i);
if (i == 4)
break;
}
getch();
// Loop exits after printing 1 through 4
```

The output of the above program is as follows:
1
2
