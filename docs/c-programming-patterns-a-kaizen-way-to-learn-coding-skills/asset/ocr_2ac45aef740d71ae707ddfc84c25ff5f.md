# How to verify logical conditions?

Let's verify the logical condition of the alphabet M captured in 7 rows and 5 columns given as :

(col==1)||(col==5)||( ((row==col)||(row+col ==6) ) && row<=3 )

# VerifyAlphabetM.c

```
#include <stdio.h>

int main() {
    int TOTAL_ROWS = 7;
    int TOTAL_COLUMNS = 5;
    int condition; //logical condition variable
    for ( int row = 1; row <= TOTAL_ROWS; row++) {
        for ( int col = 1; col <= TOTAL_COLUMNS; col++) {
            condition = (col == 1) || (col == 5) ||
                ( (row == col) || (row + col == 6) )
                && row <= 3 );
            // space(s) are used just to show formatted output.
            if (condition) {
                printf("* "); // single space
            } else {
                printf("  ");// double space
            }
        }
        printf("\n");// Move cursor to the next row
    }
    return 0;
}
```

# Output

*   *
* *  *
* *  *
*   *
*   *
*   *
*   *