# Example

```
for (i = 0; i<10; i = i+1)
{
printf("%d",i);
}
```

The for loop will be executed 10 times. Each time a value equal to the current value of i will be printed out.

Various forms of loop statements can be as follows

+   (a) `for(condition;increment/decrement)`
+   
+       `body;`
+   
+   A blank first statement will mean no initialization.
+   
+   (b) `for(initialization;condition;)`
+   
+       `body;`
+   
+   A blank last statement will mean no running increment/decrement.
+   
+   (c) `for(initialization;increment/decrement)`
+   
+       `body;`
+   
+   A blank second conditional statement means no test condition to control the exit from the loop. So, in the absence of second statement, it is required to test the condition inside the loop otherwise it results in an infinite loop where the control never exits from the loop.
+   
+   (d) `for(;;increment/decrement)`
+   
+       `body;`
+   
+   Initialization is required to be done before the loop and test condition is checked inside the loop.
+   
+   (e) `for(initialization;;)`
+   
+       `body;`
+   
+   Test condition and control variable increment/decrement is to be done inside the body of the loop.
+   
+   (f) `for(;condition;)`
+   
+       `body;`
+   
+   Initialization is required to be done before the loop and control variable increment/decrement is to be done inside the body of the loop.
+   
+   (g) `for(;;)`
+   
+       `body;`
+   
+   Initialization is required to be done before the loop, test condition and control variable increment/decrement is to be done inside the body of the loop.

# Additional Features of for loop

+   1. More than one variable can be initialized at a time in the for statement.
+      For example:
+      `for (p=1,q=0; n<18; ++n)`
+   
+   2. Like the initialization section, the increment section may also have more than one part.
+      For example,
+      `for (a=2,b=30; n <= m; n=n+1,m=m-1)`
+      ```
+      {
+      p = b/a;
+      printf("%d",p);
+      }
+      ```
+   
+   3. It is also permissible to use expressions in the assignment statements of initialization and increment sections.
+      For example
+      `for (w = (a+b); w>0; w=w/2) is valid.`
+   
+   4. One or more sections in the for statement can be omitted, if necessary.
+      For example,
+      `e = 2;`
+      `for (; e != 10 ;)`
+      ```
+      {
+      printf("%d",e);
+      e = e + 2;
+      }
+      ```

Both the initialization and increment sections are omitted in the for statement. In such cases, the sections are left blank. However, the semicolons separating the sections must remain. If the test-condition is not present, the for statement sets up an infinite loop.

# Programming Problems

# Problem 1

Write a program to print only the numbers from 1 to 100 with the help of for loop.

# Solution

```
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
printf("%d\n",i);
```