# Solution

```
```c
#include<stdio.h>
#include<conio.h>
int digit();//function prototype
void main()
{
int d;
clrscr();
d=digit();//calling of a function
printf("\n the number of digits are %d",d);
getch();
}
int digit ()
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
return (d);
}
```
```

# NO ARGUMENTS AND NO RETURN TYPE

In this type of declaration, we do not pass the arguments to the function and the function does not return any value.

**For example**

If we define void add (). The meaning of this line is that add is a function which does not accept any argument and it does not return any value.

*Programming Problems*

# Problem 1

Write a program to input two numbers and print the addition of both the numbers with the help of function and use the case of no argument and no return value.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void add ();//function prototype
void main()
```
```

```
```c
{
add();
getch();
}
void add ()
{
int a,b,c;
printf("\n enter the values of a and b");
scanf("%d %d",&a,&b);
c=a+b;
printf("\n the addition is %d",c);
}
```
```

# Problem 2

Write a program to input two numbers and print the maximum number between them with the help of function and use the case of no arguments and no return value.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void maximum();//function prototype
void main()
{
maximum();//calling of function
getch();
}
void maximum()
{
int a,b;
clrscr();
printf("\n enter the values of a and b");
scanf("%d %d",&a,&b);
if(a>b)
printf("\n the maximum value is %d",a);
else
printf("\n the maximum value is %d",b);
}
```
```

# Problem 3

Write a program to input a number and print the factorial of that number with the help of function and use the case of no arguments and no return value.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void fact ();//function prototype
```
```