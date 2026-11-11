# ### 4.2.1  Program to check if the number is even or odd: An example

As an example, let us write a program that accepts a number x as input from the user and determines if the number is even or odd. Given below is the full source code that prints a message as The number is Even if the user inputs the value of variable x which is divisible by 2. The code prints a message as The number is Odd if the user inputs the value of variable x which is not divisible by 2.

```
```c
#include<stdio.h>
void main()
{
int x;
printf("Enter a number\\n");
scanf("%d",&x);
    if(x%2==0)
    {
    printf("The number is Even\\n");
    }
    else
    {
    printf("The number is Odd\\n");
    }
}
```
```

# **Output**

```
```text
Enter a number
10
The number is Even
```
```

The sequence of instructions to be executed in the code will be altered by the result of condition x%2==0 as shown in Figure 4.3.

We will discuss the execution of the code in two cases as mentioned below:

# **Case 1: User enters the value of variable x which is divisible by 2**

When the value of variable x is divisible by 2, the condition,

`x%2==0`

will be evaluated as **true**. Hence the control of execution enters into the if block thereby printing the following message on the computer screen.

```
```text
The number is Even
```
```

It is important to note that, we have used an operator == which checks if the value of left hand side of the expression (which is x%2) is same as the value of right hand side of the expression (which is zero). This means that, the control of execution will enter into the if block provided that the remainder of x with respect to 2 is zero. For example, if the user