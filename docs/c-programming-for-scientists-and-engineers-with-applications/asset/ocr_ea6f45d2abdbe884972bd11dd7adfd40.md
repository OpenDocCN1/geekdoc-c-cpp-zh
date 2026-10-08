Notice that the storage class must be specified first and then data type followed by a variable name. The following examples show the proper declaration of variables.

```
auto int x;
extern int Y;
static int Z;
register int W;
```

# 6.2.1 Storage Class auto

Storage class auto is the default storage class. All local variables declared inside a block are of the auto storage class. The explicit declaration of an auto storage class variable is as follows:

```
auto int x;
```

which, is the same as: int x;
Auto storage class variable need not be given a value when it is declared. However such a variable must be given a value before its value is used. An auto variable may be given a value in a declaration statement or through an assignment statement or through an input statement. The following examples show the declaration and use of auto class variables.

```
#include <stdio.h>
int funccl(int, int);
int main() {
    int x = 10, y = 5, z;
    z = funccl(x, y);
    printf("x = %d y = %d z = %d\n", x, y, z);
    return 0;
}
int funccl(int a, int b) 
funccl() {
    int c;
    c = a + b;
    return c;
}
```

| x | y | z |
| 10 | 5 | 15 |

| c |
| 15 |