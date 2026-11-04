# Alternative solution

Since the column values get clear split between printing spaces and numbers. We can try to reproduce the same result using if-else condition construct. Using the loop-condition for spaces as an if-condition and printing number in else-condition.

```
```c
NumberPatternDDD2.c
#include <stdio.h>
int main() {
    int totalRows = 5; // number of rows to display

    // Row level Repetitive Action :
    for ( int row = totalRows; row >= 1; row-- ) {
        int num = 2*row - 1 ;

        // Column level Repetitive Action :
        for ( int col = 1; col <= ( totalRows ); col++ ) {

            // when spaces are to be printed
            if ( col <= ( totalRows - row ) ) {
                printf( " " );
            } else {
                printf( "%d ", num );
                num--;
            }
        } // inner for-loop

        printf( "\n" );// Move cursor to the next row
    } // outer for-loop

    return 0;
}
```
```

# Output

9 8 7 6 5
 7 6 5 4
  5 4 3
   3 2
    1