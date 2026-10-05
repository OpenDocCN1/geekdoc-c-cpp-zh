+   (a) 8
(b) 6
(c) error- compile time
(d) error- run time

# 26. What is the output of the following program ?

```
#include<stdio.h>
#define fun1 fun2
#if x == 1
#define fun2 fun3
#else
#define fun2 fun4
#endif

int main()
{
    int fun3 = 3 , fun4 = 4;
    fun1 = fun2 + fun1;
    printf("%d",fun);
    return 0;
}
```

+   (a) 8
(b) 6
(c) error- compile time
(d) error- run time

# 27. What is the output of the following program? Let the address of main() function be 0x1000.

```
#include<stdio.h>
#define abc main
int main()
{
    int abc = 10;
    printf("the value of abc : %d",abc);
    return 0;
}
```