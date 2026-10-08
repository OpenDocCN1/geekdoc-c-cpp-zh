```
int calculate_ratio(int a, int b) {
    // Implicit conversion of result back to int before returning
    return (float)a / b;
}
```

```
int ratio = calculate_ratio(10, 3);

printf("Ratio: %d\n", ratio); // Output: 3
```

In this example, the calculate_ratio performs division using float operands. However, the result is implicitly converted to an int, the function has an int return type, discarding the fractional part. As a result, the output is 3 because the fractional part is discarded during conversion.

These examples demonstrate how C handles implicit type conversion during function calls and returns. Implicit conversions may result in loss of precision or truncation of fractional components. It is important to understand implicit conversions to avoid unexpected behavior. If desired, explicit casts can be used to perform manual type conversions instead of relying on implicit conversions.

# 10.5 Passing Arrays to Functions

In C, arrays are often used to store and manipulate collections of data. When an array is passed to a function, the function only receives a pointer to the first element, the size. There are multiple ways to indicate the size of the array such as passing the size as a separate parameter, using sentinel values, or employing the first element as a size indicator.

# 10.5.1 Passing Array Size as a Separate Parameter

The most common approach to passing the size of an array to a function is to use a separate parameter. This explicitly specifies the size of the array and allows the function to iterate over the elements based on the provided size.

Here is an example of passing the array size as a separate parameter:

```
#include <stdio.h>

int sum(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    return sum;
}
```

```
int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]);
```