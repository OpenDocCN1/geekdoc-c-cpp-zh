Output
Enter a number for generating the pyramid:
6
        0
      1 0 1
    2 1 0 1 2
  3 2 1 0 1 2 3
4 3 2 1 0 1 2 3 4
5 4 3 2 1 0 1 2 3 4 5
6 5 4 3 2 1 0 1 2 3 4 5 6

# EXAMPLE A.32 Write a program to calculate the sum of odd numbers between 1 and 50.

```
Program
/*Program to demonstrate the use for Statement*/
#include<stdio.h>
#include<conio.h>

void main()
{
    int i,sum=0;
    clrscr();

    for (i=1;i<=50;i++)/*Specifying the looping condition*/
    {
        if(i%2==0)/*Identifying even numbers*/
            continue;
        sum=sum+i;/*Calculating the sum of odd numbers*/
    }

    printf("\nSum of odd numbers between 1 to 50 is = %d", sum);

    getch();
}
```

Output
Sum of odd numbers between 1 to 50 is = 625

# EXAMPLE A.33 Write a simple program to implement a one-dimensional array and print its index and corresponding values.

```
Program
/*Program for demonstrating implementation of a simple array*/
#include <stdio.h>
#include <conio.h>
```