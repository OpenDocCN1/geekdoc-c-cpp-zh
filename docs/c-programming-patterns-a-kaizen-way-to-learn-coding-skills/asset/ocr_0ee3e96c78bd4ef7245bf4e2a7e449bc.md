# # NumberPatternBBB1.c

```
```c
#include <stdio.h>
int main() {

    int totalRows = 5;  //number of rows to display

    // Row level Repetitive Action :
    for( int row = 1 ; row <= totalRows ; row ++ ) {

        // Column level Repetitive Action :
        // 1)Move cursor in the same row. 2)print character

        // spaces to be printed before printing numbers
        for( int col = 1 ; col <= (totalRows - row) ; col++ ) {
            printf("  ");
        }

        for( int num = ( 2*row - 1 ) ; num >= row ; num-- ) {
            // added extra space for clarity in output.
            printf( "%d ", num );
        }

        printf("\n");// moves control to the next line

    }

    return 0;
}
```
```

# # Output

```
```text
        1
      3 2
    5 4 3
  7 6 5 4
9 8 7 6 5
```
```