# Masks

Bitwise ANDing is frequently used for masking operations. A mask is a constant or variable that is used to extract desired bits in a variable or expression. A mask can be used to set specific bits of a data item to 0. In the example below, we'll preserve the rightmost two bits from x and zero (mask) out all of the other bits:

```
// mask1.c
#include <stdio.h>

int main(void) {
    int x = 0x679;    // 0000 0110 0111 1001
    int mask = 0x0003; // 0000 0000 0000 0011

    x = x & mask;      // 0000 0000 0000 0001
    printf("x = %#x\n", x);
    return 0;
}
```

The output produced is:

```
x = 0x1
```

Note that we could have written:

```
x &= mask;
```