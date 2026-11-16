# Program 1.9:

```
/* Program to demonstrate the use of switch statement */
/* switch.c */
#include<stdio.h>
void main()
{
 int a, b, choice;
 printf("Enter two numbers : ");
 scanf("%d %d", &a, &b);
 printf("\n Enter 1 for addition : ");
 printf("\n Enter 2 for subtraction : ");
 printf("\n Enter 3 for multiplication : ");
 printf("\n Enter 4 for division : ");
 printf("\n Enter your choice : ");
 scanf("%d", &choice);
 switch(choice)
 {
 case 1:
 printf("Sum is %d", a+b);
 break;
 case 2:
 printf("Difference is %d", a-b);
 break;
 case 3:
 printf("Product is %d", a*b);
 break;
 case 4:
 printf("Quotient is %d", a/b);
 break;
 default:
 printf("Invalid choice");
 }
}
```

# The program displays the following output

```
Enter two numbers : 5 8
Enter 1 for addition
Enter 2 for subtraction
Enter 3 for multiplication
Enter 4 for division
Enter your choice : 1
Sum is 13
```

As soon as the user enters 5 and 8 it is assigned to the variables a and b respectively. The user has entered his choice as 1 and hence the control is transferred directly to the first case statement inside the switch statement, which has the value is 1. The printf( ) function inside the case statement is executed with the sum of a and b as
Sum is 13
and the break statement below the printf( ) function transfers the control to the end of switch-case statement.