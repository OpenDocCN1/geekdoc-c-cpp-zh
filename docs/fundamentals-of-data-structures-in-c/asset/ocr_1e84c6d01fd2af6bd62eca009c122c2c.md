# 1.2 Structure of a C Program

C is a programming language and so an introduction to structure of C program is presented in this section for better understanding the logic of a program by the reader. Every C program contains few basics of building blocks. These building blocks should be written in a correct order and procedure. Let us see a sample program for calculating the sum of two integers.

```
Program 1.1:
/* Program to calculate the sum of two integers */
/* firstpgm.c */
#include<stdio.h>
void main()
{
int x, y, sum;
printf("Enter the values of X and Y : ");
scanf("%d %d", &x, &y);
sum = x + y;
printf("The sum of the variables X and Y = %d", sum);
}
The program displays the following output
Enter the values of X and Y : 25 30
The sum of the variables X and Y = 55
```

Comments are added at each end of the statement in order to understand the overall program organisation easily. Let us see each comment statement in detail.

# /* Title comment */

Any comment statement used in a C program must be enclosed within /* */. The comment statement is used to identify the purpose of the program. This statement is usually specified at the start of a program, but can be specified any where in the program. This may or may not be present in the program as per the programmers wish. The comment statement is not an executable statement. It's a good programming practice to include comment statements in a program.

# /* Library file access */

The second line in the program #include <stdio.h> refers to a special file which contains the information about the various input and output operations which must be included in the program when it is compiled. The C compiler will handle the inclusion of the required information automatically. The header file stdio.h contains the information of all the standard input and output functions in C. If you don't include the header file stdio.h in the program, the C compiler may complain about undefined functions and data types used in the program.