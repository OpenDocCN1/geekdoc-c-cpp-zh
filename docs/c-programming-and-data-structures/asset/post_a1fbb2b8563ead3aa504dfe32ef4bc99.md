
## A.16 Computer Programming

```c
while(y<row)
{
    for(x=40-3*y;x>0;--x)
        printf(" ");
    for(z=0;z<=y;++z)
    {
        if((z==0)||(y==0))
            b=1;
        else
            b=(b*(y-z+1))/z;
        printf("%6d",b);
    }
    printf("\n");
    ++y;
}
getch();
```

### Output

```text
Enter the number of rows for the Pascal's triangle:5

********Pascal's Triangle********

     1
   1   2   1
  1   3   3   1
 1   4   6   4   1

     1
   1   2   1
  1   3   3   1
 1   4   6   4   1
```

## EXAMPLE A.23

Write a program to find the sum of the following series up to 50 terms:
-1^3 - 5^3 - 7^3 - 9^3 - 11^3 - ....

```c
/*Program for demonstrating the use of while statement*/
#include <stdio.h>
#include <conio.h>
void main()
{
    int b,row,y,z;
    clrscr();
    b=1;
    y=0;
    printf("Enter the number of rows for the Pascal's triangle:");
    scanf("%d",&row);
    printf("\n*****Pascal's Triangle*****\n");
    while(y<row)
    {
        for(x=40-3*y;x>0;--x)
        {
            printf(" ");
        }
        for(z=0;z<y;++z)
        {
            if((z==0)||(y==0))
                b=1;
            else
                b=(b*(y-z+1))/z;
            printf("%6d",b);
        }
        ++y;
    }
    getch();
}
```

Sum of series = 499850

## EXAMPLE A.24

Write a program to calculate the sum of N terms of the following series: 1² + 2² + 3² + 4² + ..... n²

```c
/*Program to demonstrate the use of for statement*/
#include <stdio.h>
#include <conio.h>
void main()
{
    int i,n;
    long sum=0;
    clrscr();

    printf("Enter the value of n = ");
    scanf("%d",&n);/*Reading number of terms in the series, n*/
    for(i=1;i<=n;i++)/*Calculating the sum of the series*/
        sum=sum+i*i;

    printf("Sum of series = %ld",sum);

    getch();
}
```

### Output

```text
Enter the value of n = 5
Sum of series = 55
```

## EXAMPLE A.25

Write a program to find the sum of the following series: 1 + x + x² + x³ + ....... + xⁿ.

### Program

```c
/*Program for demonstrating the use of for statement*/
#include <stdio.h>
#include <conio.h>
#include <math.h>

void main()
{
    long sum;
    int n,x,i;
    clrscr();

    printf("Enter the values of x and n:");
    scanf("%d %d",&x,&n);/*Reading values of x and n*/

    if(n==0 || x==0)/*Identifying incorrect values*/
    {
        printf("The values must be positive integers. Please try again\n");
        getch();
    }
    else
    {
        sum=1;
        for(i=1;i<=n;i++)
        {
            sum=sum+pow(x,i);/*Calculating the sum of the series*/
        }
        printf("Sum of series=%ld\n",sum);
    }
    getch();
}
```

### Output

```text
Enter the values of x and n:2
6
Sum of series=127
```

## EXAMPLE A.26

Write a program to find the sum of the following series:
1 + 2 + 2² + 2³ + ....... + 2ⁿ.

### Program

```c
/*Program for demonstrating the use of for statement*/
#include <stdio.h>
#include <conio.h>
#include <math.h>

void main()
{
    long sum;
    int n,i;
    clrscr();

    printf("Enter the value of n: ");
    scanf("%d",&n);/*Reading value of n*/

    sum=1;
    for(i=1;i<=n;i++)
    {
        sum=sum+pow(2,i);/*Calculating the sum of the series*/
    }
    printf("Sum of series = %ld\n",sum);

    getch();
}
```

### Output

```text
Enter the value of n: 5
Sum of series = 63
```

## EXAMPLE A.27

Write a program to solve the following series:
1 + 1/2 + 1/3 + 1/4 + ... + 1/n.

### Program

```c
/*Program for demonstrating the use of for statement*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int n;
    float i;
    double sum;
    clrscr();
    printf("Enter the value of n: ");
    scanf("%d",&n);/*Reading the value of n*/
    sum = 1.0;
    for(i=2.0;i<=n;i++)/*Calculating the sum of the series*/
        sum = sum + 1.0/i;
    printf("\nThe sum of the series 1 + 1/2 + 1/3 +....+1/n = %.8f",sum);
    getch();
}
```

### Output

```text
Enter the value of n: 8

The sum of the series 1 + 1/2 + 1/3 +....+1/n = 2.71785714
```

## EXAMPLE A.28

Write a program to determine whether a given number is prime or not.

### Program

```c
/*Program for demonstrating the use of for statement*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int num,i;
    clrscr();

    printf("\nEnter a number: ");
    scanf("%d",&num);/*Reading a number*/
    for(i=2;i<=num;i++)
        if(num%i==0)/*Checking if num is divisible by another number*/
        {
            printf("\n%d is not a prime number",num);
            break;
        }
        else
            ;
    if(i==num)
        printf("\n%d is a prime number",num);
    getch();
}
```

### Output

```text
Enter a number: 79

79 is a prime number
```

## EXAMPLE A.29

Write a program for printing the Fibonacci series.

