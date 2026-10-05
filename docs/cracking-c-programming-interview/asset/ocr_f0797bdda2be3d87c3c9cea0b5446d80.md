(d) error- run time

# 5. What is the output of the following program?

```
#include<stdio.h>
#include<stdlib.h>
int main() {
    int *p = NULL;
    p = (int*)malloc(sizeof(int));
    *p = 10;
    free(p);
    int *q = (int*)malloc(sizeof(int));
    *q = 15;
    printf("%d, %d\n", *p, *q);
    return 0;
}
```

(a) 10, 15

(b) 15, 15

(c) error- run time

(d) 0, 15

# 6. What is the output of the following program? Assumption: address of p is 1000 and q is 2000.

```
#include<stdio.h>
#include<stdlib.h>
void *fun(int **q) {
    int r = 20;
    **q=r;
    printf("%u ", *q);
}
int main() {
    int *p = (int*)malloc(sizeof(int));
    *p = 55;
```