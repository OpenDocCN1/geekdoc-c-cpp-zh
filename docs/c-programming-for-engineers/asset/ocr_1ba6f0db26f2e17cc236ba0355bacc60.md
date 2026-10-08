# 10.5. Passing Arrays to Functions

```
printf("Array elements: ");
for (int i = 0; i < size; i++) {
    printf("%d ", numbers[i]);
}
printf("\n");

int arraySum = sumArray(numbers, size);
printf("Sum of array elements: %d\n", arraySum);

return 0;
```

In this example, the sumArray function accepts two parameters: an integer array called arr and an integer named size. The size parameter specifies the total count of elements within the array. Utilizing this size information, the function traverses through the array elements, summing them up.

# 10.5.2 Using First Element as Size Indicator

In this approach, the first element of an array is used to indicate the size information. This is useful when the array size is fixed and known in advance.
Here is an example of using the first element as a size indicator:

```
#include <stdio.h>

int sumArray(int arr[]) {
    int size = arr[0];
    int sum = 0;
    for (int i = 1; i < size; i++) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    int numbers[] = {5, 1, 2, 3, 4, 5}; // First element indicates the size

    printf("Array elements: ");
    for (int i = 1; i <= numbers[0]; i++) {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    int arraySum = sumArray(numbers);
    printf("Sum of array elements: %d\n", arraySum);

    return 0;
}
```