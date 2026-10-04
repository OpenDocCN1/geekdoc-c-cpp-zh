```
return 0;
}
```

# 129. Write a program that fills a 4x4 matrix with random numbers and displays the sum of the values present in each row and in each column.

```
#include <iostream>
#include <ctime>
#include <cstdlib>

int main() {
    const int SIZE = 4;
    int matrix[SIZE][SIZE];
    int rowSum[SIZE] = {0};
    int colSum[SIZE] = {0};

    // Seed random number generator
    srand(time(0));

    // Fill matrix with random numbers and display
```