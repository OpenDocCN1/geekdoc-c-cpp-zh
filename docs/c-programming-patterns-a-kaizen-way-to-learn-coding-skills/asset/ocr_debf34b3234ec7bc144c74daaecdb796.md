Now, test for different number of lines, let change it to be 7 and execute it. It should work correctly.

```
**NumberPattern10.C**

```c
#include <stdio.h>
int main() {

    int  totalRows = 7;  //number of rows to display

    for( int row = totalRows ; row >=1 ; row -- ) {

        // spaces to be printed
        for( int col = 1; col <= ( totalRows - row ); col++ ) {
            printf( "  " );
        }

        // row value to be printed
        for( int num=1; num<= row ; num++ ){
            printf( "%d", row);
        }// inner for-loop

        printf("\n");// moves control to the next line
    }// outer for-loop
    return 0;
}
```
```

```
**Output**

```text
7 7 7 7 7 7
  6 6 6 6 6
    5 5 5 5
      4 4 4
        3 3
          2 2
            1
```
```