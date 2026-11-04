Let’s execute the following program.

# NumberPatternDDD1.c

```
```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display
    int num;

    // Row level Repetitive Action :
    for ( int row = totalRows; row >= 1; row-- ) {

        // Column level Repetitive Action :
        // 1)Move cursor in the same row.
        // 2)print space characters before number.
        for ( int col = 1; col <= ( totalRows - row ); col++ ) {
            printf( "  " );// 2 spaces
        }// inner for-loop_1

        // num value to be printed
        for ( num = 2 * row - 1; num >= row; num-- ) {
            printf( "%d ", num );
        }// inner for-loop_2

        printf( "\n" );// Move cursor to the next row

    }// outer for-loop

    return 0;

}
```
```

# Output

```
```
9 8 7 6 5
  7 6 5 4
    5 4 3
      3 2
        1
```
```