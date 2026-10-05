```
{
  char a[] = {'m','a','s','s','t','e','r','s'};
  printf("%d",sizeof(a));
  return 0;
}
```

# Prog 1:

```
#include<stdio.h>
int main()
{
  char a[] = "masters";
  printf("%d",sizeof(a));
  return 0;
}
```

Compare the output of prog 1 and prog 2.

+   (a) both 7
(b) both 8
(c) Prog 1: 7, Prog 2: 7
(d) Prog 1: 8, Prog 2: 7

# 11. What is the output of the following program?

```
#include "stdio.h"
int main()
{
  char array[100];
  int i;
  printf("%d", scanf("%s%d", array , &i));
  return 0;
}
```

Assume value given to scanf "India" and 10

+   (a) 9
(b) 2
(c) 10