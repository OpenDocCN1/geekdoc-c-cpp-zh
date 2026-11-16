# Bitwise And

Similar to the logical AND operator (`&&`), the bitwise-and operator (`&`) produces a true value only if both operands are true (i.e., have non-zero values).

| b1 | b2 | b1 & b2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

We assume a 16-bit integer:

```
// and1.c

#include <stdio.h>

int main(void) {
    int x = 0x2719;   // 0010 0111 0001 1001
    int y = 0x35CD;   // 0011 0101 1100 1101
    int z;

    z = x & y;        // 0010 0101 0000 1001
    printf("z = 0x%x\n", z);
    return 0;
}
```

The output of this program is:

```
z = 0x2509
```

Note that each of the corresponding bits within each `int` variable are bit-anded together.