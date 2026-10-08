
## 9.2 Arrays Operations

```c
}
printf("\n");

return 0;
```

In this example:

- We include the header files for standard input/output (stdio.h), random number generation (stdlib.h), and time manipulation (time.h).
- We seed the random number generator with `rand(time(NULL))` to ensure that the program generates different sequences of random numbers each time it runs.
- To store the random numbers, we declare an uninitialized array of size 10.
- We use a loop to iterate through the array and assign a random number between 0 and 100 to each element using the `rand()` function and the modulo operator (%).
- Finally, we display the modified array populated with random numbers.

## 9.2.4 Searching Arrays

Searching in arrays aims to find a specific value or element within an array. Searching is used in a variety of applications, such as finding specific data in a dataset, implementing lookup tables, and optimizing search algorithms. There are several searching algorithms that can be used efficiently to locate an element in an array.

- Linear Search: This simple algorithm sequentially checks each element of the array until it finds the target or reaches the end of the array.
- Binary Search: This algorithm works on sorted arrays. It repeatedly divides the search space in half by comparing the target element with the middle element of the array. Based on the comparison, it narrows the search to the lower or upper half of the array, eliminating the other half at each step.

The choice of search algorithm depends on whether the array is sorted or unsorted and the desired time complexity for the search operation. Linear search is simpler but less efficient for large arrays, while binary search is more efficient but requires the array to be sorted.

Below is an example code demonstrating how to perform linear search in a C array:

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = sizeof(arr) / sizeof(arr[0]); // Calculate the size of array
    int key = 30; // Element to search for
    int index = -1; // Initialize index to -1 indicating element not found

    // Perform linear search
    for (int i = 0; i < n; i++) {
      if (arr[i] == key) {
        index = i; // Update index if the key is found
        break; // Exit loop once the key is found
      }
    }

    // Check if the element was found or not
    if (index != -1) {
        printf("Element %d found at index %d\n", key, index);
    } else {
        printf("Element %d not found in the array\n", key);
    }

    return 0;
}
```

This code declares an array `arr` with elements 10, 20, 30, 40, 50 and performs a linear search to find the index of the element 30. If the element is found, it prints its index; otherwise, it prints a message indicating that the element was not found.

We can also do other array operations as finding the smallest or biggest number in the array, counting the number of elements that lie in a specific range, or performing statistical analysis on the array (average, mean, median, standard deviation, etc.).

## 9.2.5 Sorting Arrays

Sorting is the process of arranging the elements of an array in a specific order, such as ascending or descending. This is a common operation in programming because it helps organize data and make it easier to search and process.

There are several sorting algorithms that can be used to sort an array, such as:

- **Bubble Sort**: This simple algorithm repeatedly compares adjacent elements and swaps them if they are in the wrong order. The process is repeated until the entire array is sorted.
- **Insertion Sort**: This algorithm builds the final sorted array one element at a time. It iterates through the array, comparing each element with the already sorted portion and inserting it at the appropriate position.
- **Selection Sort**: This algorithm divides the array into two parts: the sorted part and the unsorted part. It repeatedly selects the smallest element from the unsorted part and swaps it with the element in the sorted part.
- **Quick Sort**: This algorithm uses the divide-and-conquer strategy. It selects a pivot element, partitions the array into two subarrays based on the pivot, and recursively sorts the subarrays.

The choice of a sorting algorithm depends on several factors, such as the size of the array, the way the data is distributed, and the program's performance needs. Some algorithms work better for small arrays, while others are more efficient for larger ones. Below is an example of how to sort an array `arr` using the bubble sort algorithm, which is one of the simplest sorting methods:

Bubble sort is a simple sorting algorithm that works by repeatedly stepping through a list, comparing adjacent elements, and swapping them if they are in the incorrect order. The algorithm derives its name from the way larger elements "bubble" towards the end of the list with each pass.

The code starts with an array of numbers: {64, 34, 25, 12, 22, 90, 11}. The size of the array is calculated using `sizeof(arr) / sizeof(arr[0])`, which gives the number of elements in the array. The program then prints out the original array. The code uses two loops to sort the:

# Chapter 9. Arrays and Strings

| 64 | 64 |
|---|---|
| 34 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |
| 25 | 25 |
| 12 | 12 |
| 22 | 22 |
| 34 | 34 |

 
The choice of a sorting algorithm depends on several factors, such as the size of the array, the way the data is distributed, and the program's performance needs. Some algorithms work better for small arrays, while others are more efficient for larger ones. Below is an example of how to sort an array `arr` using the bubble sort algorithm, which is one of the simplest sorting methods:

Bubble sort is a simple sorting algorithm that works by repeatedly stepping through a list, comparing adjacent elements, and swapping them if they are in the incorrect order. The algorithm derives its name from the way larger elements "bubble" towards the end of the list with each pass.

The code starts with an array of numbers: {64, 34, 25, 12, 22, 90, 11}. The size of the array is calculated using `sizeof(arr) / sizeof(arr[0])`, which gives the number of elements in the array. The program then prints out the original array. The code uses two loops to sort the:

## 9.3 Multidimensional Arrays

Multidimensional arrays are arrays with multiple rows and columns, making them ideal for a grid of data.

### 9.3.1 Declaring and Initializing Multidimensional Arrays

To declare a multidimensional array, specify the data type, followed by the array name, and then the number of rows and columns in square brackets. For example, the following code declares a two-dimensional array of integers called `matrix` with 3 rows and 4 columns:

```c
int matrix[3][4];
```

You can initialize a multidimensional array using the same syntax, with values separated by commas and enclosed in curly braces:

```c
int matrix[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

### 9.3.2 Accessing Array Elements

To access an element in a two-dimensional array, you use two indices. The first index specifies the row, and the second index specifies the column. For example, to access the element in the second row and third column of the matrix, you can use the following code:

```c
int element = matrix[1][2];
```

This code assigns the value of the element in the second row and third column of the array matrix to the variable element.

To modify an element in a multidimensional array, you can simply assign a new value to it using the same index syntax. For example, to change the value of the element in the second row and third column of the array matrix to 10, you can use the following code:

```c
matrix[1][2] = 10;
```

You can traverse the two-dimensional array using nested loops, such as in the following code, which sums all the elements in a 3x4 matrix:

```c
int sum = 0;
for (int i = 0; i < 3; i++) {
  for (int j = 0; j < 4; j++) {
    sum += matrix[i][j];
  }
}
```

Using multidimensional arrays, you can also find the maximum element, transpose the matrix, and perform matrix multiplication.

## 9.4 Strings

In C, a string is stored in an array of characters. Each individual character of the string occupies a specific position in the array, starting from index 0. To denote the end of the
