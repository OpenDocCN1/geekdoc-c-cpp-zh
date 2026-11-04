![](bbox=[0.1, 0.07, 0.95, 0.5])

# NestedForLoop.c

```
#include <stdio.h>
int main() {
    for( int out = 1 ; out <= 2 ; out++ ) {
        printf("OUTER count No.%d\n", out);
        // nested for-loop: always re-starts and finishes
        // completely for every new value of outer for-loop.
        for( int in = 1; in <= 3; in++ ) {
            printf(" <INNER> count No.%d\n", in );
        }
    }
    return 0;
}
```

# Output

OUTER count No.1
<INNER> count No.1
<INNER> count No.2
<INNER> count No.3
OUTER count No.2
<INNER> count No.1
<INNER> count No.2
<INNER> count No.3