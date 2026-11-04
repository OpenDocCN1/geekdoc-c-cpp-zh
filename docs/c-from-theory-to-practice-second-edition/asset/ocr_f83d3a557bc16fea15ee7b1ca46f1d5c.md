U.8.16 Write a program that uses two pointers to two pointer variables to read two integers and swap their values.

U.8.17 What does the following program do?

```
```c
#include <stdio.h>

#define COLS 4

int main(void)
{
    int i, arr[] [COLS] = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120, 130, 140, 150, 160};

    for(i = 0; i < COLS; i++)
        *(arr[i]+i) = *(arr[i]+COLS-1-i) = 0;
    return 0;
}
```
```

U.8.18 Write a program that assigns random integers to a 5×5 array and checks if the sum of the elements in the main diagonal is equal to that of its secondary diagonal. Use pointer arithmetic to process the array.

U.8.19 Write a program that reads integers and stores them in a 5×5 array and displays the maximum sum stored in a column and the maximum sum in a row as well. Use pointer arithmetic to process the array.