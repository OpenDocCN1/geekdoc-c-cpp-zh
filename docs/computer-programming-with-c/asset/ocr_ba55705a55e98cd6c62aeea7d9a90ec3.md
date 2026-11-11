# **Case 2: User inputs the values such that, value of a is not greater than value of b**

When the value of variable a is not greater than the value of variable b the condition,

```
a>b
```

will be evaluated as false. Hence, the control of execution enters into the else block thereby printing the value of variable b on the computer screen. For example, if the user enters the value of variable a as 200 and value of variable b as 1000 then the control of execution will enter into the else block thereby printing the value of variable b which is 1000 on the computer screen as shown below:

```
Enter two numbers
200 1000
The maximum is 1000
```

# 4.2.3  **Program to calculate gross salary: An example**

As an example, let us write a program to compute Gross salary (GS) of an employee. The GS is obtained as the addition of House Rent Allowance (HRA), Basic Salary (BASIC) and Special Allowance (SA) which are components paid to every full time employee of the firm on monthly basis.

```
GS = HRA + BASIC + SA
```

Further, the organization has a rule that if the basic salary of a particular employee is greater than 20000 HRA is to 25 per cent and SA is 30 per cent. Otherwise, HRA is 10 per cent and SA is 50 per cent of basic salary. The program should take the value of basic salary (BASIC) as input from the user and print the calculated value of the GS.

Given below is the program that accepts the basic salary as input from the user and prints the value of the GS of the employee.

```
#include<stdio.h>
void main()
{
float BASIC, HRA, SA, GS;
printf("Enter the basic salary of the employee\n");
scanf("%f",&BASIC);
    if(BASIC>20000)
    {
    HRA=0.25*BASIC;
    SA=0.3*BASIC;
    }
    else
    {
    HRA=0.1*BASIC;
    SA=0.5*BASIC;
    }
```