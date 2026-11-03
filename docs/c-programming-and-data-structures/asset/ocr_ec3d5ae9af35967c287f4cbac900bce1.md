# A.42 Computer Programming

```
void main()
{
 int x=0,y=1,n;
 void fib(int,int,int);/*Function prototype*/
 clrscr();
 printf("Enter the number of terms in Fibonacci series: ");
 scanf("%d",&n); /*Reading number of terms in the series*/
 printf("\nThe Fibonacci series is:");
 printf("\n\n\t%d\t%d",x,y); /*Printing ist two terms of the series*/
 fib(x,y,n-2); /*Function Call*/
 printf("\n");
 getch();
}
void fib(int a,int b,int n)
{
 int c;
 if(n==0)
 return;
 n--;
 c=a+b;
 printf("\n\t%d",c);
 fib(b,c,n);/*recursive function call*/
}
```

Output
Enter the number of terms in Fibonacci series: 8

The Fibonacci series is:

0 1 1 2 3 5 8 13

# EXAMPLE A.50 Write a program that uses functions to compute the product of two given matrices.

```
Program
/*Program for multiplying two 3 X 3 matrices using functions*/
#include <stdio.h>
#include <conio.h>

void main()
{
 int i,j,k,a[3][3],b[3][3];
 void multiply (int [] [], int [] []); /*Declaring the function prototype for matrix multiplication*/
```