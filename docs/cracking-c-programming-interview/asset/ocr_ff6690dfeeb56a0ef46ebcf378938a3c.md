```
int i=10, j=6;
printf("%d\n", i++j);
return 0;
}
```

+   (a) 17

+   (b) 16

+   (c) error-compile time

+   (d) None of these

# 27. What is the output of the following program?

```
#include<stdio.h>
int main()
{
  void *p;
  int i=20;
  p = &i;
  void *q = p; //line 4
  printf("%d, %d, %d\n", i, *p, *q); //line 5
  return 0;
}
```

+   (a) 20, 20, 20

+   (b) 20, g, g

+   (c) compiler error at line 4

+   (d) compiler error at line 5

# 28. What is the output of the following program?

```
#include<stdio.h>
int main()
{
  int a[] = {10, 20, 30, 40, 50};
  printf("%u %u %u", sizeof(a[1]), sizeof(a), sizeof(a));
  return 0;
}
```

+   (a) 4 8 20