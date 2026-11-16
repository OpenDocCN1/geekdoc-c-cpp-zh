We can output the contents of our two-dimensional array as follows:

```
```c
// 2d5.c

#include <stdio.h>

int main(void) {
    int i, j, num[3][4] = {
        { 2, 4, 6, 8 },
        { 1, 3, 5, 7 },
        { 3, 6, 9, 12 }
    };

    for (i = 0; i < 3; ++i) {
        for (j = 0; j < 4; ++j) {
            printf("%4d", num[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
```

Our output looks like this:

| 2 | 4 | 6 | 8 |
|---|---|---|---|
| 1 | 3 | 5 | 7 |
| 3 | 6 | 9 | 12 |

# Two-Dimensional Array of Characters

The declaration for a two-dimensional array of characters must include the extra space for a null terminator if each row is to be treated as a character string:

```
```c
// 2d6.c

char name[20] [31];
```
```

This declares a two-dimensional array of 20 rows, each to contain 30 data characters plus the null terminator that the compiler appends to each string. The data is stored in row-major order, which means that each row forms an array or items in memory. Each row is itself a one-dimensional array and can be used in contexts where an array is allowed.