```
sum=0;
else
{
sign=(n%2==0)?-1:1;
term=sign*power(x,2*n-1)/fact(2*n-1);
sum=term+rseries(x,n-1);
}
return sum;
}
```

The ith term of the series is x^(2*i-1)/(2*i-1)! . In iterative function, we'll take a loop from i=1 to i=n and add all the terms. To calculate the numerator and denominator of a term we'll use the functions power() and fact(). Since the terms have alternate positive and negative signs, so we'll take a variable sign, initialize it with 1 and multiply it with -1 on each iteration of the loop.

# Problem 10

Write a program to find out the Least Common Multiple and Highest Common factor of two numbers recursively. The iterative method is given in Program P5.42.

```
/*P6.37 Program to find out the LCM and HCF of two numbers recursively*/
#include<stdio.h>
int m,n;
main()
{
int x,y;
printf("Enter two numbers : ");
scanf("%d %d",&x,&y);
printf("HCF of %d and %d is %d\n",x,y,hcf(x,y));
m=x;n=y;
printf("LCM of %d and %d is %d\n",x,y,lcm(x,y));
}
int hcf(int a,int b)
{
if(a==b)
return(b);
else if(a<b)
hcf(a,b-a);
else
hcf(a-b,b);
}
int lcm(int a,int b)
{
if(a==b)
return(b);
else if(a<b)
lcm(a+m,b);
else
lcm(a,b+n);
}
```