```
#include<stdio.h>
int main()
{
    int a[3] = {5, 6, 7};
    char *c = (char *)a;
    printf("%d, %d, %d, %d\n", *c, c[0], c[1], c[2]);
    return 0;
}
```

+   (a) 0, 5, 0, 7
(b) 5, 5, 7, garbage
(c) 5, 5, 0, 0
(d) 5, 5, 0, garbage

# 26. What is the output of the following program?

```
#include<stdio.h>
#define FOO(x) foo(#x) //line 2
int foo(char *x)
{
    printf("%c %c", *x,x[1]); //line 4
}
int main()
{
    FOO(65); //line 8
    return 0;
}
```

+   (a) 5 6
(b) 7 8
(c) 6 5
(d) error-compile time

# 27. What is the output of the following program?

```
#include<stdio.h>
int main()
{
```