The updated final solution can be expressed in the following program.

# NumberPatternDD3.c

```
```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display

    // Row level Repetitive Action :
    for ( int row = 0; row < totalRows; row++ ) {

        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        // Action2.print character

        // spaces to be printed before printing numbers
        for ( int col = totalRows; col >= 1; col-- ) {

            if ( col <= ( totalRows - row ) ) {
                printf( "%d ", col );
            } else {
                printf( "  " );
            }
        }

        // move control to the next line
        printf( "\n" );
    }

    return 0;
}
```
```

# Output

```text
5 4 3 2 1
  4 3 2 1
    3 2 1
      2 1
        1
```