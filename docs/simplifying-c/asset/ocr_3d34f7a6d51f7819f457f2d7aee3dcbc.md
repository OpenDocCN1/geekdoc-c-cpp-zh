The arithmetic operations in C language can be categorized as integer arithmetic, real arithmetic, or mixed mode arithmetic based on the operand used in the expression. The next section discusses these arithmetic operations in detail.

# Integer Arithmetic

In C language, when the operands used in the expression are positive or negative whole numbers, the arithmetic is considered to be an integer arithmetic. The resultant expression is called an integer expression, whose result is always an integer. Program 1 gives an example of integer arithmetic:

# Program 1

```
/* Program to illustrate the use of integer arithmetic */
#include <stdio.h>

/* Beginning of main function */
main() 
{
 /* Declare variables */
int i_base, i_height, i_area;

/* Accept the value of base and height */
printf("\nEnter the value of base of triangle: ");
scanf("%d",&i_base);
printf("\nEnter the value of height of triangle: ");
scanf("%d",&i_height);

/* Calculate are of triangle */
i_area = (i_base * i_height) / 2;

/* Print Area */
printf("\nArea of triangle with base %d and height % is %d\n", i_base,i_height,i_area);
return;
}
/* End of function main */
```

Output 1:

| Enter the value of base of triangle: 10 Enter the value of height of triangle: 15 Area of triangle with base 10 and height 15 is 75 |
| --- |

Output 2:

| Enter the value of base of triangle: 5 Enter the value of height of triangle: 15 Area of triangle with base 5 and height 15 is 37 |
| --- |

Program 1 is designed to calculate the area of a triangle. Output 1 of the program does not have any problem. Let's observe Output 2 carefully: as per the conventional mathematics, (5 × 15)/2 should result in 37.50. However, it can be seen in Output 2 that the value of area is 37 instead of 37.50. This is the reason why we said that the output of an integer arithmetic is always an integer value. The division operator in C language works differently from conventional mathematics. In conventional mathematics, 7/10 would give