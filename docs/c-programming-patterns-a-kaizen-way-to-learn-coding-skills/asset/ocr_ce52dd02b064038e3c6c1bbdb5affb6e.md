Let's execute the following program.

```
```c
PatternG1.c

#include <stdio.h>
int main() {

    int totalRows = 5; // number of rows to display

    for (int row = 1; row <= (2 * totalRows - 1); row++) {

        if (row <= totalRows) {
            for (int col = 1; col <= row; col++) {
                printf("* ");
            }
        } else {
            for (int col = 1; col <= (2 * totalRows - row); col++) {
                printf("* ");
            }
        }
        printf("\n");
    }
    return 0;
}
```
```

```
```text
Output

*
* *
* * *
* * * *
* * * * *
* * * *
* * *
* *
*
```
```

The <u>inner for-loop 1</u> and <u>inner for-loop 2</u> differ only in the maximum limit value of the **col** variable.

It will be better if we capture maximum limit of **col** variable in a different variable.

Then we will be in a position to use only one inner for-loop for the complete column level repetition.