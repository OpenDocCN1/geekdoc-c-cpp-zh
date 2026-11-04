Let's execute the following program.

# NumberPattern1F.c

```
#include <stdio.h>
int main() {
    int totalRows = 7; // number of rows to display
    int num;
    // Row level Repetitive Action:
    for ( int row = 1; row <= totalRows; row++ ) {
        // Column level Repetitive Action:
        // print the value of variable num column-wise
        for ( int col = 1; col <= row; col++ ) {
            if ( row % 2 == 1 ) {
                num = 1;
            } else {
                num = 0;
            }
            printf( "%d ", num );
        } // inner loop
        printf( "\n" );// Moves cursor to the next row
    } // outer loop
    return 0;
}
```

# Output

1
0 0
1 1 1
0 0 0 0
1 1 1 1 1
0 0 0 0 0 0
1 1 1 1 1 1 1