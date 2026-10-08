This data is entered from the input device keyboard, as it is shown by rows, and output is displayed on the monitor, which is a standard output device. The code to input and output this data using array offset is as follows.

Nested loops are used to increment the array pointer by rows and by columns.

```
#include <stdio.h>
#define IMAX 3
#define JMAX 4

int main() 
{
    float values[IMAX][JMAX];
    int i, j;

    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            scanf("%f", *(values + i) + j));
        }
    }
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            printf("%5.2f ", *(values + i) + j));
        }
        printf("\n");
    }
    return 0;
}
```

As the computer does not check array bounds, if an array is stored in row-major order, an array pointer and a single loop can be used to input or output all elements of the array sequentially as in the following:

```
float values[IMAX][JMAX];
float *ptr, valuesend, i;
```