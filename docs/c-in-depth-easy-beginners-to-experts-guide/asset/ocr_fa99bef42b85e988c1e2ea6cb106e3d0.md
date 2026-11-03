# **Functions**

# **************

# 113.wap which shows sending & receiving values between functions.

```
#include<stdio.h>
#include<conio.h>
int calsum(int x,int y,int z);/* function prototype*/
void main()
{
int a,b,c,sum;
printf("\n Enter any three numbers");
scanf("\n %d%d%d",&a,&b,&c);
sum=calsum(a,b,c);    /*function calling*/
printf("\n Sum=%d",sum);
getch();
}
/*function definination or body*/
int calsum(int x,int y,int z)
{
int d;
d= x+y+z;
return(d);
}
```

# 114.wap to calculate square of no. with return type.

```
#include<stdio.h>
#include<conio.h>
float square(float);/* function prototype*/
void main()
{
float a,b;
printf("\n Enter any number");
scanf("\n %f",&a);
b=square(a);
printf("\n square of %f is %f",a,b);
```