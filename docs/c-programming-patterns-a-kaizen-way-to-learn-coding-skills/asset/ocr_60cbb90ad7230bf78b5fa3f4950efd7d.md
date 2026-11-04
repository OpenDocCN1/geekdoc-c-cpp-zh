Now, test for different number of lines, let it be 7. It should work correctly, so that we can be confirmed that our solution is generalised and fit for any number of lines.

# NumberPattern1B.c

```
```c
#include <stdio.h>
int main() {

    int totalRows = 7;  //number of rows to display

    for( int row = 1; row <= totalRows ; row ++ ) {

        // spaces to be printed before printing numbers
        for(int col = 1 ; col <= (totalRows - row) ; col++) {
            printf( " " );
        }

        for(int num = row; num >= 1 ; num--) {

        // added extra space for clarity in output.
            printf("%d ", num );
        }

        printf("\n");// move control to the next line
    }
    return 0;
}
```
```

# Output

```
```
          1
        2 2
      3 3 3
    4 4 4 4
  5 5 5 5 5
6 6 6 6 6 6
7 7 7 7 7 7 7
```
```