```
```c
int main()
{
    int i = 15;
    printf("Factorial of %d is %d\n", i, factorial(i));
    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
Factorial of 15 is 2004310016
```
```

# Fibonacci Series

The following example generates the Fibonacci series for a given number using a recursive function:

```
```c
#include <stdio.h>

int fibonacci(int i)
{
    if(i == 0)
    {
        return 0;
    }
    if(i == 1)
    {
        return 1;
    }
    return fibonacci(i-1) + fibonacci(i-2);
}

int main()
{
    int i;
    for (i = 0; i < 10; i++)
    {
        printf("%d\t% n", fibonacci(i));
    }
```
```