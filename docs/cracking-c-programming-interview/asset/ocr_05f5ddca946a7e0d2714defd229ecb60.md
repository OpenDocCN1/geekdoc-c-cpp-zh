```
#include<stdio.h>
int main()
{
    printf("%d\t",sizeof(0.5));
    printf("%d\t",sizeof(9000));
    printf("%d\t",sizeof('X'));
    return 0;
}
```

+   (a) 4 4

+   (b) 4 4

+   (c) 4 4 1

+   16. Consider the following declarations of enum. Choose the correct one

+   (i) enum college {student, teacher, staff}x;

+   (ii) enum college {student, teacher, staff};

+   (iii) enum {student, teacher = -5, staff}x;

+   (iv) enum x {student, teacher, staff};

+   (a) i, iv

+   (b) ii, iii

+   (c) i, iii, iv

+   (d) i, ii, iii, iv

# 17. What is the output of the following program?

```
#include<stdio.h>
int main()
{
    signed x;
    unsigned y;
    x = 10 +- 10u +- 10u +- 10;
    y = x;
    if(x==y)
        printf("%d",x,y);
```