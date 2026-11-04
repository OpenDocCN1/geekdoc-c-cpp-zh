Hence, our final if-condition will be;

| if-condition | `upper_limit >= col >= lower_limit` |
|---|---|
| Mathematical expression | `col <= (totalRows + 1 - row)` |
| Syntax | `if( col <= (totalRows + 1 - row) )` |

# NumberPatternDD2.C

```
```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display

    // Row level Repetitive Action :
    for ( int row = 1; row <= totalRows; row++ ) {

        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        // Action2.print character

        // spaces to be printed before printing numbers
        for ( int col = totalRows; col >= 1; col-- ) {

            if ( col <= ( totalRows + 1 - row ) ) {
                printf( "%d ", col );
            } else {
                printf( "  " );
            }

        }// inner for-loop

        printf( "\n" );// moves control to the next line

    }// outer for-loop

    return 0;
}
```
```

# Output

```
```
5 4 3 2 1
  4 3 2 1
    3 2 1
      2 1
        1
```
```