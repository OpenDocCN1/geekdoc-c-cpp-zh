# ## 5.9 Answers for Terminal Questions

+   1. `void` is the keyword used to specify that the function doesn’t return any value. It can also be used to specify the absence of arguments.
+   
+   2. Function declaration is a direction to the compiler that what type of data is returned by the function, the function name and about the arguments whereas the function definition is actually writing the body of the function along with the function header.

```
```c
#include<stdio.h>
main()
{
    int n=10;
    int fun(int n);
    printf("%d", fun(n));
}
int fun(int n)
{
    if(n>0) return (n+fun(n-2));
}
```
```

+   4. `gcd(m,n) = { m or n if m = n
+      GCD(m, m-n) if m > n
+      GCD(n,m) if m < n }`

+   5. `fib(i) = { 0 if i = 1
+      1 if i = 2`