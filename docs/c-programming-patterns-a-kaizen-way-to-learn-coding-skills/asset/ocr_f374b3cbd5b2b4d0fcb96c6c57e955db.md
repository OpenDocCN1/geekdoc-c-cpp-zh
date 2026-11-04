# ***Let’s convert steps into C program.***

`Pattern1A_1.c`

```
```c
#include <stdio.h>

int main() {

    printf("*");   // print * character 1 time
    printf("\n"); // Move cursor to the next row

    printf("*");
    printf("*");   //print * characters 2 times, same row
    printf("\n"); // Move cursor to the next row

    printf("*");
    printf("*");
    printf("*");   // print * characters 3 times, same row
    printf("\n"); // Move cursor to the next row

    printf("*");
    printf("*");
    printf("*");
    printf("*");   //print * characters 4 times, same row
    printf("\n"); // Move cursor to the next row

    printf("*");
    printf("*");
    printf("*");
    printf("*");
    printf("*");   //print 5 times, same row
    printf("\n"); // Move cursor to the next row

    return 0;

}
```
```

# Output

```
```
*
**
***
****
*****
```
```

This solution will fail in a situation if we want to dynamically increase the total number of rows to 7,10,15...and so on. Whenever we execute this program will always get fixed output of 5 rows

There are two kinds of statements that are get ***repeated many times*** in the program.

`printf("*");`    and  `printf("\n");`

Repetition means directly we need to think about ***for-loop***. Hence we can use it for the same.

Let’s try to deep dive how the ***for-loop*** should be constructed in order to match our targeted output. We will do the reverse engineering. By observing the pattern’s output we try to build the logic.