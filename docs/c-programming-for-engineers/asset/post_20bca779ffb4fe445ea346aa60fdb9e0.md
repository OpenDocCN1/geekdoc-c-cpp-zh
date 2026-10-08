
# Chapter 9

## Arrays and Strings

Variables such as integers, floating-point numbers, and characters can only hold one value at a time. Arrays are called scalar variables. Arrays enable programmers to store multiple related items; arrays are used to store multiple values of the same data type under a single variable name, allowing efficient handling of collections of related data.

For example, if a program needs to track the test scores of 60 students, using 60 separate integer variables is impractical. An array provides a more organized solution by grouping all scores under a single array name, making it easier to work with the data.

## 9.1 Introduction

Before using arrays, they need to be declared and initialized. Declaring an array specifies the data type and size of the array, while initializing an array assigns values to its elements. For example, the following code declares and initializes an array of integers:

```c
int arr[5] = {1, 2, 3, 4, 5};
```

In this example, the array has 5 elements of type int, and each element is initialized with a value.

To access elements of an array, you use an index, which is an integer value representing the position of the element in the array. In C, indices start from 0. For example, to access the second element of the array arr, you would use the following code:

```c
int second_number = arr[1]; // Copy to another variable
arr[1] = 100;             // Change to a new value
```

This code retrieves the value of the second element of arr and modifies it. If you don't specify the size when initializing an array, the compiler determines it based on the number of initial values:

```c
int arr[] = {1, 2, 3, 4, 5};
```

You can also declare an array without initializing it, like this:

In this case, the array contains garbage values until you assign specific values later in your program.

Attempting to access or modify an element beyond the array's size (e.g., arr[5]) results in undefined behavior, which can lead to unpredictable program behavior, including garbage values or crashing the program. Arrays in C are zero-indexed, meaning the first element has an index of 0, and the last element's index is one less than the size.

## 9.2 Arrays Operations

One-dimensional arrays consist of a single column and multiple rows and are commonly used to store collections of data. Various operations can be performed on arrays to manipulate and analyze data effectively. In this section, we will discuss some basic array operations, such as computing the sum, average, maximum, and minimum.

### 9.2.1 Lookup Tables

Lookup tables are a powerful concept in programming that enable efficient retrieval of data by mapping input values to corresponding output values. They are commonly implemented using arrays, where each element represents a key or index, and the corresponding value is stored at that position. Lookup tables excel in scenarios involving repetitive calculations or data lookups based on a known set of inputs.

The following code demonstrates the usage of a lookup table to determine the number of days in a specific month.

```c
#include <stdio.h>

int main() {
    const int month_days[12] = {31, 28, 31, 30, 31, 30,
                               31, 31, 30, 31, 30, 31};
    int month = 3; // Accessing lookup table for March

    printf("Number of days in month %d: %d\n",
           month, month_days[month - 1]);

    return 0;
}
```

The code defines a constant array called month_days that stores the number of days in each month of the year. By accessing month_days[month - 1] where month corresponds to the desired month, the code retrieves the number of days for that month. For example, month_days[2] corresponds to March, which has 31 days.

The following code showcases the use of a lookup table to count the number of set bits (bits with a value of 1) in the lowest nibble (lowest 4 bits) of the binary representation of a given number.

```c
#include <stdio.h>

int main() {
    const int bits[16] = {0, 1, 1, 2, 1, 2, 2, 3, 1, 2, 2, 3, 2, 3, 4};
    int nibble = 10; // Accessing number of bits in the number 10

    printf("Number of bits set in %d: %d\n",
           nibble, bits[nibble & 0xF]);

    return 0;
}
```

The bits array is defined as a constant array with 16 elements, where each element represents the count of set bits for the corresponding decimal number from 0 to 15. By performing a bitwise AND operation bits[nibble & 0xF] to extract the least significant 4 bits of nibble, the code uses the result as an index to access the corresponding count of set bits in the lookup table. For instance, bits[10 & 0xF] corresponds to the number of set bits in the binary representation of 10, which is 2.

These examples illustrate the efficiency and convenience of lookup tables to retrieve information based on specific inputs. They offer a direct approach that minimizes the need for complex calculations.

### 9.2.2 Traversing Arrays

Traversing an array involves visiting each element. Loops are commonly used for this purpose. For example, to calculate the average of elements, you divide the sum by the total number of elements.

```c
int sum = 0;
for (int i = 0; i < 5; i++) {
    sum += arr[i];
}
double average = (double) sum / 5;
printf("The average of elements is: %.2f\n", average);
```

To find the maximum or minimum value in an array, you iterate over the array and keep track of the current maximum or minimum. For instance, to find the maximum value in an array called arr:

```c
int max = arr[0];
for (int i = 1; i < 5; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
```

```c
printf("The maximum value in the array is: %d\n", max);
```

In this example, max is initialized with the first element's value, compared against the remaining elements in the array to find the maximum.

### 9.2.3 Modifying Array Elements

Modifying array elements means modifying the values stored in one or more of its elements. This can be done directly by accessing and assigning new values to the elements via their indices. When using algorithms that require changes to the contents or updating data stored in the array, array elements are frequently modified. Below is an example code that fills a 10-element array with random numbers from 0 to 100:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    // Seed the random number generator
    srand(time(NULL));

    int arr[10]; // Declare an array of size 10

    // Fill the array with random numbers
    for (int i = 0; i < 10; i++) {
        arr[i] = rand() % 101; // Generate a random number 0-100
    }

    // Display the array with modified elements
    printf("Array with Modified Elements: % ");
    for (int i = 0; i < 10; i++) {
        printf("%d\n", arr[i]);
    }
    return 0;
}
```
