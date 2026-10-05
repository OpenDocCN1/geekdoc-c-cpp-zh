+   (b) error- run time
(c) john
(d) garbage

# 19. What is the output of the following program?

+   (a) garbage
(b) 10 20
(c) 10 10
(d) error- link time

# 20. What is the output of the following program?

```
#include<stdio.h>
extern int i;
int main()
{
    extern int i; //line 1
    i = 10; //line 2
    printf("%d",i);
    return 0;
}
```

+   (a) 10
(b) error due to line 2
(c) garbage
(d) 0