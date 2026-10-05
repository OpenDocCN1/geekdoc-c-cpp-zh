+   (a) 1
(b) 10
(c) error due line1
(d) error due line2

# 23. What is the output of the following program?
Two files are given as one.c and two.c.

```
one.c
----
#include<stdio.h>
extern int i;
int i = 10;
extern int p;
int main() {
    extern int i;
    printf("%d %d",i,p);
    return 0;
}
```

+   two.c
----
int p = 20;
(a) 10 20
(b) error- compile time in two.c for no header files and/or no main()
(c) error- compile time in one.c for invalid use of extern int i and/or extern int p
(d) error- run time

# 24. What is the output of the following program?
Two files are given as one.c and two.c one.c.

```
#include<stdio.h>
extern int i;
int i = 10;
extern int p;
```