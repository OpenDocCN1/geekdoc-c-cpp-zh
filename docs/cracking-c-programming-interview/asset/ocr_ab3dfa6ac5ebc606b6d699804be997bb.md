# Your intention is superior than hard work.

# Group-4 Questions

# Number of 'C' Question: 60

# Other Important Interview Questions: 15

![](bbox=[0.353, 0.307, 0.646, 0.483])

1. What is the output of the following program?

```
//basic function pointer example
#include<stdio.h>
int fun(int x, int y)
{
    int z = x*y+x+y*x-y;
    return z;
}
int main()
{
    int (*fun_ptr) (int, int); //line 1
    fun_ptr = fun;
    int x = (int)fun_ptr(1, 2);
    printf("%d", x);
    return 0;
}
```

(a) 3