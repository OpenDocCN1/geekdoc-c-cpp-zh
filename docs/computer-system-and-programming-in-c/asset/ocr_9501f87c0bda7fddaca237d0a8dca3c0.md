```
void main()
{
fact();
getch();
}
void fact()
{
int n,f=1;
clrscr();
printf("\n enter the number");
scanf("%d",&n);
while(n>0)
{
f=f*n;
n--;
}
printf("\n the factorial is %d",f);
}
```

# Problem 4

Write a program to input a number and print the number of digits of that particular number with the help of function and use the case of no arguments and no return value.

# Solution

```
#include<stdio.h>
#include<conio.h>
void digit();//function prototype
void main()
{
digit();
getch();
}
void digit ()
{
int n,d;
clrscr();
printf("\n enter the number");
scanf("%d",&n);
while(n>0)
{
n=n/10;
d++;
}
printf("\n the number of digits are %d",d);
}
```

# CALL BY VALUE AND CALL BY REFERENCE

The arguments passed to function can be of two types namely:

+   1. Values passed
+   2. Address passed

The first type refers to call by value and the second type refers to call by reference.
In the call by value only the duplicate value of the variable is passed to the function and if we perform any changes in the function then that particular changes does not reflect to the main program.
But in the call by reference the actual address is passed in the function and if perform any changes in the function then that particular changes must be reflect in the main program.

For instance consider **program1**

```
#include<stdio.h>
#include<conio.h>
void interchange(int,int);
void main()
{
int x=50, y=70;
interchange(x,y);
printf("x=%d y=%d",x,y);
}
void interchange(int x1,int y1)
{
int z1;
z1=x1;
x1=y1;
y1=z1;
printf("x1=%d y1=%d",x1,y1);
}
```

Here the value to function interchange is passed by value.

Consider **program2**

```
#include<stdio.h>
#include<conio.h>
void interchange(int *,int *);
void main()
{
int x=50, y=70;
interchange(&x,&y);
printf("x=%d y=%d",x,y);
}
void interchange(int *x1,int *y1)
{
int *z1;
*z1=*x1;
*x1=*y1;
```