Let's execute the following program.

# PatternE1.c

```
```c
#include <stdio.h>
int main() {
    int totalRows = 5; // total number of rows to display
    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = 0; row < totalRows; row++) {
        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        for (int col = 1; col <= (totalRows + row); col++) {
            if (col >= (totalRows - row)) {
                // Action2.prints star "*" character
                printf("* ");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }
        }// inner for-loop
        printf("\n");// Move cursor to the next row
    }// outer for-loop
    return 0;
}
```
```

# Output

*
* * *
* * * * *
* * * * * * *
* * * * * * * * *