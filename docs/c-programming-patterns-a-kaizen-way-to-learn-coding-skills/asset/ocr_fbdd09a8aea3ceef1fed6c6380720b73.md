# NumberPatternAAA.c

```
```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display

    // Row level Repetitive Action :
    for ( int row = 1; row <= totalRows; row++) {

        // Column level Repetitive Action:
        // 1)Move cursor in the same row. 2)print character
        for ( int col = row; col <= ( 2 * row - 1 ); col++ ) {

            // added extra space for clarity in output.
            printf( "%d ", col );

        }

        // move control to the next line
        printf( "\n" );

    }

    return 0;
}
```
```

# Output

```
```text
1
2 3
3 4 5
4 5 6 7
5 6 7 8 9
```
```

**ProblemGBAAA:** Modify program NumberPatternAAA.c so that it should show following output using switch-case for values 1 and 2 respectively.

```
```text
Output
──────────────
1
  3
3  5
5  7
5  7  9
```
```

```
```text
Output
──────────────
2
  4
4  6
6  8
```
```