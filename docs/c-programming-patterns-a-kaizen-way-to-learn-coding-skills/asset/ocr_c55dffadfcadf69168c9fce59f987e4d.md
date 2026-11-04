Let's execute the following program.

# PatternH2_1.c

```
#include <stdio.h>
int main() {
    int totalRows = 4; //number of rows to display

    // Row level Repetitive Action :
    // Executes Repetitive Action at Column level and
    // then Move control to  next row.
    for (int row = 1; row <= (2 * totalRows - 1); row++) {
        //1st half : Column level Repetitive Action :
        if (row <= totalRows) {
            for (int col = 1; col <= (totalRows + row - 1); col++) {
                if (col >= (totalRows - row + 1)) {
                    printf("* ");
                } else {
                    printf("  ");
                }
            }//inner for-loop_1
        }
        // 2nd half : Column level Repetitive Action :
        if (row > totalRows) {
            for (int col = 1; col <= (3 * totalRows - row - 1); col++) {
                if (col >= (row - totalRows + 1)) {
                    printf("* ");
                } else {
                    printf("  ");
                }
            }//inner for-loop_2
        }
        printf("\n");// Move cursor to next row.
    }// outer for-loop

    return 0;
}
```

# Output

   *
  * *
 * * * *
* * * * *
 * * * *
  * *
   *