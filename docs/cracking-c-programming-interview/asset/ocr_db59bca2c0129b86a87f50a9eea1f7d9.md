```
return 0;
)
```

+   (a) India is great
(b) Love is great
(c) yes is great
(d) error- compile time

# 10. What is the output of the following program?

```
#include<stdio.h>
int main()
{
    char *str = "Love p\0eop\0le";
    printf("%ld %ld", sizeof(str), strlen(str));
}
```

+   (a) 6 6
(b) 7 6
(c) 13 6
(d) 4 6

# 11. Determine the output of the following program? Suppose the base address of an array is 1000.

```
#include<stdio.h>
int main()
{
    int a[2][3] = {2, 4, 7, 3, 2, 2, 3, 3, 4};
    printf("%u %u %u %d", a, *a, **a, ***a);
    printf("%u %u %u %d", a+1, *(a+1), ***(a+1);
    printf("%u %u %u %d\n", *(a+2)+3), *(a+2), *(*(a[1]+1));
    return 0;
}
```

# 12. Consider the following declarations