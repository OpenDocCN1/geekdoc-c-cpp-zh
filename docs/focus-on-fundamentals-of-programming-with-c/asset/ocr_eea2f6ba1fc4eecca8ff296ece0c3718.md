# Bitwise Exclusive-Or

The bitwise exclusive-or operator produces a 1 when the two operands are of a different value and produced a 0 when the two operands are the same.

| b1 | b2 | b1 ^ b2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

For example:

```
// xor1.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;
    int y = 0x85CD;
    int z;
    z = x ^ y;
    printf("z = 0x%x\n", z);
    return 0;
}
```

The output of this program is:

```
z = 0x97F9
```

Note that any value exclusive-ored with itself produces 0:

```
// xor2.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;
    printf("x = 0x%x\n", x ^ x);
    return 0;
}
```