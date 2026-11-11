switch statement to conclude. If the user types in more than one digit, the **default** block is accomplished, producing an error message.

```
```c
switch(n) {
case 0:
printf("You typed zero.\n");
break;
case 1:
case 9:
printf("n is a perfect square\n");
break;
case 3:
case 5:
case 7:
printf("n is a prime number\n");
break;
case 2:
printf("n is a prime number\n");
case 4:
case 6:
case 8:
printf("n is an even number\n");
break;
default:
printf("Only single-digit numbers allowed\n");
break;
}
```
```

# **Problem 4**

Write a program that performs the following, depending upon the choice selected by the user.

+   i. Calculate the square of number if choice is 1
+   
+   ii. Calculate the cube of number if choice is 2 and 4
+   
+   iii. Calculate the cube of the given number if choice is 3
+   
+   iv. Otherwise print the number as it is

# **Solution**

```
```c
#include<stdio.h>
#include<conio.h>
#include<math.h>
void main()
{
int n,choice;
printf("\n Enter any number:\n ");
scanf("%d”,&n);
```
```

```
```c
printf(“Choice is as follows:\n\n”);
printf(“1. To find square of the number\n”);
printf(“2. To find square-root of the number\n”);
printf(“3. To find cube of a number\n”);
printf(“4. To find the square-root of the number\n\n”);
printf(“Enter your choice:\n”);
scanf(“%d”,&choice);
switch (choice)
{
case 1 : printf(“The square of the number is %d\n”,n*n);
break;
case 2 :
case 4 : printf(“The square-root of the given number is %f”,sqrt(n));
break;
case 3: printf(“The cube of the given number is %d”,n*n*n);
default : printf(“The number you had given is %d”,n);
break;
}
getch();
}
```
```

The output of the above code segment is as follows:

Enter any number:
4

Choice is as follows:
1. To find square of the number
2. To find square-root of the number\n”);
3. To find cube of a number
4. To find the square-root of the number

Enter your choice:
2
The square-root of the given number is 2

# **LOOP CONTROL STATEMENTS**

In looping, a sequence of statements are executed until some condition is satisfied which is placed for termination of the loop. A program loop comprises two segments; one is the body of the loop and the other known as the control statement. The control is tested forever for execution of the body of the loop. Depending upon the position of the control statement in the loop, a control may be