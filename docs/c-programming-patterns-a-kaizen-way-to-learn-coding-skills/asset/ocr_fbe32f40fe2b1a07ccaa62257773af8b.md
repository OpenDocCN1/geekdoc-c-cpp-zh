Now, test for different number of lines, let it be 7. It should work correctly.

# NumberPattern2C.c

```
```c
#include <stdio.h>
int main() {
    int totalRows = 7; //number of rows to display
    for( int row = totalRows ; row >= 1 ; row -- ) {
        // row value to be printed
        for(int col = 1 ; col <= row ; col++) {
            printf( "%d ", row );
        }// inner for-loop
        printf("\n");// moves control to the next line
    }// outer for-loop
    return 0;
}
```
```

# Output

7 7 7 7 7 7 7
6 6 6 6 6 6
5 5 5 5 5
4 4 4 4
3 3 3
2 2
1