### Program

```c
/*Program for demonstrating the use of for statement*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int num1=0, num2=1,len,i,fab;
    clrscr();

    printf("\n\nEnter Length of the Fibonacci Series: ");
    scanf("%d",&len);/*Reading series length*/

    printf("\n<---FIBONACCI SERIES--->");
    printf("\n%d  %d",num1,num2);/*Printing initial values of the series*/

    /*Printing the Fibonacci series*/
    for(i = 1; i <= len-2; i++)
    {
        fab=num1 + num2;
        printf("  %d",fab);
        num1=num2;
        num2=fab;
    }

    getch();
}
```

### Output

```text
Enter Length of the Fibonacci Series: 6
<---FIBONACCI SERIES--->
0 1 1 2 3 5
```

## EXAMPLE A.30

Write a program to calculate the sum of the following series: 1³ + 3⁴ + 5⁵...... up to 100 terms.

## A.22 Computer Programming

### Program

```c
/*Program for demonstrating the use of for statement*/
#include<stdio.h>
#include<conio.h>
#include<math.h>

void main()
{
    int i;
    long sum=0;
    clrscr();
    for(i=1;i<=100;i=i+2)
        sum=sum+pow(i,4);/*Calculating the sum of the series*/
    printf("\nSum of the series up to first 100 terms is equal to %ld",sum);
    getch();
}
```

### Output

```text
Sum of the series up to first 100 terms is equal to 99966690
```

## EXAMPLE A.31

Write a program for displaying a pyramid of the following form:

```text
0
1 0 1
2 1 0 1 2
3 2 1 0 1 2 3
4 3 2 1 0 1 2 3 4
5 4 3 2 1 0 1 2 3 4 5
```

### Program

```c
/*Program for demonstrating nesting of for statements*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int num,i,y,x=40;
    clrscr();

    printf("\nEnter a number for \ngenerating the pyramid:\n");
    scanf("%d",&num);

    /*Displaying the pyramid*/
    for(y=0;y<=num;y++)
    {
        gotoxy(x,y+1);
        for(i=-y;i<=y;i++)
            printf("%3d",abs(i));
        x=x-3;
    }

    getch();
}
```

### Output

```text
Enter a number for generating the pyramid:
6
        0
      1 0 1
    2 1 0 1 2
  3 2 1 0 1 2 3
4 3 2 1 0 1 2 3 4
5 4 3 2 1 0 1 2 3 4 5
6 5 4 3 2 1 0 1 2 3 4 5 6
```

## EXAMPLE A.32

Write a program to calculate the sum of odd numbers between 1 and 50.

### Program

```c
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

### Output

```text
Sum of odd numbers between 1 to 50 is = 625
```

## EXAMPLE A.33

Write a simple program to implement a one-dimensional array and print its index and corresponding values.

### Program

```c
/*Program for demonstrating implementation of a simple array*/
#include <stdio.h>
#include <conio.h>

void main() {
    int i;
    int arr[5];/*Declaring an array of five elements*/
    clrscr();

    printf("Enter the array values:\n");
    for(i=0;i<5;i++)
        scanf("%d", &arr[i]);/*Reading values to be stored in the array*/

    printf("\nArray arr[5] contains the following values:\n");
    for(i=0;i<5;i++)
        printf("arr[%d] = %d\n", i,arr[i]);/*Printing array values*/
    getch();
}
```

### Output

```text
Enter the array values:
10
20
30
40
50

Array arr[5] contains the following values:
arr[0] = 10
arr[1] = 20
arr[2] = 30
arr[3] = 40
arr[4] = 50
```

## EXAMPLE A.34

Write a program to generate Fibonacci series using arrays.

### Program

```c
/*Program for demonstrating the use arrays for generating Fibonacci series*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int arr[50],len,i;
    clrscr();

    printf("\n\nEnter length of the Fibonacci series: ");
    scanf("%d",&len);/*Reading series length*/

    arr[0]=0;/*Initializing 1st element of Fibonacci series*/
    arr[1]=1;/*Initializing 2nd element of Fibonacci series*/
    /*Storing the Fibonacci series values in array arr[]*/
    for(i=2;i<len;i++)
        arr[i]=arr[i-1]+arr[i-2];
    /*Printing the Fibonacci series*/
    printf("\n----FIBONACCI SERIES---->\n");
    for(i=0;i<len;i++)
        printf("%d ",arr[i]);
    getch();
}
```

### Output

```text
Enter length of the Fibonacci series: 8

<---FIBONACCI SERIES--->
0 1 1 2 3 5 8 13
```

## EXAMPLE A.35

Write a program to perform linear search on a one-dimensional array.

### Program

```c
/*Program for demonstrating linear search using a simple array*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int arr[10],i,j,element;
    int flag=0;
    clrscr();

    printf("Enter the 10 elements of the array:\n");
    for(i=0;i<10;i++)
        scanf("%d",&arr[i]);/*Reading array values*/

    printf("\n\nEnter the element that you want to search: ");
    scanf("%d",&element);/*Reading the element to be searched*/

    for(j=0;j<10;j++)
        if (arr[j] == element) /*Checking whether the search was successful*/
        {
            printf("\n\nThe element %d is present at %d position in the list\n",element,j+1);
            flag=1;
            break;
        }
    if(flag==0)/*Checking whether the search was unsuccessful*/
        printf("\n\nThe element %d is not present in the list\n",element);

    getch();
}
```
