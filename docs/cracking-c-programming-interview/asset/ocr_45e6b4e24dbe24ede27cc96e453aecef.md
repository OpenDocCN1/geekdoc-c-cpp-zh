(a) error- compile time in structure declaration

(b) error- compile time in assignment in L1

(c) 1 16

(d) 1 8

# 48. What is the output of the following program?

```
#include<stdio.h>
struct student{
    int a : 4;
    int b : 5;
} sl;
int main()
{
    sl.a = 10;
    sl.b = 17;
    char *p = &sl;
    printf("%d", *p);
    p++;
    printf("%d", *p);
    return 0;
}
```

(a) 10 17

(b) 41 64

(c) 26 1

(d) 41 17

# 49. What is the output of the following program?

```
#include<stdio.h>
struct student{
    int SN;
    char grade ;
} sl;
int main()
{
    sl.SN = 1;
```