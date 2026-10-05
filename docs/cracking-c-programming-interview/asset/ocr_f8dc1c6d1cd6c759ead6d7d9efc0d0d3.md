```
printf("origin is (%d, %d)\n",pp->x,pp->y);
return 0;
}
```

+   (a) origin is (0, 0) origin is (0, 0)
(b) origin is (1, 1) origin is (1, 1)
(c) origin is(garbage, garbage)
(d) error- compile time

# 3. What is the output of the following program?

```
#include<stdio.h>
int _l_abc(int i) {
  return(i++);
}
int main() {
  int i=\_l_abc(10);
  printf("%%d\n",i);
  return 0;
}
```

+   (a)-10
(b) 9
(c) garbage
(d) error- invailid function name

# 4. What is the output of the following program?

```
#include<stdio.h>
int main() {
  char *p;
  int *q;
  long *r;
  p=q=r=0;
```