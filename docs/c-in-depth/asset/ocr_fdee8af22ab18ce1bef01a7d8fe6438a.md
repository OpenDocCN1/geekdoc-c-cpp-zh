# 6.9.4 Function With Arguments And Return Value

These types of functions have arguments, so the calling function can send data to the called function, it can also return any value to the calling function using return statement. This function can be written as-

```
int func(int,int);
main()
{
    int r;
    ........
    r=func(a,b);
    ........
    func(c,d);
}
int func(int a,int b )
{
    ........
    ........
    return (expression);
}
```

Here return statement returns the value of the expression to the calling function. The functions sum(), multiply(), max() that we had written earlier are examples of these types of functions. Let us take one more example program-

```
/*P6.14 Program to find the sum of digits of any number*/
#include<stdio.h>
int sum(int n);
main()
{
    int num;
    printf("Enter the number : ");
    scanf("%d",&num);
    printf("Sum of digits of %d is %d\n",num,sum(num));
}
int sum(int n)
{
    int i,sum=0,rem;
    while(n>0)
    {
        rem=n%10;        /*rem takes the value of last digit*/
        sum+=rem;
        n/=10;           /*skips the last digit of number*/
    }
    return (sum);
}
```

While describing the different type of functions, we have assumed arguments and return values of type int for simplicity. These values can be of any data type.