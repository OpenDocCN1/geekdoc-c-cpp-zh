```
The program displays the following output
Enter the limit : 10
Sum of Even numbers within 10 is 30
```

In Program 2.3, main() is the calling function which calls the function sum(). The sum() contains no arguments and hence, there are no argument declarations. Note that the called function (i.e., sum()) receives its data (i.e., the limit for calculating the even numbers) directly from the input terminal (i.e., keyboard) in the called function (i.e., sum()). The return statement is employed in this function to return the sum of first n even numbers calculated within the limit and the result is displayed from the main() function to the standard output device (i.e., screen). Note that int is used before the function name sum() instead of void since it returns a value of type int to the called function.

# Function with Arguments and no Return Values

When a function has arguments, it receives data from the calling function. The main() function will not have any control over the way in which the function receives its input data. We can also make the calling function to read data from the input terminal and pass it to the called function. This approach seems better because the calling function can check the validity of data, before it is passed over to the called function. Program 2.4, helps you to understand things better.

# Program 2.4:

```
/* Program to calculate simple interest. */
/* agnot.c */
#include<stdio.h>
void simple(float, float, int); /* Function prototype or declaring functions */
float principal, rate;
int year;
void main()
{
printf("Enter principal,rate of interest & no.of years \n");
scanf("%f %f %d", &principal, &rate, &year);
simple(principal, rate, year);
}
void simple(float principal, float rate, int year)
{
float simple interest = 0.0;
simple interest = ( principal * rate * year ) / 100;
printf("The simple interest is %.2f", simple_interest);
}
```

```
The program displays the following output
Enter principal,rate of interest & no.of years
5000 1.5 2
The simple interest is 150.00
```