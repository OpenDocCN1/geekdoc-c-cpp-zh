For example:

```
// address.c

#include <stdio.h>

int main(void) {
    int x = 5;
    printf("*x = %d\t &x = %p\n", x, &x);
}
```

prints both the value of variable x as well as its address in memory. The output will be similar to:

```
x = 5   &x = FFFFFFF4
```

int x[5];

const pointer
*always the first value of the array !!!

*(x+1) == x[1]
2nd element

int x[5];
int *V;
V = x;
V++
=> *V 则是指第 2 element
*V++