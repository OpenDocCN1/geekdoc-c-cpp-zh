# Nested for Loops

There are times when we have a need to place a `for` loop within the body of another `for` loop. This is referred to as a nested `for` loop. Can you follow the flow of control of the nested `for` loop below:

```
// nest.c
#include <stdio.h>
int main(void) {
    int i, j;
    for (i = 1; i <= 4; ++i) {
        for (j = 1; j <= 3; ++j) {
            printf("%d %d\n", i, j);
        }
    }
    return 0;
}
```

Here's the output that gets produced:

```
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
4 1
4 2
4 3
```