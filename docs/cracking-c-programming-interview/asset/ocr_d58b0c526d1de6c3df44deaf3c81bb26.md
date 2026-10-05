```
#include<stdio.h>
void fun(int *p)
{
    printf("%d, %d, %d", p[2], p[3], p[4]);
}
int main()
{
    int a[5] = {3, 1, 5, 4, 2};
    int p[4];
    //p = a;
    int *ptr = a;
    fun(a);
    fun(&a);
}
```

+   (a) 5, 4, 2
(b) 5, 4, 2, 5, 4, 2
(c) 2, 5, 4, 2, 5, 4
(d) error- compile the above program if we uncomment the commented line p = a;

38. **What will be the output of the above program if we uncomment the commented line p = a;**

+   (a) same output
(b) error- base address of an array cannot be updated

39. **What will be the output of the following program?**

```
#include<stdio.h>
int main()
{
    int a[4] = {5, 6, 7, 8};
    int *p = a+3;
    printf("%d ", p[-2]);
    return 0;
}
```

+   (a) 8
(b) 6