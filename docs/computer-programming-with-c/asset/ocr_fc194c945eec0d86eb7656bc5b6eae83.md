# Solved Example 7.2

Write a program to take the value of variable n as input from the user and to calculate the result of following series using recursion.

1+2+3+4+--+n

```
```c
#include<stdio.h>
int sum(int);
void main()
{
 int n;
 printf("Enter the value of n: \n");
 scanf("%d",&n);
 printf("The value of the series is: %d \n",sum(n));
}
int sum(int n)
{
 if(n==1)
 {
 return n;
 }
 else
 {
 return sum(n-1)+n;
 }
}
```
```

# Output

Enter the value of n:
4
The value of the series is: 10

# Solved Example 7.3

Write a program to create a function average() that accepts an integer type array as an argument and returns the average of n elements stored in the array.

```
```c
#include<stdio.h>
float average(int[],int);
void main()
{
 int a[100],n,i;
 float mean;
 printf("Enter the number of elements to be stored in the array\n");
 scanf("%d",&n);
```
```