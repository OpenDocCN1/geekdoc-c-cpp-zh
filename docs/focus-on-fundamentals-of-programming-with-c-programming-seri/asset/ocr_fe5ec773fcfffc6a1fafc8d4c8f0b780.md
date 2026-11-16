```
// findMaxValue2.c

#include <stdio.h>

int findMax(int num, int value);

int main (void) {
    int num, value, max;

    num = 5;
    value = 1000;

    max = findMax(num, value);
    printf("The first power of %d larger than %d is %d.\n", num,
           value, max);
    return 0;
}

int findMax(int num, int value) {
    int product = num;

    while (product <= value) {
        product *= num;
    }

    return product;
}
```

Here's the output produced:

The first power of 5 larger than 1000 is 3125.

# Counter Controlled Loops

A counter controlled loop repeats a series of executable statements a specified number of times using a variable to count the number of loop iterations completed.

+   • The number of times that the loop body will be repeated must be known before checking the loop condition the first time and must not be changed within the loop body.

+   • The counting variable must be initialized to a known value before checking the loop condition the first time.