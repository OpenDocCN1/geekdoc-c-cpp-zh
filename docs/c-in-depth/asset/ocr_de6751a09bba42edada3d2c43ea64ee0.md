n! = { 1          n=0
      n * (n-1)!   n>0 }

Now we'll write a program, which finds out the factorial using a recursive function.

```
/*P6.24 Program to find the factorial of a number by recursive method*/
#include<stdio.h>
long fact(int n);
main()
{
    int num;
    printf("Enter a number : ");
    scanf("%d",&num);
    printf("Factorial of %d is %ld\n",num,fact(num));
}
long fact(int n)
{
    if (n==0)
        return(1);
    else
        return(n*fact(n-1));
}
```

This function returns 1 if the argument n is 0, otherwise it returns n*fact(n-1). To return n*fact(n-1), the value of fact(n-1) has to be calculated for which fact() has to be called again but this time with an argument of n-1. This process of calling fact() continues till it is called with an argument of 0.

Suppose we want to find out the factorial of 5.

+   - Initially main() calls factorial(5)
+   - Since 5>0, factorial(5) calls factorial(4)
+   - Since 4>0, factorial(4) calls factorial(3)
+   - Since 3>0, factorial(3) calls factorial(2)
+   - Since 2>0, factorial(2) calls factorial(1)
+   - Since 1>0, factorial(1) calls factorial(0)

winding phase

When factorial() is called with n=0 then the condition inside if statement becomes true, so now the recursion stops and control returns to factorial(1) Now every called function will return the value to the previous function. These values are returned in the reverse order of function calls.