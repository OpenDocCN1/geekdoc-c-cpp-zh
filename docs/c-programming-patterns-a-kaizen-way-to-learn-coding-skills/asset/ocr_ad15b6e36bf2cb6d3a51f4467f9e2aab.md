Let's try to execute the following program.

# NumberPattern3D.c

```
#include <stdio.h>
int main() {
    int totalRows = 5; //number of rows to display

    for( int row = totalRows ; row >=1 ; row-- ) {

        for( int col = totalRows; col >= 1 ; col-- ) {

            if( col <= row ) {
                // row value to be printed
                printf( "%d ", row );
            }else {
                // spaces to be printed
                printf( " " );
            }

        }
        printf("\n");// move control to the next line
    }

    return 0;
}
```

# Output

5 5 5 5 5
  4 4 4 4
    3 3 3
      2 2
        1