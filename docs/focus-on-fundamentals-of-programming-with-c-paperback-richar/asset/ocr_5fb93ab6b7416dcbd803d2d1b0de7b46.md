```
// array5.c
// Function rmodifies elements of array that is passed by reference
void updateArray(int x[], int size) {
    int i;

    for (i = 0; i < size; ++i) {
        x[i] = i * -2;
    }
}
```

The program output looks like this:

| Before: | 0 | 10 | 20 | 30 | 40 | 50 | 60 | 70 | 80 | 90 |
|---|---|---|---|---|---|---|---|---|---|---|
| After: | 0 | -2 | -4 | -6 | -8 | -10 | -12 | -14 | -16 | -18 |

# Example: Function to sum array elements.

Our function to sum the elements of an array required that we iterate through the array visiting each array element. As we visit each array element, we place its contents into a summation variable. We must be sure to initialize the summation variable to zero before using it!!

Once again we want our function to sum arrays of different sizes so we must pass the array size as an additional argument to the function.

```
// sumElements.c
// Function to sum array elements
int sumArray(int num[], int size) {
    int i, sum = 0;

    for (i = 0; i < size; ++i) {
        sum += num[i];
    }
    return(sum);
}
```

# Example: Output array with format.

Suppose we wanted to write a function that prints `max` elements of an array `num`, 10 per line, with each column separated by one blank, and with each line (including the last) terminated by exactly one new line.