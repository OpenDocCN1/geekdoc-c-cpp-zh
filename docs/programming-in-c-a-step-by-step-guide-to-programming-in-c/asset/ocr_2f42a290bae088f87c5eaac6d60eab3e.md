automatic variables, but, however it is optional. If another function somewhere else declares a local variable with the same name, it's a different variable entirely, and the two don't clash with each other. If an automatic variable is not initialized in some manner, however, its initial value will be unpredictable and contains some garbage value.

# Program 6.1: Program to find factorial of a number

```
#include<stdio.h>
main()
{
auto int n; /* Here the keyword auto is optional */
long int fact(int);
printf("read the integer n:");
scanf("%d", &n);
printf("\nn!=%ld", fact(n));
}
long int fact(auto int n) /* n is local to the function fact() and auto is optional */ {
auto int i; /* Here the keyword auto is optional */
auto long int factorial=1; /* Here the keyword auto is optional */ while(n>0)
{
factorial=factorial*n;
n=n-1;
}
return factorial;
}
```