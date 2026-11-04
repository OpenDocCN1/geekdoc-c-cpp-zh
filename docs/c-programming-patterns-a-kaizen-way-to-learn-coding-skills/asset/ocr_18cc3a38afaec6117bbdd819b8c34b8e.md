# Row Level Repetitive Action

Outer for-loop starts at row=0 & will repeat till row <= totalRows − 1 or row < totalRows.

| Elements Of Row Level for-loop |
|---|---|
| min_val | 0 |
| max_val | totalRows |
| variable_name | row |
| Loop condition | row < totalRows |
| statement(s) | Column level for-loop
printf("\n");// Moves cursor to the next row |

The new solution changes are in the following program.

# PatternB2.c

```
#include <stdio.h>
int main() {
    int totalRows = 5;  //number of rows to display
    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for( int row = 0 ; row < totalRows ; row ++ ) {
        // Column level Repetitive Action :
        for(int col = 1 ; col <= ( totalRows - row ) ; col++) {
            // Action1.Move cursor in the same row
            // Action2.print "*" character
            printf("* ");
        }
        printf("\n");// Move cursor to the next row
    }
    return 0;
}
```

# Output

* * * * *
* * * *
* * *
* *
*