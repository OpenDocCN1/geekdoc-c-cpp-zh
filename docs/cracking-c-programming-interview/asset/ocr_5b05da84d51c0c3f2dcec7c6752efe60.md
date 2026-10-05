```
int **ptr = &p2;
p2 = p1;
p3 = p2;
return 0;
)
```

+   (a) ptr points to x;
(b) ptr points to y;
(c) ptr points to z;
(d) compile time error

# 9. What is the output of the following program?

```
#include<stdio.h>
int main()
{
int a[5] = {50, 60, 70, 80, 90};
int *p = a;
int *q = &a[2];
p++;
int **ptr = p+1;
**ptr;
printf("%dd %d %d", p[2], *q, ptr[0]);
return 0;
}
```

+   (a) 80 70 70
(b) 80 71 71
(c) 80 74 74
(d) 80 5 6

# 10. Which of the following declaration throws run time error?

+   (a) int **ptr = &ptr;
(b) int **ptr = &ptr;
(c) int **ptr = **ptr;
(d) int **ptr = ptr;

# 11. What is the output of the following program?