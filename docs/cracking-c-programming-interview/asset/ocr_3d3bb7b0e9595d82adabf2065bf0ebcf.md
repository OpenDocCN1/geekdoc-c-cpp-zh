```
char **ptr[] = {str, str+2, str+1, str+3};
char ***p;
p = ptr;
p += 3;
printf("%s %s", (**)p)+2, *ptr[1]+'b'-'a' );
return 0;
}
```

+   (a) eat ello
(b) ve ndia
(c) lo ndia
(d) eat ove

60.

```
#include<stdio.h>
#include<stdlib.h>
int main()
{
    while(1)
    {
        int *p = (int *)malloc(sizeof(int));
        *p=10;
        printf("hello%d", *p);
    }
    return 0;
}
```

+   (a) "hello10" gets infinite time
(b) stack overflow
(c) heap overflow
(d) error- compile time

# Other important questions for the Interview are as follows:

+   1. Write a C program to count the number of digits in a given number.
2. Write a C program to find L.C.M. of two numbers.