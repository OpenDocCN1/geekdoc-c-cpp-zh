In do-while, the statements would be executed at least once even if the condition fails for the first time itself. The operation of the do-while loop can be stated from the flowchart in Fig. 1.6. Program 1.13, helps you to understand things better.

```
Program 1.13:
/* do_while.c */
#include<stdio.h>
void main()
{
 char yes;
 int a, b;
 do
 {
 printf("Enter two numbers : ");
 scanf("%d %d", &a, &b);
 printf("SUM = %d", a+b);
 printf("\n Do U want to continue say Y/N : ");
 scanf("%c", &yes);
 }while((yes == 'Y')||(yes == 'y'));
}
```

![](bbox=[0.656, 0.106, 0.886, 0.486])

The program displays the following output
Enter two numbers : 5 5
SUM = 10
Do u want to continue say Y/N : Y
Enter two numbers : 6 3
SUM = 9
Do u want to continue say Y/N : N

The output of Program 1.13, clearly states the function of a do-while loop. The control enters the loop without testing any condition and the body of the loop is executed once. The while statement checks the condition, since it is true (i.e., y) control is transferred again to the starting of the do loop and the body of the loop is again executed. This process continues until the condition is false (i.e., n). Note that semicolon is placed after while since it is considered as statement in the do-while loop.

# 1.10.3 The for Loop

The for loop is most commonly and popularly used loop in C. The for loop allows us to specify three things about the loop in a single line. They are,

+   - Initializing the value for the loop
+   - Condition in the loop counter to determine whether the loop should continue or not
+   - Incrementing or decrementing the value of loop counter each time the program segment has been executed.