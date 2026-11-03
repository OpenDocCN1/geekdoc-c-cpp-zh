```
```c
printf("n*****Pascal's Triangle*****
");
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
}
printf("%6d",b);
}
++y;
}
getch();
```
```

Sum of series = 499850

# EXAMPLE A.24

Write a program to calculate the sum of N terms of the following series: 1² + 2² + 3² + 4² + ..... n²

```
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
for(i=1;i<=n;i++);/*Calculating the sum of the series*/
sum=sum+i*i;

printf("Sum of series = %ld",sum);

getch();
}
```
```