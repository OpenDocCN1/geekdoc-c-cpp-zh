(d) error- compile time

52. What is the output of the following program? Suppose the base address of an array 'a' is 1000?

```
#include<stdio.h>
int main()
{
 int a[] = {5, 6, 7, 8, 9, 10};
 int *p = &a;
 int *q = &a+1;
 printf("%u %u \ a, p);
 printf("%u %u \ a+1, q);
 return 0;
}
```

+   (a) 1000 1000 1001 1001
(b) 1000 1000 1004 1004
(c) 1000 1000 1004 1020
(d) 1000 1000 1004 1024

53. What is the output of the following program?

```
#include<stdio.h>
int main()
{
 char *str1 = "hello India";
 char *str2 = "how are you";
 strcpy(str1, str2);
 printf("%s", str1);
 return 0;
}
```

+   (a) how are you
(b) hello India
(c) error- compile time
(d) error- run time

54. What is the output of the following program?