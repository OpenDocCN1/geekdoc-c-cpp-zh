+   2. int fun(int *a[2])
(a) No
(b) Yes

# 45. What is the output of the following program?

```
#include<stdio.h>
int main()
{
  int x=300;
  char *p = &x;
  ++p=2;
  printf("%d",x);
  return 0;
}
```

+   (a) 300
(b) 554
(c) 301
(d) 556

# 46. What is the output of the following program?

```
#include<stdio.h>
int main()
{
  int i = 258;
  int *ptr = &i;
  printf("%d %d", *((char*)ptr), *((char*)ptr+1));
  return 0;
}
```

+   (a) 255 0
(b) 255 3
(c) 0 0
(d) 2 1

# 47. What is the output of the following program?