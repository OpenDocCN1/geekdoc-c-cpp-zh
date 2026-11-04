# C.11.30 What is the output of the following program?

```
```c
#include <stdio.h>

void test(int *arg);

int var = 100;

int main(void)
{
    int *ptr, i = 30;

    ptr = &i;
    test(ptr);
    printf("%d\n", *ptr);
    return 0;
}

void test(int *arg)
{
    arg = &var;
}
```
```