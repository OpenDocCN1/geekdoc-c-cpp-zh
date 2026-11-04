1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
1 2 3 4
1 2 3
1 2
1

# NumberPatternGG1

# StringPatternGG1.c

```
```c
#include <string.h>
#include <stdlib.h>
#include <stdio.h>
int main() {
    int totalRows = 5; // number of rows to display
    int index = -1;   // array's index to increment by 1.
    char line1[44]={""}; // initialize with blank string.
    char line2[5]={""}; // initialize with blank string.

    for( int row = 1; row <= ( 2 * totalRows - 1 ); row++ ) {
        // Column level Repetitive Action :
        // expanding array by filling it up using '*' char.
        if ( row <= totalRows ) {
            ++index; // will track record of line1 array elements
            // convert num to string
            itoa(row, line2, 10);
            strcat( line1 , line2 ); // append strings
        } else {
            // replacing numeric character from the end
            // of the array a space character.

            // decrement index only when row > totalRows
            line1[index--] = ' ';
        }
        // Print string and move cursor to the next row
        printf("%s\n",line1);
    }
    return 0;
}
```
```

# Output

1
12
123
1234
12345
1234
123
12
1