![](image_rsrc3UK.jpg)

Din Asotic

Arrays in C++

Copyright © 2023 by Din Asotic

All rights reserved. No part of this publication may be reproduced, stored or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning, or otherwise without written permission from the publisher. It is illegal to copy this book, post it to a website, or distribute it by any other means without permission.

Please use information found in this book carefully. The author is not responsible for any issues caused by misunderstanding concepts in this work.

Any questions about the book series can be asked on development@eucoding.com

First edition

This book was professionally typeset on Reedsy
Find out more at [reedsy.com](https://reedsy.com)

![Publisher Logo](image_rsrc3UM.jpg)

# Contents

[Introduction to Arrays in C++](#part0004.xhtml)

[1\. Array Declaration](#part0005.xhtml)

[2\. Array Declaration and Initialization](#part0006.xhtml)

[3\. Array Access](#part0007.xhtml)

[4\. Array Size](#part0008.xhtml)

[5\. Array Modification](#part0009.xhtml)

[6\. Array Traversal](#part0010.xhtml)

[7\. Sorting](#part0011.xhtml)

[8\. Array Searching](#part0012.xhtml)

[9\. Array Copying](#part0013.xhtml)

[10\. Array Concatenation](#part0014.xhtml)

[11\. Array Reversal](#part0015.xhtml)

[12\. Array Comparison](#part0016.xhtml)

[13\. Array Sum](#part0017.xhtml)

[14\. Array Average](#part0018.xhtml)

[15\. Array Maximum](#part0019.xhtml)

[16\. Array Minimum](#part0020.xhtml)

[17\. Array Unique Elements](#part0021.xhtml)

[18\. Array Frequency](#part0022.xhtml)

[19\. Array Subarray](#part0023.xhtml)

[20\. Array Element Swapping](#part0024.xhtml)

[21\. Array Partition](#part0025.xhtml)

[22\. Array Shuffling](#part0026.xhtml)

[23\. Array Rotation](#part0027.xhtml)

[24\. Array Insertion](#part0028.xhtml)

[25\. Array Deletion](#part0029.xhtml)

[26\. Array Palindrome](#part0030.xhtml)

[27\. Array Intersection](#part0031.xhtml)

[28\. Array Union](#part0032.xhtml)

[29\. Array Difference](#part0033.xhtml)

[30\. Array Subset](#part0034.xhtml)

[31\. Array Symmetry](#part0035.xhtml)

[32\. Array Sorting Order](#part0036.xhtml)

[33\. Array Majority Element](#part0037.xhtml)

[34\. Array Missing Element](#part0038.xhtml)

[35\. Array Range](#part0039.xhtml)

[36\. Array Product](#part0040.xhtml)

[37\. Array Partitioning](#part0041.xhtml)

[38\. Array Duplicates](#part0042.xhtml)

[39\. Array Even-Odd Partitioning](#part0043.xhtml)

[40\. Array Zero Sum Subarray](#part0044.xhtml)

[41\. Array Longest Increasing Subarray](#part0045.xhtml)

[42\. Array Longest Common Subsequence](#part0046.xhtml)

[43\. Array Longest Palindromic Subsequence](#part0047.xhtml)

[44\. Array Longest Bitonic Subarray](#part0048.xhtml)

[45\. Array Maximum Sum Subarray](#part0049.xhtml)

[46\. Array Circular Subarray Sum](#part0050.xhtml)

[47\. Array Kth Smallest Element](#part0051.xhtml)

[48\. Array Consecutive Elements](#part0052.xhtml)

[49\. Array Peaks and Valleys](#part0053.xhtml)

[50\. Array Majority Elements](#part0054.xhtml)

[51\. Array Leader Elements](#part0055.xhtml)

[52\. Array Equilibrium Index](#part0056.xhtml)

[53\. Array Rearrangement](#part0057.xhtml)

[54\. Array Max Consecutive Ones](#part0058.xhtml)

[55\. Array Zigzag Traversal](#part0059.xhtml)

[56\. Array Spiral Traversal](#part0060.xhtml)

[57\. Array Pascal’s Triangle](#part0061.xhtml)

[58\. Array Rotated Sorted Search](#part0062.xhtml)

[59\. Array Maximal Square](#part0063.xhtml)

[60\. Array Frequency Count](#part0064.xhtml)

[61\. Array Median](#part0065.xhtml)

[62\. Array Inversion Count](#part0066.xhtml)

[63\. Array Next Permutation](#part0067.xhtml)

[64\. Array Three Sum](#part0068.xhtml)

[65\. Array Two Sum](#part0069.xhtml)

[66\. Array Valid Mountain](#part0070.xhtml)

[67\. Array Sliding Window Maximum](#part0071.xhtml)

[68\. Array Dutch National Flag](#part0072.xhtml)

[69\. Array Next Greater Element](#part0073.xhtml)

[70\. Array Subarray with Given Sum](#part0074.xhtml)

[71\. Array Product of Array Except Self](#part0075.xhtml)

[72\. Array First Missing Positive](#part0076.xhtml)

[73\. Array Game of Life](#part0077.xhtml)

[74\. Array Jump Game](#part0078.xhtml)

[75\. Array Max Points on a Line](#part0079.xhtml)

[76\. Array Merge Intervals](#part0080.xhtml)

[77\. Array Plus One](#part0081.xhtml)

[78\. Array Triplet Sum Closest](#part0082.xhtml)

[79\. Array Subsets](#part0083.xhtml)

[80\. Array Unique Paths](#part0084.xhtml)

[81\. Array Submatrix Sum](#part0085.xhtml)

[82\. Array Spiral Matrix Generation](#part0086.xhtml)

[83\. Array Target Sum](#part0087.xhtml)

[84\. Array Maximum Subarray Product](#part0088.xhtml)

[85\. Array Kth Largest Element](#part0089.xhtml)

[86\. Array Subarray with Equal 0s and 1s](#part0090.xhtml)

[87\. Array Minimum Size Subarray Sum](#part0091.xhtml)

[88\. Array Sort Colors](#part0092.xhtml)

[89\. Array Sort Colors](#part0093.xhtml)

[90\. Array Maximum Frequency Element](#part0094.xhtml)

[91\. Array Maximum Subarray Sum with No Adjacent Elements](#part0095.xhtml)

[92\. Array Perfect Peak](#part0096.xhtml)

[93\. Array Repeated Number](#part0097.xhtml)

[94\. Array Subarray with Maximum XOR](#part0098.xhtml)

[95\. Array Sum of Absolute Differences](#part0099.xhtml)

[96\. Array Wiggle Sort](#part0100.xhtml)

[97\. Array Range Sum Query](#part0101.xhtml)

[98\. Array Longest Mountain Subarray](#part0102.xhtml)

[99\. Array Count Inversions](#part0103.xhtml)

[100\. Array Maximum Area of Histogram](#part0104.xhtml)

[Appendix](#part0105.xhtml)

# Introduction to Arrays in C++

An array, in computer science, is a collection of elements stored at contiguous memory locations. It is one of the simplest and most important data structures in computer programming. This guide provides a thorough introduction to arrays in C++, one of the most widely used programming languages today.

## What is an Array?

An array in C++ is a data structure that holds a fixed-size sequence of values of the same type. The size of the array is determined at the time of creation and cannot be changed. It is often used when we want to store a list of elements and access them by a single variable, instead of declaring separate variables for each element.

## Array Declaration

In C++, an array can be declared in several ways, but the standard way is as follows:

dataType arrayName[arraySize];

Here, dataType is the type of values that the array will hold, arrayName is the name given to the array, and arraySize is an integer constant greater than zero, indicating the number of elements the array will contain. For instance, if we want to create an array of integers named ‘numbers’ with space for 5 elements, the declaration would look like this:

int numbers[5];

## Array Initialization

We can initialize an array at the time of declaration, or we can declare it first and then initialize. The methods are as follows:

### Initialization at the Time of Declaration

int numbers[5] = {1, 2, 3, 4, 5};

Here, we have an array named ‘numbers’ that can hold 5 integer values. The values inside the curly braces are the initial values of the array.

### Initialization after Declaration

If you don’t initialize an array at the time of declaration, you can assign values to it later as follows:

int numbers[5];
numbers[0] = 1;
numbers[1] = 2;
numbers[2] = 3;
numbers[3] = 4;
numbers[4] = 5;

This is equivalent to the previous method. However, remember that the index of an array in C++ starts from 0, not 1.

## Accessing Array Elements

Array elements are accessed using their indices. The index refers to the position of the element in the array, with the first element at index 0\. Here’s how you can access the array elements:

cout << numbers[0];  // This will output 1
cout << numbers[4];  // This will output 5

Be careful not to access an index beyond the size of your array, as it leads to undefined behavior.

## Multidimensional Arrays

In addition to one-dimensional arrays, C++ supports multidimensional arrays. The most common is the two-dimensional array, often used to represent matrices.

Declaration and initialization of a 2D array can be done as follows:

int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};

Here, matrix is a two-dimensional array that contains 2 arrays, each with 3 elements. To access the elements, we use two indices:

cout << matrix[0][0]; // Outputs 1
cout << matrix[1][2]; // Outputs 6

## Arrays and Loops

Arrays are often used with loops. For instance, if we wanted to output all elements of an array, we could use a for loop as follows:

int numbers[5] = {1, 2, 3, 4, 5};

for (int i = 0; i < 5; i++) {
    cout << numbers[i] << " ";
}

This would output 1 2 3 4 5.

## Limitations of Arrays in C++

While arrays are incredibly useful, they do have some limitations in C++. These include:

1.  Fixed Size: Once the size of an array is declared, it cannot be changed. This could lead to wasted space if the array isn’t fully utilized or a shortage of space if we have more elements than the array can hold.

2.  Same Data Type: All elements in the array must be of the same data type.

3.  Lack of Built-in Methods: Unlike higher-level data structures like vectors or lists, arrays don’t come with built-in methods for operations like sorting, inserting, deleting, etc.

Despite these limitations, arrays are fundamental to understanding data structures and algorithms. They provide a solid basis for learning about more complex data structures and are still used widely due to their simplicity and efficiency.

# 1

# Array Declaration

In C++, you can declare an array of integers with a fixed size of 10 using the following syntax:

int myArray[10];

Here’s an explanation of the syntax:

*   int: It specifies the data type of the elements in the array, which in this case is integers. You can replace int with any other data type if you want to create an array of a different type.

*   myArray: It is the name given to the array. You can choose any valid identifier as the name.

*   [10]: It indicates the size of the array, specifying the number of elements the array can hold. In this case, the size is 10, meaning the array can store 10 integers.

To access individual elements of the array, you can use the array name followed by the index of the element in square brackets. The index ranges from 0 to size-1\. Here’s an example:

int myArray[10];  // Declaration of the array

// Accessing individual elements
myArray[0] = 42;  // Assigning 42 to the first element of the array
int element = myArray[0];  // Accessing the value of the first element and storing it in a variable

In this example, myArray[0] refers to the first element of the array, and myArray[0] = 42 assigns the value 42 to that element. Similarly, myArray[1] would refer to the second element, myArray[2] to the third element, and so on.

# 2

# Array Declaration and Initialization

Here’s an example program in C++ that demonstrates the declaration and initialization of an array:

#include <iostream>

int main() {
    // Declare and initialize an array of integers
    int numbers[5] = {1, 2, 3, 4, 5};

    // Print the array elements
    for (int i = 0; i < 5; ++i) {
        std::cout << numbers[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we declare an array named numbers of size 5, which means it can store 5 integers. We initialize the array with the values {1, 2, 3, 4, 5} using the curly braces initializer list. Each value is separated by a comma.

Arrays in C++ are derived data types. They are derived from the fundamental data types and can be thought of as a collection of elements of the same data type. In the example program, we declared an array of integers (int), but arrays can also be declared for other data types like char, float, or even user-defined types.

The array declaration consists of two parts: the data type of the elements and the name of the array. In the example, the data type is int, and the array is named numbers. The size of the array is specified inside square brackets [5], indicating that the array can hold 5 integers.

Arrays are zero-indexed, which means the first element of the array has an index of 0, the second element has an index of 1, and so on. In the program, we use a for loop to iterate over the array elements and print them using std::cout.

It’s important to note that when initializing an array, the number of elements in the initializer list must match the size of the array. If the initializer list has fewer elements, the remaining elements are automatically initialized to zero for numeric types (int, float, etc.) or to the null character (’\0’) for character arrays (char).

# 3

# Array Access

Here’s an example program in C++ that accesses and prints the elements of an array:

#include <iostream>

int main() {
    int array[] = {1, 2, 3, 4, 5};
    int size = sizeof(array) / sizeof(array[0]);

    for (int i = 0; i < size; i++) {
        std::cout << "Element at index " << i << ": " << array[i] << std::endl;
    }

    return 0;
}

In this program, we have an integer array named array with 5 elements: 1, 2, 3, 4, and 5\. The size of the array is calculated by dividing the total size of the array (sizeof(array)) by the size of an individual element (sizeof(array[0])). This calculation determines the number of elements in the array and assigns it to the variable size.

The program then uses a for loop to iterate over the elements of the array. The loop variable i represents the index of the current element being accessed. The loop starts with i initialized to 0 and continues as long as i is less than the size of the array (i < size). In each iteration, the program prints the index and the corresponding element value using array[i].

Now let’s discuss how array indices work and the importance of accessing elements within valid bounds.

In C++, arrays are zero-indexed, meaning the first element of an array has an index of 0, the second element has an index of 1, and so on. Therefore, to access a particular element in an array, we use its corresponding index.

For example, in the program above, array[0] represents the first element, array[1] represents the second element, and so on. Array indices allow us to specify which element we want to access or modify within the array.

It is crucial to access array elements within valid bounds to avoid unexpected behavior and errors. Array indices must be non-negative integers and should not exceed the size of the array. Accessing elements outside the valid bounds of an array can lead to:

1.  Undefined behavior: The program may produce unpredictable results. It could crash, return incorrect values, or modify unrelated memory locations, which can be difficult to debug.

2.  Memory access violations: If an index is out of bounds, the program may try to read from or write to a memory location that does not belong to the array. This can lead to segmentation faults or access violations, causing the program to terminate abruptly.

To ensure valid array access, it is important to check that the indices used to access array elements are within the range of valid indices (0 to size-1). This prevents errors and ensures the program operates on the intended elements of the array.

# 4

# Array Size

In C++, the sizeof operator is used to determine the size, in bytes, of a variable or a data type. When used with an array, the sizeof operator returns the total size of the array in bytes.

The sizeof operator calculates the size of an object or a type by evaluating the number of bytes it occupies in the computer’s memory. It takes either a type or an expression as its operand and returns an unsigned integer value representing the size of that operand.

When you use the sizeof operator with an array, it returns the total size of the array, which is calculated by multiplying the size of each element in the array by the number of elements. For example, if you have an array of integers with 10 elements, and each integer takes 4 bytes of memory, the sizeof operator would return 40 (10 elements * 4 bytes per element).

Here’s an example that demonstrates the usage of sizeof with an array:

#include <iostream>

int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    std::cout << "Size of the array: " << size << std::endl;
    std::cout << "Size of each element: " << sizeof(numbers[0]) << " bytes" << std::endl;
    std::cout << "Total size of the array: " << sizeof(numbers) << " bytes" << std::endl;

    return 0;
}

In this example, sizeof(numbers) gives you the total size of the numbers array, while sizeof(numbers[0]) gives you the size of each element in the array. By dividing the total size by the size of each element, you can determine the number of elements in the array.

Note that the sizeof operator determines the size of the array at compile-time, so it won’t give you the number of elements in a dynamically allocated array or an array passed as a function argument (unless it’s a reference or a pointer). In those cases, you would need to track the size separately.

# 5

# Array Modification

Here’s an example of a C++ program that modifies the elements of an array:

#include <iostream>

int main() {
    const int SIZE = 5;
    int numbers[SIZE];

    // Initialize the array with some values
    for (int i = 0; i < SIZE; i++) {
        numbers[i] = i + 1;
    }

    // Print the original array
    std::cout << "Original array: ";
    for (int i = 0; i < SIZE; i++) {
        std::cout << numbers[i] << " ";
    }
    std::cout << std::endl;

    // Modify individual elements of the array
    numbers[0] = 10;
    numbers[2] = 20;
    numbers[4] = 30;

    // Print the modified array
    std::cout << "Modified array: ";
    for (int i = 0; i < SIZE; i++) {
        std::cout << numbers[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we declare an array numbers of size SIZE (which is set to 5 in this example). We then use a loop to assign initial values to the elements of the array. In this case, we assign values 1 to SIZE to the array elements.

To assign new values to individual elements of the array, we use the array index notation. For example, numbers[0] = 10; assigns the value 10 to the first element of the array, numbers[2] = 20; assigns 20 to the third element, and numbers[4] = 30; assigns 30 to the fifth element.

Finally, we use another loop to print the elements of the array before and after the modifications to verify the changes.

When modifying arrays, it’s important to ensure that the index used to access the array elements is within the bounds of the array. Otherwise, it can lead to undefined behavior or runtime errors.

# 6

# Array Traversal

Array traversal refers to the process of accessing each element in an array and performing some operation on it. In C++, array traversal is typically done using loops, such as the “for” or “while” loop.

Here’s an example program that demonstrates array traversal using a “for” loop:

#include <iostream>

int main() {
    int arr[] = {1, 2, 3, 4, 5};  // Example array

    // Traversing the array using a for loop
    for (int i = 0; i < sizeof(arr) / sizeof(arr[0]); i++) {
        // Perform operation on each element
        std::cout << arr[i] << " ";  // Print the element
    }

    return 0;
}

In this program, we have an integer array arr containing some elements. The sizeof(arr) / sizeof(arr[0]) expression calculates the length of the array. We use a “for” loop to iterate over the array, starting from index 0 and continuing until the index reaches the length of the array minus 1.

Within the loop, you can perform any desired operation on each element. In the given example, we simply print each element using std::cout. You can replace this line with any other operation or calculation you want to perform on the elements of the array.

The loop will iterate through each element of the array, performing the specified operation on each one. This way, you can process each element individually without having to write repetitive code for each element separately.

Array traversal is a fundamental concept in programming and is widely used for various tasks, such as searching, sorting, filtering, or modifying array elements.

# 7

# Sorting

The Bubble Sort algorithm works by repeatedly swapping adjacent elements if they are in the wrong order. This process continues until the entire array is sorted. Here’s an example implementation:

#include <iostream>
using namespace std;

// Function to swap two elements
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Function to perform bubble sort
void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; ++i) {
        // Last i elements are already in place
        for (int j = 0; j < size - i - 1; ++j) {
            // Swap if the current element is greater than the next element
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

// Function to print the array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {5, 2, 8, 12, 1, 6};
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    printArray(arr, size);

    bubbleSort(arr, size);

    cout << "Sorted array: ";
    printArray(arr, size);

    return 0;
}

In this program, the bubbleSort function takes the array and its size as parameters. It uses nested loops to iterate through the array and compare adjacent elements. If the current element is greater than the next element, they are swapped using the swap function.

The outer loop (i) controls the number of iterations, which is equal to the size of the array minus 1\. The inner loop (j) compares and swaps the elements until the end of the unsorted portion of the array.

Finally, the printArray function is used to display the original and sorted arrays.

When you run this program, the output will be:

Original array: 5 2 8 12 1 6
Sorted array: 1 2 5 6 8 12

The elements of the array are successfully sorted in ascending order using the Bubble Sort algorithm.

The next sorting algorithm I’ll explain is the Selection Sort algorithm. It works by dividing the array into two parts: the sorted part at the beginning and the unsorted part at the end. The algorithm repeatedly finds the smallest (or largest) element from the unsorted part and swaps it with the first element of the unsorted part. This process continues until the entire array is sorted.

Here’s a C++ implementation of the Selection Sort algorithm:

#include <iostream>
using namespace std;

// Function to swap two elements
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Function to perform selection sort
void selectionSort(int arr[], int size) {
    for (int i = 0; i < size - 1; ++i) {
        // Find the minimum element in the unsorted part of the array
        int minIndex = i;
        for (int j = i + 1; j < size; ++j) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        // Swap the found minimum element with the first element of the unsorted part
        swap(arr[i], arr[minIndex]);
    }
}

// Function to print the array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {5, 2, 8, 12, 1, 6};
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    printArray(arr, size);

    selectionSort(arr, size);

    cout << "Sorted array: ";
    printArray(arr, size);

    return 0;
}

In this program, the selectionSort function takes the array and its size as parameters. It uses two loops to perform the selection sort algorithm. The outer loop (i) represents the sorted part of the array, and the inner loop (j) finds the minimum element from the unsorted part.

Inside the inner loop, the index of the minimum element (minIndex) is updated whenever a smaller element is found. After iterating through the unsorted part, the minimum element is swapped with the first element of the unsorted part.

The outer loop continues this process until the entire array is sorted.

When you run this program, the output will be:

Original array: 5 2 8 12 1 6
Sorted array: 1 2 5 6 8 12

The elements of the array are successfully sorted in ascending order using the Selection Sort algorithm.

Insertion Sort algorithm: It works by dividing the array into two parts: the sorted part at the beginning and the unsorted part at the end. The algorithm iterates through the unsorted part and picks one element at a time, comparing it with the elements in the sorted part and inserting it in the correct position. This process continues until the entire array is sorted.

Here’s a C++ implementation of the Insertion Sort algorithm:

#include <iostream>
using namespace std;

// Function to perform insertion sort
void insertionSort(int arr[], int size) {
    for (int i = 1; i < size; ++i) {
        int key = arr[i];
        int j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key, to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Function to print the array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {5, 2, 8, 12, 1, 6};
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    printArray(arr, size);

    insertionSort(arr, size);

    cout << "Sorted array: ";
    printArray(arr, size);

    return 0;
}

In this program, the insertionSort function takes the array and its size as parameters. It uses a loop to iterate through the array starting from the second element (index 1). For each element, it compares it with the elements in the sorted part (from index 0 to i-1), shifting the larger elements to the right.

The inner loop (while loop) continues shifting the elements until it finds the correct position for the current element (key). Finally, the element is inserted in its correct position in the sorted part of the array.

The outer loop continues this process until the entire array is sorted.

When you run this program, the output will be:

Original array: 5 2 8 12 1 6
Sorted array: 1 2 5 6 8 12

The elements of the array are successfully sorted in ascending order using the Insertion Sort algorithm.

# 8

# Array Searching

In C++, there are several searching algorithms that can be used to find a specific element in an array. Here, I will explain two commonly used algorithms: linear search and binary search.

1.  Linear Search:

*   Linear search is a simple searching algorithm that sequentially checks each element of the array until a match is found or the entire array is traversed.

*   It is suitable for both sorted and unsorted arrays.

*   To implement linear search in C++, you can use a loop to iterate through each element of the array and compare it with the target element.

*   If a match is found, you can return the index of the element. Otherwise, you can return a value to indicate that the element was not found.

Here’s an example implementation of linear search in C++:

#include <iostream>

int linearSearch(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i;  // Found the target element at index i
        }
    }
    return -1;  // Element not found
}

int main() {
    int arr[] = {5, 2, 8, 10, 3};
    int size = sizeof(arr) / sizeof(arr[0]);
    int target = 8;

    int result = linearSearch(arr, size, target);
    if (result == -1) {
        std::cout << "Element not found." << std::endl;
    } else {
        std::cout << "Element found at index " << result << std::endl;
    }

    return 0;
}

1.  Binary Search:

*   Binary search is a more efficient algorithm that requires the array to be sorted in ascending order.

*   It follows the divide-and-conquer approach by repeatedly dividing the search space in half until the target element is found.

*   To implement binary search, you need to maintain two pointers: start and end, which represent the range of the search space.

*   At each step, you calculate the middle element and compare it with the target.

*   If the middle element is equal to the target, you return its index. If the middle element is greater than the target, you update end to be the middle element’s index minus one. Otherwise, you update start to be the middle element’s index plus one.

*   This process continues until the target element is found or the search space is empty.

Here’s an example implementation of binary search in C++:

#include <iostream>

int binarySearch(int arr[], int size, int target) {
    int start = 0;
    int end = size - 1;

    while (start <= end) {
        int mid = start + (end - start) / 2;

        if (arr[mid] == target) {
            return mid;  // Found the target element at index mid
        } else if (arr[mid] > target) {
            end = mid - 1;  // Target lies in the left half
        } else {
            start = mid + 1;  // Target lies in the right half
        }
    }

    return -1;  // Element not found
}

int main() {
    int arr[] = {2, 3, 5, 8, 10};
    int size = sizeof(arr) / sizeof(arr[0]);
    int target = 8;

    int result = binarySearch(arr, size, target);
    if (result == -1) {
        std::cout << "Element not found." << std::endl;
    } else {
        std::cout << "Element found at index " << result << std::endl;
    }

    return 0;
}

These are two basic searching algorithms that can be used to search for a specific element in an array. Other advanced algorithms, such as interpolation search or exponential search, can also be implemented based on specific requirements and characteristics of the data.

# 9

# Array Copying

Here’s an example program in C++ that demonstrates different methods of array copying:

#include <iostream>

// Function to copy elements from one array to another using a loop
void copyArrayUsingLoop(int source[], int destination[], int size) {
    for (int i = 0; i < size; i++) {
        destination[i] = source[i];
    }
}

// Function to copy elements from one array to another using the memcpy function
void copyArrayUsingMemcpy(int source[], int destination[], int size) {
    memcpy(destination, source, size * sizeof(int));
}

// Function to copy elements from one array to another using the std::copy function
void copyArrayUsingStdCopy(int source[], int destination[], int size) {
    std::copy(source, source + size, destination);
}

int main() {
    const int SIZE = 5;
    int source[SIZE] = {1, 2, 3, 4, 5};
    int destination1[SIZE];
    int destination2[SIZE];
    int destination3[SIZE];

    copyArrayUsingLoop(source, destination1, SIZE);
    copyArrayUsingMemcpy(source, destination2, SIZE);
    copyArrayUsingStdCopy(source, destination3, SIZE);

    // Printing the copied arrays
    std::cout << "Copied array using loop: ";
    for (int i = 0; i < SIZE; i++) {
        std::cout << destination1[i] << " ";
    }
    std::cout << std::endl;

    std::cout << "Copied array using memcpy: ";
    for (int i = 0; i < SIZE; i++) {
        std::cout << destination2[i] << " ";
    }
    std::cout << std::endl;

    std::cout << "Copied array using std::copy: ";
    for (int i = 0; i < SIZE; i++) {
        std::cout << destination3[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we have three different methods for copying arrays: using a loop, using the memcpy function, and using the std::copy function.

1.  Copying using a loop: The copyArrayUsingLoop function uses a loop to iterate through each element of the source array and copies it to the destination array. This method is straightforward and easy to understand. However, it may be less efficient compared to other methods, especially when dealing with large arrays, as it involves individual element assignments.

2.  Copying using memcpy: The copyArrayUsingMemcpy function uses the memcpy function from the C standard library. This function allows us to copy a block of memory from the source array to the destination array. It operates at a lower level and can be more efficient than a loop for large arrays. However, it assumes that the arrays are contiguous blocks of memory, and it works with bytes, so we need to specify the number of bytes to copy (size * sizeof(int) in this case).

3.  Copying using std::copy: The copyArrayUsingStdCopy function utilizes the std::copy function from the C++ standard library. It provides a higher-level abstraction for copying elements between containers. The std::copy function takes care of handling different iterator types and performs the copying operation. It is a more idiomatic and safer approach for array copying in C++. However, its performance characteristics are similar to the loop-based method.

When choosing a method for array copying, consider the trade-offs between simplicity, efficiency, and code readability. For small arrays, the performance difference between these methods may not be significant. However, for larger arrays, the memcpy or std::copy methods are generally preferred due to their potential efficiency gains.

# 10

# Array Concatenation

Here’s an example program in C++ that concatenates two arrays into a third array:

#include <iostream>

const int MAX_SIZE = 100;

void concatenateArrays(int arr1[], int arr1Size, int arr2[], int arr2Size, int result[]) {
    // Copy elements from arr1 to result
    for (int i = 0; i < arr1Size; i++) {
        result[i] = arr1[i];
    }

    // Copy elements from arr2 to result
    for (int i = 0; i < arr2Size; i++) {
        result[arr1Size + i] = arr2[i];
    }
}

int main() {
    int arr1[MAX_SIZE] = {1, 2, 3, 4, 5};
    int arr1Size = 5;

    int arr2[MAX_SIZE] = {6, 7, 8};
    int arr2Size = 3;

    int result[MAX_SIZE];

    concatenateArrays(arr1, arr1Size, arr2, arr2Size, result);

    int resultSize = arr1Size + arr2Size;

    std::cout << "Concatenated array: ";
    for (int i = 0; i < resultSize; i++) {
        std::cout << result[i] << " ";
    }

    return 0;
}

Explanation:

1.  The function concatenateArrays takes in two input arrays (arr1 and arr2), their sizes (arr1Size and arr2Size), and an output array (result).

2.  Inside the function, the elements of arr1 are copied into the result array using a for loop.

3.  Next, the elements of arr2 are copied into the result array, starting from the index arr1Size to ensure they are appended after the elements of arr1.

4.  In the main function, you declare the input arrays arr1 and arr2 along with their sizes (arr1Size and arr2Size).

5.  You also declare an output array result to store the concatenated array.

6.  Call the concatenateArrays function with the appropriate arguments to concatenate arr1 and arr2 into result.

7.  Calculate the size of the resulting array (resultSize) by adding the sizes of arr1 and arr2.

8.  Finally, use a for loop to print the elements of the result array, demonstrating the concatenated array.

When you run this program, the output will be:

Concatenated array: 1 2 3 4 5 6 7 8

This program demonstrates how to combine the elements of two arrays into a single array. The key concept is to iterate through each element of the arrays and copy them into the resulting array in the desired order. By appropriately managing the indices, you can

# 11

# Array Reversal

Here’s a C++ program that reverses the elements of an array:

#include <iostream>

void reverseArray(int arr[], int size) {
    int start = 0;
    int end = size - 1;

    while (start < end) {
        // Swap elements at start and end indices
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;

        // Move start and end towards the center
        start++;
        end--;
    }
}

int main() {
    const int size = 5;
    int arr[size] = {1, 2, 3, 4, 5};

    std::cout << "Original array: ";
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }

    reverseArray(arr, size);

    std::cout << "\nReversed array: ";
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }

    return 0;
}

Explanation:

1.  The reverseArray function takes two parameters: the array to be reversed (arr) and the size of the array (size).

2.  The function initializes two variables, start and end, with the indices of the first and last elements of the array, respectively.

3.  It enters a while loop that continues until start becomes greater than or equal to end.

4.  Inside the loop, it swaps the elements at indices start and end using a temporary variable temp.

5.  After the swap, it increments start and decrements end to move towards the center of the array.

6.  The loop continues until start is no longer less than end, ensuring all elements have been swapped.

7.  In the main function, an array arr of size 5 is declared and initialized with some values.

8.  The original array is printed using a for loop.

9.  The reverseArray function is called with the array and its size as arguments to reverse the elements.

10.  Finally, the reversed array is printed using another for loop.

When you run this program, it will output the original array and the reversed array:

Original array: 1 2 3 4 5
Reversed array: 5 4 3 2 1

The program works by swapping the first and last elements, then moving towards the center of the array, continuing to swap elements until all elements have been reversed.

# 12

# Array Comparison

Here’s an example program in C++ that compares two arrays and checks if they are equal:

#include <iostream>

bool areArraysEqual(int arr1[], int arr2[], int size) {
    for (int i = 0; i < size; i++) {
        if (arr1[i] != arr2[i]) {
            return false;
        }
    }
    return true;
}

int main() {
    int size;
    std::cout << "Enter the size of the arrays: ";
    std::cin >> size;

    int array1[size];
    int array2[size];

    std::cout << "Enter the elements of the first array: ";
    for (int i = 0; i < size; i++) {
        std::cin >> array1[i];
    }

    std::cout << "Enter the elements of the second array: ";
    for (int i = 0; i < size; i++) {
        std::cin >> array2[i];
    }

    bool equal = areArraysEqual(array1, array2, size);
    if (equal) {
        std::cout << "The arrays are equal." << std::endl;
    } else {
        std::cout << "The arrays are not equal." << std::endl;
    }

    return 0;
}

In this program, the areArraysEqual function takes two arrays (arr1 and arr2), along with the size of the arrays (size). It compares the elements of the arrays using a for loop and checks if they are equal. If any elements differ, it immediately returns false, indicating that the arrays are not equal. If the loop completes without finding any differences, it returns true, indicating that the arrays are equal.

In the main function, the user is prompted to enter the size of the arrays. Then, the elements of the first and second arrays are inputted using two separate for loops. Finally, the areArraysEqual function is called, and the result is displayed accordingly.

Note that in this example, the arrays are assumed to contain integers. You can modify the code to compare arrays of different data types by changing the data type of the arrays (int in this case) and the corresponding input and output operations.

# 13

# Array Sum

Here’s an example of a C++ program that calculates the sum of all elements in an array:

#include <iostream>

int main() {
    // Define the array
    int arr[] = {2, 4, 6, 8, 10};
    int size = sizeof(arr) / sizeof(arr[0]);  // Calculate the size of the array

    int sum = 0;  // Initialize the sum variable

    // Iterate through the array and accumulate the sum
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }

    // Print the sum
    std::cout << "Sum of array elements: " << sum << std::endl;

    return 0;
}

In this program, we first define an array arr with some elements. The size variable is calculated by dividing the total size of the array (in bytes) by the size of a single element (in bytes). This ensures that even if the array size changes, the program will still work correctly.

Next, we initialize a variable sum to 0\. This variable will accumulate the sum of all elements in the array.

The for loop is used to iterate through the array. It starts from i = 0 and continues until i < size. In each iteration, the value of arr[i] is added to the sum variable using the += operator.

Finally, we print the calculated sum using std::cout.

When you run this program, the output will be:

Sum of array elements: 30

This indicates that the sum of the elements in the array [2, 4, 6, 8, 10] is indeed 30.

# 14

# Array Average

Here’s an example program in C++ that calculates the average of all elements in an array:

#include <iostream>

double calculateAverage(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];  // Accumulate the sum of all elements
    }
    return static_cast<double>(sum) / size;  // Calculate and return the average
}

int main() {
    int arr[] = {5, 10, 15, 20, 25};
    int size = sizeof(arr) / sizeof(arr[0]);  // Calculate the size of the array

    double average = calculateAverage(arr, size);  // Call the function to calculate the average

    std::cout << "Average: " << average << std::endl;

    return 0;
}

Explanation:

1.  The calculateAverage function takes two parameters: arr, which is the array containing the elements, and size, which represents the number of elements in the array.

2.  Within the function, a variable sum is initialized to 0\. It will be used to accumulate the sum of all the elements.

3.  A for loop is used to iterate over each element of the array. The loop starts from 0 and continues until size-1.

4.  Inside the loop, each element of the array arr[i] is added to the sum variable.

5.  After the loop, the average is calculated by dividing the sum by the size of the array. To ensure accurate division, the sum is cast to double using the static_cast<double>(sum) expression.

6.  Finally, the calculateAverage function returns the calculated average.

7.  In the main function, an example array arr is defined with some sample values.

8.  The size of the array is calculated using the expression sizeof(arr) / sizeof(arr[0]), which determines the total number of elements by dividing the total size of the array by the size of a single element.

9.  The calculateAverage function is called with the array and its size, and the resulting average is stored in the average variable.

10.  The average is then printed to the console using std::cout.

When you run this program, it will output:

Average: 15

In this example, the average of the elements in the array {5, 10, 15, 20, 25} is 15.

# 15

# Array Maximum

Here’s a C++ program that finds the maximum element in an array:

#include <iostream>

int findMaximum(int arr[], int size) {
    int max = arr[0];  // Assume the first element as the maximum

    // Iterate through the array starting from the second element
    for (int i = 1; i < size; i++) {
        if (arr[i] > max) {
            max = arr[i];  // Update max if a larger element is found
        }
    }

    return max;
}

int main() {
    int arr[] = {5, 2, 9, 1, 7};
    int size = sizeof(arr) / sizeof(arr[0]);

    int maximum = findMaximum(arr, size);

    std::cout << "Maximum element in the array: " << maximum << std::endl;

    return 0;
}

Explanation:

1.  The findMaximum function takes an array arr and its size size as input.

2.  It assumes the first element arr[0] as the maximum value.

3.  The for loop starts from the second element (i = 1) and iterates through the array.

4.  Inside the loop, it compares each element arr[i] with the current maximum value (max).

5.  If arr[i] is greater than max, it updates the value of max to arr[i].

6.  After iterating through the entire array, the function returns the maximum value.

7.  In the main function, we create an example array arr and calculate its size by dividing the total size of the array by the size of a single element.

8.  We call the findMaximum function, passing the array and its size, and store the returned maximum value in the maximum variable.

9.  Finally, we print the maximum value using std::cout.

When executing the program, it will output:

Maximum element in the array: 9

The program iterates through the array and keeps track of the maximum value by comparing each element with the current maximum. If a larger element is found, it updates the maximum value. At the end of the iteration, the maximum value is returned.

# 16

# Array Minimum

Here’s a C++ program that finds the minimum element in an array:

#include <iostream>

int findMinimum(int arr[], int size) {
    int minimum = arr[0]; // Assume the first element as the minimum

    for (int i = 1; i < size; i++) {
        if (arr[i] < minimum) {
            minimum = arr[i]; // Update the minimum if a smaller element is found
        }
    }

    return minimum;
}

int main() {
    int arr[] = {5, 3, 9, 1, 7}; // Sample array
    int size = sizeof(arr) / sizeof(arr[0]); // Calculate the size of the array

    int minElement = findMinimum(arr, size);

    std::cout << "The minimum element in the array is: " << minElement << std::endl;

    return 0;
}

Explanation:

1.  The findMinimum function takes two parameters: the array (arr) and the size of the array (size).

2.  It assumes the first element of the array as the minimum (minimum = arr[0]).

3.  The for loop iterates over the array starting from the second element (i = 1) up to the last element (i < size).

4.  Inside the loop, it compares each element (arr[i]) with the current minimum (minimum).

5.  If the element is smaller than the current minimum, it updates the value of minimum to the smaller element.

6.  Finally, the minimum value is returned.

7.  In the main function, we create a sample array (arr) and calculate its size by dividing the total size of the array by the size of a single element.

8.  We then call the findMinimum function with the array and its size, storing the result in the minElement variable.

9.  Finally, we print the minimum element using std::cout.

When running the program, it will output:

The minimum element in the array is: 1

The program iterates through the array starting from the second element and compares each element with the current minimum. If a smaller element is found, the minimum value is updated accordingly. By the end of the loop, the minimum value represents the smallest element in the array.

# 17

# Array Unique Elements

Here’s an example program in C++ that removes duplicate elements from an array:

#include <iostream>
#include <unordered_set>

int main() {
    // Sample array with duplicate elements
    int arr[] = { 1, 2, 3, 4, 2, 1, 5, 6, 3, 4, 7, 8, 9, 5 };

    // Calculate the size of the array
    int size = sizeof(arr) / sizeof(arr[0]);

    // Create an unordered set to store unique elements
    std::unordered_set<int> uniqueElements;

    // Iterate through the array
    for (int i = 0; i < size; ++i) {
        // Insert each element into the set
        uniqueElements.insert(arr[i]);
    }

    // Print the unique elements
    std::cout << "Unique elements: ";
    for (int element : uniqueElements) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}

Explanation:

1.  The program starts by declaring an array arr with duplicate elements.

2.  The size of the array is calculated by dividing the total size of the array by the size of an individual element.

3.  An unordered_set called uniqueElements is created to store the unique elements from the array. The unordered set is chosen for its efficient lookup time.

4.  The program then iterates through the array using a for loop.

5.  In each iteration, the current element arr[i] is inserted into the uniqueElements set using the insert() function. The unordered set takes care of ensuring uniqueness automatically.

6.  After the loop completes, the program prints the unique elements stored in the set using another for loop.

7.  Finally, the program exits with a return value of 0.

When iterating through the array, the program inserts each element into the unordered set. The unordered set automatically handles the duplicate elements and only keeps the unique ones. By utilizing the unordered set’s uniqueness property, we can easily remove duplicates from the array.

Note that the order of elements in the output is not guaranteed to be the same as the original array, as the unordered set does not preserve the order of insertion.

# 18

# Array Frequency

Here’s an example program in C++ that counts the frequency of each element in an array using a std::map:

#include <iostream>
#include <map>

int main() {
    int arr[] = {1, 2, 3, 2, 4, 1, 3, 2, 1, 4};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::map<int, int> frequencyMap;

    // Iterate over the array and update the frequency map
    for (int i = 0; i < size; i++) {
        frequencyMap[arr[i]]++;
    }

    // Display the frequency of each element
    for (const auto& pair : frequencyMap) {
        std::cout << "Element " << pair.first << " occurs " << pair.second << " times." << std::endl;
    }

    return 0;
}

Explanation:

1.  We define an array arr with some elements and determine its size using the formula sizeof(arr) / sizeof(arr[0]).

2.  We create a std::map<int, int> named frequencyMap, where the keys represent the elements from the array and the values represent their frequencies.

3.  We iterate over the array using a for loop and update the frequency map accordingly. For each element arr[i], we use the frequencyMap[arr[i]]++ statement to increment the frequency of that element in the map.

4.  Finally, we iterate over the frequency map using a range-based for loop. For each pair of element and frequency, we display the element and its corresponding frequency using std::cout.

By using a std::map, we can efficiently keep track of the frequencies of each element in the array. The map automatically handles the storage and retrieval of key-value pairs, allowing us to easily update and access the frequencies as we iterate through the array.

# 19

# Array Subarray

In C++, you can create a new array that contains a portion of the original array by following these steps:

1.  Determine the starting and ending indices of the subarray you want to extract from the original array.

2.  Calculate the size of the subarray by subtracting the starting index from the ending index and adding 1 (to include the element at the ending index).

3.  Declare a new array with a size equal to the calculated size of the subarray.

4.  Iterate over the original array, starting from the starting index and ending at the ending index.

5.  Copy each element from the original array to the corresponding index in the new array.

Here’s an example code snippet that demonstrates this process:

#include <iostream>

int main() {
    int originalArray[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};  // Original array

    int startingIndex = 2;  // Starting index of subarray
    int endingIndex = 6;    // Ending index of subarray

    int subarraySize = endingIndex - startingIndex + 1;  // Calculate the size of subarray

    int* subarray = new int[subarraySize];  // Create a new array for the subarray

    for (int i = startingIndex; i <= endingIndex; i++) {
        subarray[i - startingIndex] = originalArray[i];  // Copy elements from original array to subarray
    }

    // Print the subarray
    for (int i = 0; i < subarraySize; i++) {
        std::cout << subarray[i] << " ";
    }

    delete[] subarray;  // Deallocate memory for the subarray

    return 0;
}

In this example, the original array contains elements from 1 to 10. We extract a subarray starting from index 2 (element 3) and ending at index 6 (element 7). The resulting subarray is {3, 4, 5, 6, 7}, which is printed to the console. Finally, we deallocate the memory allocated for the subarray using the delete[] operator.

Remember to deallocate the memory for the new array using delete[] to avoid memory leaks once you’re done using it.

# 20

# Array Element Swapping

Here’s an example program in C++ that swaps the values of two elements in an array using a temporary variable:

#include <iostream>

void swapElements(int array[], int index1, int index2) {
    int temp = array[index1];  // Store the value of the first element in a temporary variable
    array[index1] = array[index2];  // Assign the value of the second element to the first element
    array[index2] = temp;  // Assign the value from the temporary variable to the second element
}

int main() {
    int array[] = {5, 10, 15, 20, 25};  // Example array
    int index1 = 1;  // Index of the first element to swap
    int index2 = 3;  // Index of the second element to swap

    std::cout << "Before swapping: ";
    for (int i = 0; i < sizeof(array) / sizeof(array[0]); i++) {
        std::cout << array[i] << " ";
    }
    std::cout << std::endl;

    swapElements(array, index1, index2);

    std::cout << "After swapping: ";
    for (int i = 0; i < sizeof(array) / sizeof(array[0]); i++) {
        std::cout << array[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we have a function swapElements that takes an array, index1, and index2 as parameters. The function uses a temporary variable, temp, to store the value of the first element (array[index1]). Then it assigns the value of the second element (array[index2]) to the first element and finally assigns the value from the temporary variable (temp) to the second element.

In the main function, we initialize an example array and define the indices of the elements we want to swap (index1 and index2). We then print the array before the swapping, call the swapElements function, and print the array after the swapping to see the updated values.

Note that in C++, arrays are zero-indexed, so the first element has an index of 0, the second element has an index of 1, and so on.

# 21

# Array Partition

Here’s an example of a C++ program that partitions an array based on a given pivot value:

#include <iostream>
using namespace std;

void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int partition(int arr[], int low, int high, int pivot) {
    int i = low - 1;
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void arrayPartition(int arr[], int size, int pivot) {
    int partitionIndex = partition(arr, 0, size - 1, pivot);

    cout << "Partitioned Array: ";
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    cout << "Pivot Index: " << partitionIndex << endl;
}

int main() {
    int arr[] = { 10, 7, 8, 9, 1, 5 };
    int size = sizeof(arr) / sizeof(arr[0]);
    int pivot = 8;

    cout << "Original Array: ";
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    arrayPartition(arr, size, pivot);

    return 0;
}

In this program, the partition function takes an array (arr), the low and high indices of the array, and the pivot value. It rearranges the elements in the array such that all elements smaller than the pivot value come before it, and all elements greater than the pivot value come after it. The function returns the index of the pivot element after partitioning.

The arrayPartition function is responsible for calling the partition function and displaying the partitioned array and the pivot index.

In the main function, we initialize an array, specify the size of the array, and choose a pivot value. The original array is displayed, and then the arrayPartition function is called with the array, size, and pivot value.

When you run this program, the output will look like this:

Original Array: 10 7 8 9 1 5
Partitioned Array: 7 1 5 9 10 8
Pivot Index: 4

In the partitioned array, the elements smaller than the pivot (8) come before it, and the elements greater than the pivot come after it. The pivot index is 4, indicating the position of the pivot element in the partitioned array.

Feel free to modify the program according to your specific requirements or integrate it into your existing code.

# 22

# Array Shuffling

Here’s an example program in C++ that shuffles the elements of an array:

#include <iostream>
#include <cstdlib>   // for rand() and srand()
#include <ctime>     // for time()

using namespace std;

// Function to swap two elements in an array
void swapElements(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Function to shuffle an array
void shuffleArray(int arr[], int size) {
    // Initialize random seed using current time
    srand(static_cast<unsigned int>(time(nullptr)));

    // Generate random indices and swap elements
    for (int i = size - 1; i > 0; --i) {
        // Generate a random index between 0 and i (inclusive)
        int j = rand() % (i + 1);

        // Swap the current element with the randomly selected element
        swapElements(arr[i], arr[j]);
    }
}

int main() {
    const int size = 10;
    int arr[size] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    cout << "Original array: ";
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    shuffleArray(arr, size);

    cout << "Shuffled array: ";
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}

Explanation:

1.  The swapElements function takes two integers as parameters and swaps their values using a temporary variable.

2.  The shuffleArray function shuffles the elements of the array using the Fisher-Yates algorithm:

*   It initializes the random seed by calling srand with the current time (to ensure different results on each run).

*   It iterates over the array from the last element to the second element.

*   For each iteration, it generates a random index j between 0 and i (inclusive) using the % operator.

*   It swaps the current element at index i with the element at index j.

1.  In the main function, an array of integers is declared and initialized.

2.  The original array is printed.

3.  The shuffleArray function is called to shuffle the array.

4.  The shuffled array is printed.

Note: This program assumes that you have C++11 or a later version to support the use of auto and range-based for loops. If you’re using an older version of C++, you may need to modify the code accordingly.

# 23

# Array Rotation

Here’s a C++ program that rotates the elements of an array by a given number of positions:

#include <iostream>

// Function to rotate the elements of an array by a given number of positions
void rotateArray(int arr[], int n, int k) {
    // Create a temporary array to store the rotated elements
    int temp[k];

    // Store the first k elements of the original array in the temporary array
    for (int i = 0; i < k; i++) {
        temp[i] = arr[i];
    }

    // Shift the remaining elements of the original array by k positions
    for (int i = k; i < n; i++) {
        arr[i - k] = arr[i];
    }

    // Copy the rotated elements from the temporary array to the end of the original array
    for (int i = 0; i < k; i++) {
        arr[n - k + i] = temp[i];
    }
}

// Function to display the elements of an array
void displayArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    int k;
    std::cout << "Enter the number of positions to rotate: ";
    std::cin >> k;

    std::cout << "Original array: ";
    displayArray(arr, n);

    rotateArray(arr, n, k);

    std::cout << "Rotated array: ";
    displayArray(arr, n);

    return 0;
}

In this program, we have two main functions:

1.  rotateArray: This function takes the array (arr), the number of elements in the array (n), and the number of positions to rotate the array (k) as input. It performs the rotation by following these steps:

*   It creates a temporary array (temp) of size k to store the first k elements of the original array.

*   It shifts the remaining elements of the original array to the left by k positions.

*   Finally, it copies the rotated elements from the temporary array to the end of the original array.

1.  displayArray: This function takes the array (arr) and the number of elements in the array (n) as input. It simply displays the elements of the array.

In the main function, we initialize an array (arr) with some values and determine the number of elements in the array (n). Then, we prompt the user to enter the number of positions to rotate (k). After that, we call the rotateArray function to rotate the array and display the original and rotated arrays using the displayArray function.

To achieve circular rotation, we shift the elements to the left and copy the shifted elements to the end of the array. For example, if the array is [1, 2, 3, 4, 5] and we want to rotate it by 2 positions, the process would be as follows:

*   Store the first 2 elements in the temporary array: temp = [1, 2]

*   Shift the remaining elements to the left: arr = [3, 4, 5, 4, 5]

*   Copy the rotated elements from the temporary array to the end of the original array: arr = [3, 4, 5, 1, 2]

Now, the array is rotated by 2 positions.

Note that this program assumes that the number of positions to rotate (k) is less than or equal to the number of elements in the array (n). If k is greater than n, the rotation will still be performed, but it will wrap around multiple times. You can modify the program to handle cases where k is greater than n as per your requirements.

# 24

# Array Insertion

Here’s a program in C++ that inserts a new element at a specific position in an array:

#include <iostream>

const int MAX_SIZE = 100;

void insertElement(int arr[], int& size, int position, int element) {
    if (position < 0 || position > size) {
        std::cout << "Invalid position. Element cannot be inserted." << std::endl;
        return;
    }

    // Shift elements to the right from the insertion position
    for (int i = size - 1; i >= position; i--) {
        arr[i + 1] = arr[i];
    }

    // Insert the new element at the specified position
    arr[position] = element;

    // Increment the size of the array
    size++;
}

void displayArray(const int arr[], int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[MAX_SIZE];
    int size;

    std::cout << "Enter the size of the array (up to " << MAX_SIZE << "): ";
    std::cin >> size;

    std::cout << "Enter the elements of the array: ";
    for (int i = 0; i < size; i++) {
        std::cin >> arr[i];
    }

    int position, element;
    std::cout << "Enter the position where the element should be inserted: ";
    std::cin >> position;

    std::cout << "Enter the element to be inserted: ";
    std::cin >> element;

    insertElement(arr, size, position, element);

    std::cout << "Array after insertion: ";
    displayArray(arr, size);

    return 0;
}

In this program, the insertElement function takes an array (arr), the current size of the array (size), the position where the element should be inserted (position), and the element to be inserted (element).

First, it checks if the specified position is valid. If it’s less than 0 or greater than the current size, it prints an error message and returns.

If the position is valid, the function starts shifting the elements to the right from the insertion position. It iterates from the last element to the insertion position and moves each element one position to the right.

After shifting the elements, it inserts the new element at the specified position by assigning the element value to arr[position].

Finally, the function increments the size of the array (size) to account for the inserted element.

The displayArray function is a helper function that prints the elements of the array.

In the main function, the program prompts the user to enter the size of the array, the elements of the array, the position, and the element to be inserted. It then calls the insertElement function and displays the resulting array.

Note: This program assumes that the array has enough space to accommodate the new element and doesn’t perform any boundary checks.

# 25

# Array Deletion

Here’s a C++ program that demonstrates deleting an element at a specific position in an array and shifting the remaining elements to close the gap:

#include <iostream>

void deleteElement(int arr[], int& size, int position) {
    if (position < 0 || position >= size) {
        std::cout << "Invalid position." << std::endl;
        return;
    }

    // Shift elements to close the gap
    for (int i = position; i < size - 1; i++) {
        arr[i] = arr[i + 1];
    }

    // Decrement the size of the array
    size--;

    std::cout << "Element at position " << position << " has been deleted." << std::endl;
}

int main() {
    const int MAX_SIZE = 100;
    int arr[MAX_SIZE] = {1, 2, 3, 4, 5};
    int size = 5;
    int position;

    std::cout << "Enter the position of the element to delete: ";
    std::cin >> position;

    deleteElement(arr, size, position);

    std::cout << "Updated array: ";
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

Explanation:

1.  The deleteElement function takes three parameters: the array arr, a reference to the size of the array size, and the position of the element to be deleted.

2.  First, it checks if the provided position is valid, i.e., it should be within the range of the array.

3.  If the position is valid, the function starts shifting the elements to close the gap. It iterates from the given position until the second-to-last element of the array.

4.  For each iteration, it assigns the value of the next element to the current element, effectively shifting all elements one position to the left.

5.  After the shifting is complete, the size of the array is decremented by 1 to reflect the deletion of an element.

6.  Finally, in the main function, the user is prompted to enter the position of the element to be deleted.

7.  The deleteElement function is called with the provided position, and the array and size are updated accordingly.

8.  The updated array is then printed to verify the deletion and shifting of elements.

Note: This program assumes that the array contains integers. You can modify it to work with other types by changing the array type and modifying the input/output statements accordingly.

# 26

# Array Palindrome

Here’s a C++ program that checks if an array is a palindrome:

#include <iostream>
using namespace std;

bool isPalindrome(int arr[], int size) {
    int start = 0;
    int end = size - 1;

    while (start < end) {
        if (arr[start] != arr[end]) {
            return false;
        }
        start++;
        end--;
    }

    return true;
}

int main() {
    int arr[] = {1, 2, 3, 2, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    if (isPalindrome(arr, size)) {
        cout << "The array is a palindrome." << endl;
    } else {
        cout << "The array is not a palindrome." << endl;
    }

    return 0;
}

In this program, the isPalindrome function is defined to check whether an array is a palindrome. It takes two parameters: arr, which is the array to be checked, and size, which is the size of the array.

The function uses two indices, start and end, to compare elements from the beginning and end of the array. It starts by initializing start to 0 (the first element) and end to size - 1 (the last element).

The function enters a while loop that continues as long as start is less than end. Inside the loop, it compares arr[start] and arr[end]. If they are not equal, it means the array is not a palindrome, and the function returns false.

If the elements are equal, the function increments start and decrements end to move towards the center of the array. This process continues until start becomes greater than or equal to end.

If the while loop finishes without encountering any non-matching elements, the function returns true, indicating that the array is a palindrome.

In the main function, an example array is defined, and its size is calculated using the sizeof operator. The isPalindrome function is then called with the array and its size as arguments. Based on the return value, it prints whether the array is a palindrome or not.

Note that this program assumes that the array contains integer elements. You can modify it to work with other data types by changing the function signature and adjusting the comparison logic accordingly.

# 27

# Array Intersection

Here’s an example program in C++ that finds the intersection of two arrays:

#include <iostream>
#include <unordered_set>
#include <vector>

std::vector<int> findIntersection(const std::vector<int>& array1, const std::vector<int>& array2) {
    std::unordered_set<int> set1(array1.begin(), array1.end());  // Convert array1 to a set

    std::vector<int> result;
    for (const auto& element : array2) {
        if (set1.count(element) > 0) {
            result.push_back(element);  // Add common elements to the result vector
            set1.erase(element);        // Remove element from set1 to avoid duplicates
        }
    }

    return result;
}

int main() {
    std::vector<int> array1 = {1, 2, 3, 4, 5};
    std::vector<int> array2 = {3, 4, 5, 6, 7};

    std::vector<int> intersection = findIntersection(array1, array2);

    std::cout << "Intersection: ";
    for (const auto& element : intersection) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we define the findIntersection function that takes two vectors (array1 and array2) as input and returns a new vector containing the common elements. Here’s how the function works:

1.  We create an unordered set (set1) from array1 to efficiently check for the existence of elements during comparison.

2.  We initialize an empty vector (result) to store the common elements.

3.  We iterate over each element in array2.

4.  For each element, we use the count function of the set to check if it exists in set1\. If it does, it means it’s a common element.

5.  We add the common element to the result vector and remove it from set1 to avoid duplicates.

6.  Once the iteration is complete, we return the result vector.

7.  In the main function, we create two sample arrays (array1 and array2).

8.  We call the findIntersection function, passing in the two arrays, and store the result in the intersection vector.

9.  Finally, we print the elements of the intersection vector to demonstrate the common elements between the two arrays.

When you run this program, the output will be:

Intersection: 3 4 5

It shows the common elements between array1 and array2, which are 3, 4, and 5.

# 28

# Array Union

Here’s an example program in C++ that finds the union of two arrays and combines their elements into a new array without duplicates:

#include <iostream>
#include <unordered_set>
#include <vector>

std::vector<int> findUnion(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::unordered_set<int> uniqueElements;
    std::vector<int> unionArray;

    // Add elements from arr1 to the union array
    for (int num : arr1) {
        if (uniqueElements.find(num) == uniqueElements.end()) {
            uniqueElements.insert(num);
            unionArray.push_back(num);
        }
    }

    // Add elements from arr2 to the union array
    for (int num : arr2) {
        if (uniqueElements.find(num) == uniqueElements.end()) {
            uniqueElements.insert(num);
            unionArray.push_back(num);
        }
    }

    return unionArray;
}

int main() {
    // Example arrays
    std::vector<int> array1 = {1, 2, 3, 4, 5};
    std::vector<int> array2 = {4, 5, 6, 7, 8};

    std::vector<int> unionResult = findUnion(array1, array2);

    // Print the union array
    std::cout << "Union array: ";
    for (int num : unionResult) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we define a function findUnion that takes two arrays, arr1 and arr2, as input and returns the union of the arrays as a new array.

We use an unordered_set called uniqueElements to keep track of the unique elements encountered so far. This allows us to efficiently check for duplicates while iterating through the arrays.

We iterate over arr1 and add each element to the unionArray only if it is not already present in uniqueElements. Similarly, we iterate over arr2 and add each element to unionArray if it is not a duplicate.

Finally, we print the resulting union array.

When you run the program, the output will be:

Union array: 1 2 3 4 5 6 7 8

Note that the order of elements in the union array may vary since unordered_set does not guarantee a specific order.

# 29

# Array Difference

Here’s an example C++ program that finds the difference between two arrays and creates a new array with the unique elements:

#include <iostream>
#include <vector>
#include <algorithm>

// Function to find the difference between two arrays
std::vector<int> arrayDifference(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> difference;

    // Sort the arrays for efficient comparison
    std::vector<int> sortedArr1 = arr1;
    std::vector<int> sortedArr2 = arr2;
    std::sort(sortedArr1.begin(), sortedArr1.end());
    std::sort(sortedArr2.begin(), sortedArr2.end());

    // Find the unique elements in arr1
    for (int element : sortedArr1) {
        if (!std::binary_search(sortedArr2.begin(), sortedArr2.end(), element)) {
            difference.push_back(element);
        }
    }

    return difference;
}

int main() {
    // Example usage
    std::vector<int> arr1 = {1, 2, 3, 4, 5};
    std::vector<int> arr2 = {3, 4, 5, 6, 7};

    std::vector<int> result = arrayDifference(arr1, arr2);

    std::cout << "Elements unique to arr1: ";
    for (int element : result) {
        std::cout << element << " ";
    }

    return 0;
}

In this program, the arrayDifference function takes two std::vector<int> parameters, arr1 and arr2, and returns a new std::vector<int> containing the elements that are unique to arr1. Here’s a breakdown of how it works:

1.  The function first creates an empty vector difference to store the unique elements.

2.  To ensure efficient comparison, copies of arr1 and arr2 are created and sorted using std::sort.

3.  Then, each element in sortedArr1 is checked if it exists in sortedArr2 using std::binary_search. If it doesn’t exist, it means the element is unique to arr1, and it is added to the difference vector.

4.  Finally, the difference vector is returned from the function.

In the main function, we provide example arrays arr1 and arr2\. The arrayDifference function is called with these arrays, and the resulting vector is stored in the result variable. The unique elements are then printed using std::cout.

When you run this program, the output will be:

Elements unique to arr1: 1 2

This indicates that the elements 1 and 2 are unique to arr1 and are not present in arr2.

# 30

# Array Subset

Here’s a C++ program that checks if one array is a subset of another array:

#include <iostream>
#include <unordered_set>
using namespace std;

bool isSubset(int arr1[], int size1, int arr2[], int size2) {
    unordered_set<int> set;

    // Add all elements of arr1 to the set
    for (int i = 0; i < size1; i++) {
        set.insert(arr1[i]);
    }

    // Check if all elements of arr2 exist in the set
    for (int i = 0; i < size2; i++) {
        if (set.find(arr2[i]) == set.end()) {
            return false; // Element not found in set
        }
    }

    return true; // All elements found in set
}

int main() {
    int arr1[] = {1, 2, 3, 4, 5};
    int size1 = sizeof(arr1) / sizeof(arr1[0]);

    int arr2[] = {3, 4, 5};
    int size2 = sizeof(arr2) / sizeof(arr2[0]);

    if (isSubset(arr1, size1, arr2, size2)) {
        cout << "arr2 is a subset of arr1." << endl;
    } else {
        cout << "arr2 is not a subset of arr1." << endl;
    }

    return 0;
}

Explanation:

1.  The isSubset function takes two arrays (arr1 and arr2) as input, along with their respective sizes (size1 and size2).

2.  It uses an unordered_set called set to store all elements of arr1.

3.  The first for loop iterates over arr1 and inserts each element into the set using the insert function.

4.  The second for loop iterates over arr2 and checks if each element exists in the set using the find function. If an element is not found (find returns set.end()), it means it’s not a subset, and the function returns false.

5.  If all elements of arr2 are found in the set, the function returns true.

6.  In the main function, we define two arrays (arr1 and arr2) and their sizes (size1 and size2).

7.  We call the isSubset function with these arrays and sizes, and based on the return value, we output whether arr2 is a subset of arr1 or not.

In the provided example, the program will output “arr2 is a subset of arr1” because all elements of arr2 (3, 4, and 5) are present in arr1.

# 31

# Array Symmetry

Here’s a C++ program that checks if an array is symmetric:

#include <iostream>

bool isSymmetric(int arr[], int size) {
    int start = 0;
    int end = size - 1;

    while (start <= end) {
        if (arr[start] != arr[end]) {
            return false;
        }
        start++;
        end--;
    }

    return true;
}

int main() {
    int arr[] = {1, 2, 3, 3, 2, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    if (isSymmetric(arr, size)) {
        std::cout << "Array is symmetric." << std::endl;
    } else {
        std::cout << "Array is not symmetric." << std::endl;
    }

    return 0;
}

In this program, the isSymmetric function takes an array (arr) and its size (size) as parameters. It initializes two variables, start and end, to keep track of the indices from the beginning and end of the array, respectively.

The function then enters a while loop that continues as long as start is less than or equal to end. Within the loop, it compares the elements at arr[start] and arr[end]. If they are not equal, it means the array is not symmetric, and the function returns false.

If the loop completes without finding any non-matching elements, it means the array is symmetric, and the function returns true.

In the main function, an example array arr is declared with some symmetric values. The size of the array is calculated using the formula sizeof(arr) / sizeof(arr[0]). The isSymmetric function is then called with the array and its size, and the result is printed accordingly.

Keep in mind that this program assumes the array contains integer values. If you’re working with a different data type, you can modify the program accordingly.

# 32

# Array Sorting Order

Here’s an example program in C++ that checks if an array is sorted in ascending or descending order:

#include <iostream>

bool isAscending(int arr[], int size) {
    for (int i = 1; i < size; i++) {
        if (arr[i] < arr[i - 1])
            return false;
    }
    return true;
}

bool isDescending(int arr[], int size) {
    for (int i = 1; i < size; i++) {
        if (arr[i] > arr[i - 1])
            return false;
    }
    return true;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5}; // Example array

    int size = sizeof(arr) / sizeof(arr[0]);

    if (isAscending(arr, size))
        std::cout << "The array is sorted in ascending order." << std::endl;
    else if (isDescending(arr, size))
        std::cout << "The array is sorted in descending order." << std::endl;
    else
        std::cout << "The array is not sorted." << std::endl;

    return 0;
}

In this program, we define two functions: isAscending and isDescending.

The isAscending function checks if the array is sorted in ascending order by comparing each element with its previous element. If at any point an element is found to be smaller than the previous element, the function returns false, indicating that the array is not sorted in ascending order. If the loop completes without finding any out-of-order elements, the function returns true, indicating that the array is sorted in ascending order.

The isDescending function works similarly but checks if the array is sorted in descending order. It compares each element with its previous element, and if it finds an element that is greater than the previous element, it returns false. If the loop completes without finding any out-of-order elements, the function returns true, indicating that the array is sorted in descending order.

In the main function, we create an example array arr and calculate its size using the formula sizeof(arr) / sizeof(arr[0]). We then call the isAscending and isDescending functions with the array and its size to determine the sorting order. Based on the returned values, we print the appropriate message to indicate whether the array is sorted in ascending order, descending order, or not sorted at all.

Please note that this program assumes that the array contains integer values. You can modify the program to work with other data types or customize it to suit your specific needs.

# 33

# Array Majority Element

Here’s a C++ program that finds the majority element in an array using a map to track element frequencies:

#include <iostream>
#include <unordered_map>
#include <vector>

int findMajorityElement(const std::vector<int>& arr) {
    std::unordered_map<int, int> freqMap;

    // Count the frequency of each element in the array
    for (int num : arr) {
        freqMap[num]++;
    }

    // Find the element with frequency greater than half the array size
    int halfSize = arr.size() / 2;
    for (const auto& pair : freqMap) {
        if (pair.second > halfSize) {
            return pair.first;
        }
    }

    // No majority element found
    return -1;
}

int main() {
    std::vector<int> arr = {1, 2, 2, 2, 3, 2, 4, 2, 5};

    int majorityElement = findMajorityElement(arr);

    if (majorityElement != -1) {
        std::cout << "Majority element: " << majorityElement << std::endl;
    } else {
        std::cout << "No majority element found." << std::endl;
    }

    return 0;
}

Explanation:

1.  We start by including the necessary C++ standard libraries: iostream, unordered_map, and vector.

2.  The findMajorityElement function takes an input array arr as a parameter and returns the majority element if it exists, or -1 if there is no majority element.

3.  Inside the function, we create an unordered_map called freqMap to track the frequency of each element in the array. The key of the map represents the element, and the value represents its frequency.

4.  We iterate through the input array arr, and for each element, we increment its corresponding frequency in the freqMap using the operator++ of unordered_map.

5.  After counting the frequencies, we determine the threshold for a majority element by dividing the size of the array by 2 and storing it in the halfSize variable.

6.  We then iterate through the key-value pairs in the freqMap using a range-based for loop. For each pair, if the frequency (pair.second) is greater than halfSize, we have found a majority element, so we return the element (pair.first).

7.  If we finish the loop without finding a majority element, we return -1 to indicate that no majority element exists.

8.  In the main function, we create a sample array arr with some elements.

9.  We call the findMajorityElement function with arr as the argument and store the result in the majorityElement variable.

10.  Finally, we check the value of majorityElement. If it is not -1, we print the majority element. Otherwise, we print a message indicating that no majority element was found.

When you run this program, it will output “Majority element: 2” because the element 2 appears more than half of the time in the array {1, 2, 2, 2, 3, 2, 4, 2, 5}.

# 34

# Array Missing Element

Here’s a C++ program that finds the missing element in a sequence of numbers represented by an array using the method you described:

#include <iostream>

int findMissingElement(int arr[], int n) {
    int expectedSum = (n + 1) * (n + 2) / 2; // Calculate the sum of the expected sequence

    for (int i = 0; i < n; i++) {
        expectedSum -= arr[i]; // Subtract the sum of the array elements
    }

    return expectedSum;
}

int main() {
    int arr[] = {1, 2, 4, 5, 6}; // Example array
    int n = sizeof(arr) / sizeof(arr[0]);

    int missingElement = findMissingElement(arr, n);

    std::cout << "The missing element is: " << missingElement << std::endl;

    return 0;
}

In this program, we define a function findMissingElement that takes an array arr and its size n as input. The expected sum of the sequence is calculated using the formula (n + 1) * (n + 2) / 2, which is the sum of the first n+1 natural numbers.

We then iterate over the elements of the array and subtract each element from the expected sum. The resulting value will be the missing element, as all the other elements cancel out. Finally, the missing element is returned.

In the main function, we create an example array and calculate its size using the sizeof operator. We then call the findMissingElement function with the array and its size, and the missing element is printed to the console.

Note that this program assumes that the sequence of numbers is continuous, starting from 1\. If the sequence starts from a different number or has a different pattern, the formula for the expected sum needs to be adjusted accordingly.

# 35

# Array Range

Here’s an example of a C++ program that finds the range of an array while keeping track of the maximum and minimum values:

#include <iostream>

int findRange(int arr[], int size) {
    int minVal = arr[0];  // Initialize minVal with the first element of the array
    int maxVal = arr[0];  // Initialize maxVal with the first element of the array

    // Iterate through the array starting from the second element
    for (int i = 1; i < size; i++) {
        // Update minVal if a smaller value is found
        if (arr[i] < minVal) {
            minVal = arr[i];
        }

        // Update maxVal if a larger value is found
        if (arr[i] > maxVal) {
            maxVal = arr[i];
        }
    }

    // Calculate and return the range
    int range = maxVal - minVal;
    return range;
}

int main() {
    int arr[] = {5, 2, 9, 1, 7};
    int size = sizeof(arr) / sizeof(arr[0]);

    int range = findRange(arr, size);

    std::cout << "Range: " << range << std::endl;

    return 0;
}

Explanation:

1.  The findRange function takes an array (arr) and its size (size) as parameters and returns the range of the array.

2.  In the findRange function, two variables (minVal and maxVal) are initialized with the first element of the array.

3.  The for loop starts from the second element of the array (i = 1) and iterates through the rest of the array.

4.  Inside the loop, it checks if the current element is smaller than minVal or larger than maxVal and updates the respective variables accordingly.

5.  After the loop finishes, the range is calculated as the difference between maxVal and minVal.

6.  The range is returned from the findRange function.

7.  In the main function, an example array is declared and its size is calculated.

8.  The findRange function is called with the array and its size, and the result is printed to the console.

In the given example, the range of the array {5, 2, 9, 1, 7} is calculated to be 8.

# 36

# Array Product

Here’s a C++ program that calculates the product of all elements in an array:

#include <iostream>

int main() {
    const int SIZE = 5;  // Size of the array
    int arr[SIZE] = {2, 4, 6, 8, 10};  // Example array

    int product = 1;  // Variable to store the product

    // Iterate through the array and multiply the elements
    for (int i = 0; i < SIZE; i++) {
        product *= arr[i];
    }

    // Output the product
    std::cout << "The product of the elements in the array is: " << product << std::endl;

    return 0;
}

Explanation:

1.  We start by including the necessary header file, iostream, which provides input/output operations.

2.  In the main() function, we define the size of the array (SIZE) and initialize an array arr with example values. You can modify the size and contents of the array to fit your needs.

3.  We initialize a variable product to store the result of multiplying the array elements. We set it to 1 initially since multiplying by 1 does not change the value.

4.  Using a for loop, we iterate through the array from index 0 to SIZE-1.

5.  Inside the loop, we multiply each element of the array arr[i] with the current value of product and update product with the result.

6.  Finally, we output the calculated product using std::cout and end the line with std::endl.

When you run this program, it will output the product of all elements in the array based on the values you provided. In this case, the output will be 3840 (2 * 4 * 6 * 8 * 10).

# 37

# Array Partitioning

Here’s an example program in C++ that partitions an array into two subarrays based on the sign of the elements:

#include <iostream>
#include <vector>

void partitionArray(std::vector<int>& arr) {
    int i = 0; // Index for positive elements
    int j = arr.size() - 1; // Index for negative elements

    while (i < j) {
        // Find the first negative element from the left side
        while (arr[i] >= 0 && i < j)
            i++;

        // Find the first positive element from the right side
        while (arr[j] < 0 && i < j)
            j--;

        // Swap the positive and negative elements
        if (i < j)
            std::swap(arr[i], arr[j]);
    }
}

int main() {
    std::vector<int> arr = { 4, -7, 2, -9, 5, -3, 8, -1 };

    std::cout << "Original Array: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;

    partitionArray(arr);

    std::cout << "Partitioned Array: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;

    return 0;
}

In this program, we use the two-pointer approach to partition the array. The variable i represents the index for positive elements, and the variable j represents the index for negative elements. We start with i at the beginning of the array and j at the end.

We then use two nested while loops to find the first negative element from the left side (i) and the first positive element from the right side (j). Once we find these elements, we swap them to rearrange the array.

The process continues until i and j cross each other or meet, ensuring that all positive elements are on the left side and all negative elements are on the right side.

After the partitioning is complete, the program prints both the original array and the partitioned array for verification.

Here’s the output of the above program:

Original Array: 4 -7 2 -9 5 -3 8 -1
Partitioned Array: -7 -9 -3 -1 5 2 8 4

As you can see, the positive elements (4, 2, 5, 8) are on the left side, while the negative elements (-7, -9, -3, -1) are on the right side, as per the partitioning logic.

# 38

# Array Duplicates

Here’s an example program in C++ that uses a map to track element frequencies and identify duplicates in an array:

#include <iostream>
#include <map>
#include <vector>

std::vector<int> findDuplicates(const std::vector<int>& nums) {
    std::map<int, int> frequencyMap;
    std::vector<int> duplicates;

    // Count the frequency of each element in the array
    for (int num : nums) {
        frequencyMap[num]++;
    }

    // Check for duplicates based on frequency
    for (const auto& pair : frequencyMap) {
        if (pair.second > 1) {
            duplicates.push_back(pair.first);
        }
    }

    return duplicates;
}

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5, 2, 3, 5, 6, 7, 8, 8, 9, 10, 10};

    std::vector<int> duplicates = findDuplicates(numbers);

    std::cout << "Duplicate elements: ";
    for (int duplicate : duplicates) {
        std::cout << duplicate << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, we define a function findDuplicates that takes an array of integers (nums) as input and returns a vector of integers containing the duplicate elements found in the array.

To track the frequency of elements, we use a std::map<int, int> called frequencyMap. The keys of the map represent the elements in the array, and the values represent their frequencies. We iterate over each element in the nums array and increment the frequency count in the map accordingly.

After counting the frequencies, we iterate over the elements in the frequencyMap and check if their frequency is greater than 1\. If so, it means the element is a duplicate, and we add it to the duplicates vector.

In the main function, we create an example array of integers (numbers) and call the findDuplicates function to find the duplicate elements. Finally, we print the duplicate elements on the console.

When you run this program, the output will be:

Duplicate elements: 2 3 5 8 10

This indicates that the numbers 2, 3, 5, 8, and 10 are duplicates in the given array.

Using a map allows us to efficiently track the frequencies of elements while iterating over the array only once. This approach has a time complexity of O(n), where n is the size of the array, as we iterate over the array once and the map once.

# 39

# Array Even-Odd Partitioning

Here’s a C++ program that partitions an array into two subarrays, one containing even elements and the other containing odd elements:

#include <iostream>
#include <vector>

void evenOddPartition(std::vector<int>& arr) {
    int left = 0;
    int right = arr.size() - 1;

    while (left < right) {
        // Move left pointer to the right until it finds an odd element
        while (arr[left] % 2 == 0 && left < right) {
            left++;
        }

        // Move right pointer to the left until it finds an even element
        while (arr[right] % 2 != 0 && left < right) {
            right--;
        }

        // Swap the elements at left and right pointers
        if (left < right) {
            std::swap(arr[left], arr[right]);
        }
    }
}

int main() {
    // Example usage
    std::vector<int> arr = {2, 5, 8, 9, 12, 4, 7, 10};

    std::cout << "Original array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }

    evenOddPartition(arr);

    std::cout << "\nPartitioned array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }

    return 0;
}

In this program, the evenOddPartition function takes a reference to a vector arr and rearranges its elements such that even elements come before odd elements. It uses two pointers, left and right, which initially point to the first and last elements of the array, respectively.

The function uses a while loop to iterate until the left and right pointers meet. Inside the loop, it moves the left pointer to the right until it finds an odd element (using the condition arr[left] % 2 == 0), and it moves the right pointer to the left until it finds an even element (using the condition arr[right] % 2 != 0).

When an odd element is found on the left and an even element is found on the right, the elements are swapped using the std::swap function.

After the loop finishes, the array will be partitioned with even elements on the left side and odd elements on the right side. The main function demonstrates the usage of the evenOddPartition function with an example array.

Running this program will produce the following output:

Original array: 2 5 8 9 12 4 7 10
Partitioned array: 2 10 8 12 4 9 7 5

As you can see, the even elements (2 8 12 4 10) are on the left side of the array, and the odd elements (9 7 5) are on the right side.

# 40

# Array Zero Sum Subarray

Here’s a C++ program that uses prefix sums to find a subarray with a sum of zero in an array:

#include <iostream>
#include <unordered_map>
#include <vector>

std::vector<int> findZeroSumSubarray(const std::vector<int>& arr) {
    std::unordered_map<int, int> prefixSums;
    std::vector<int> result;
    int sum = 0;

    // Iterate through the array and compute prefix sums
    for (int i = 0; i < arr.size(); i++) {
        sum += arr[i];

        // Check if the current prefix sum already exists in the map
        if (sum == 0) {
            // Zero sum subarray found from index 0 to i
            result.push_back(0);
            result.push_back(i);
            return result;
        } else if (prefixSums.find(sum) != prefixSums.end()) {
            // Zero sum subarray found from index prefixSums[sum]+1 to i
            result.push_back(prefixSums[sum] + 1);
            result.push_back(i);
            return result;
        }

        // Store the current prefix sum and its corresponding index in the map
        prefixSums[sum] = i;
    }

    return result; // No zero sum subarray found
}

int main() {
    std::vector<int> arr = {4, 2, -3, 1, 6};
    std::vector<int> result = findZeroSumSubarray(arr);

    if (!result.empty()) {
        std::cout << "Zero sum subarray found from index " << result[0] << " to " << result[1] << std::endl;
        for (int i = result[0]; i <= result[1]; i++) {
            std::cout << arr[i] << " ";
        }
    } else {
        std::cout << "No zero sum subarray found." << std::endl;
    }

    return 0;
}

Explanation:

The program uses the concept of prefix sums and a hash map (unordered_map) to solve the problem efficiently.

1.  We start by initializing an unordered_map called prefixSums to store the prefix sums encountered during the iteration.

2.  We also declare a vector called result to store the starting and ending indices of the zero sum subarray (if found).

3.  We initialize a variable sum to keep track of the current prefix sum.

4.  We iterate through the array arr using a for loop.

5.  In each iteration, we update the sum by adding the current element arr[i].

6.  We check if the sum is zero. If it is, that means we have found a zero sum subarray from index 0 to i. We update the result vector accordingly and return it.

7.  If the sum is not zero, we check if the current prefix sum sum exists in the prefixSums map. If it does, that means we have found a zero sum subarray from index prefixSums[sum]+1 to i. We update the result vector and return it.

8.  If the current prefix sum does not exist in the prefixSums map, we store it along with its index i in the map.

9.  After the loop finishes, if no zero sum subarray is found, an empty result vector is returned.

10.  In the main function, we create an example array arr and call the findZeroSumSubarray function to get the result.

11.  If the result vector is not empty, we print the indices of the zero sum subarray and the elements of the subarray itself. Otherwise, we print a message indicating that no zero sum subarray was found.

Using prefix sums and hashing techniques helps us achieve an efficient time complexity of O(N), where N is the size of the input array. The space complexity is also O(N) due to the storage of prefix sums in the unordered_map.

# 41

# Array Longest Increasing Subarray

Here’s an example program in C++ that finds the longest increasing subarray in an array:

#include <iostream>
#include <vector>

std::vector<int> findLongestIncreasingSubarray(const std::vector<int>& array) {
    std::vector<int> longestSubarray;
    std::vector<int> currentSubarray;

    for (int i = 0; i < array.size(); ++i) {
        if (i == 0 || array[i] <= array[i - 1]) {
            // Reset the current subarray if the current element is less than or equal to the previous element
            currentSubarray.clear();
        }

        currentSubarray.push_back(array[i]);

        if (currentSubarray.size() > longestSubarray.size()) {
            // Update the longest subarray if the current subarray is longer
            longestSubarray = currentSubarray;
        }
    }

    return longestSubarray;
}

int main() {
    std::vector<int> array = {1, 2, 3, 2, 5, 7, 8, 9, 1, 2, 3, 4};

    std::vector<int> longestIncreasingSubarray = findLongestIncreasingSubarray(array);

    std::cout << "Longest increasing subarray: ";
    for (int num : longestIncreasingSubarray) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this program, the function findLongestIncreasingSubarray takes an array as input and returns the longest increasing subarray found in it. It uses two vectors: longestSubarray to store the longest subarray found so far, and currentSubarray to keep track of the currently processed subarray.

The iteration through the array starts with i = 0\. If i is 0 or the current element array[i] is less than or equal to the previous element array[i - 1], it means a new increasing subarray starts at the current element. In such cases, currentSubarray is cleared to start a new subarray.

Regardless of whether a new subarray starts or not, the current element is always added to currentSubarray. After that, the program checks if the length of currentSubarray is greater than the length of longestSubarray. If it is, longestSubarray is updated with the contents of currentSubarray.

After the loop completes, longestSubarray contains the longest increasing subarray found in the input array, and it is returned by the function.

In the main function, an example array is created ({1, 2, 3, 2, 5, 7, 8, 9, 1, 2, 3, 4}), and the findLongestIncreasingSubarray function is called on this array. The resulting subarray is then printed to the console.

When you run this program, the output will be:

Longest increasing subarray: 2 5 7 8 9

This indicates that the longest increasing subarray in the given array is [2, 5, 7, 8, 9].

# 42

# Array Longest Common Subsequence

Here’s a C++ program that finds the longest common subsequence between two arrays using dynamic programming:

#include <iostream>
#include <vector>

std::vector<int> longestCommonSubsequence(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    int m = arr1.size();
    int n = arr2.size();

    // Create a 2D table to store the lengths of common subsequences
    std::vector<std::vector<int>> dp(m + 1, std::vector<int>(n + 1, 0));

    // Building the dp table using dynamic programming
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (arr1[i - 1] == arr2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = std::max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    // Backtracking to find the longest common subsequence
    std::vector<int> lcs;
    int i = m, j = n;
    while (i > 0 && j > 0) {
        if (arr1[i - 1] == arr2[j - 1]) {
            lcs.push_back(arr1[i - 1]);
            --i;
            --j;
        } else if (dp[i - 1][j] > dp[i][j - 1]) {
            --i;
        } else {
            --j;
        }
    }

    std::reverse(lcs.begin(), lcs.end()); // Reverse the result to get the correct order

    return lcs;
}

int main() {
    std::vector<int> arr1 = {1, 2, 3, 4, 5};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};

    std::vector<int> lcs = longestCommonSubsequence(arr1, arr2);

    std::cout << "Longest Common Subsequence: ";
    for (int num : lcs) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}

Explanation:

1.  The longestCommonSubsequence function takes two input arrays, arr1 and arr2, and returns the longest common subsequence between them.

2.  We create a 2D table, dp, with dimensions (m+1) x (n+1), where m and n are the lengths of arr1 and arr2 respectively. This table will store the lengths of common subsequences between prefixes of the arrays.

3.  We initialize the table with zeros.

4.  We iterate through the arrays using two nested loops, comparing elements from arr1 and arr2\. If the elements are equal, we increment the value in dp by 1 compared to the value in the previous diagonal element (dp[i-1][j-1]). If the elements are not equal, we take the maximum value between the element above (dp[i-1][j]) and the element on the left (dp[i][j-1]).

5.  After the dynamic programming step, the dp[m][n] element will contain the length of the longest common subsequence.

6.  We perform backtracking to find the actual elements of the longest common subsequence. Starting from the bottom-right of the dp table, we compare elements of arr1 and arr2\. If they are equal, we add the element to the lcs vector and move diagonally up-left. Otherwise, we move either up or left, depending on which adjacent element in the dp table is larger.

7.  Finally, we reverse the lcs vector to get the correct order of the elements.

8.  In the main function, we initialize two example arrays, arr1 and arr2, and call the longestCommonSubsequence function to find the longest common subsequence.

9.  We print the resulting longest common subsequence to the console.

This approach uses dynamic programming to build a table that stores the lengths of common subsequences between prefixes of the input arrays. By backtracking through the table, we can find the actual elements of the longest common subsequence. The time complexity of this solution is O(m * n), where m and n are the lengths of the input arrays.

# 43

# Array Longest Palindromic Subsequence

Here’s a C++ program that finds the longest palindromic subsequence in an array using dynamic programming:

#include <iostream>
#include <vector>

using namespace std;

int longestPalindromicSubsequence(const vector<int>& arr) {
    int n = arr.size();
    vector<vector<int>> dp(n, vector<int>(n, 0));

    // Base case: every element is a palindrome of length 1
    for (int i = 0; i < n; i++) {
        dp[i][i] = 1;
    }

    // Build the table bottom-up
    for (int len = 2; len <= n; len++) {
        for (int i = 0; i < n - len + 1; i++) {
            int j = i + len - 1;
            if (arr[i] == arr[j] && len == 2) {
                dp[i][j] = 2;
            } else if (arr[i] == arr[j]) {
                dp[i][j] = dp[i + 1][j - 1] + 2;
            } else {
                dp[i][j] = max(dp[i][j - 1], dp[i + 1][j]);
            }
        }
    }

    // The longest palindromic subsequence length is stored in dp[0][n-1]
    return dp[0][n - 1];
}

int main() {
    vector<int> arr = {1, 2, 3, 2, 1, 5};

    int longest = longestPalindromicSubsequence(arr);
    cout << "Longest Palindromic Subsequence Length: " << longest << endl;

    return 0;
}

Explanation:

The dynamic programming approach involves building a 2D table dp to store the lengths of the longest palindromic subsequences for different subarrays of the given array arr.

*   The table dp is initialized with all elements set to 0.

*   The base case is when the length of the subarray is 1 (i.e., len = 1). In this case, every element itself is a palindrome of length 1, so dp[i][i] is set to 1.

*   Then, we build the table bottom-up for increasing subarray lengths (len). For each subarray length, we iterate through all possible subarrays of that length.

*   If the first and last elements of the subarray are the same (arr[i] == arr[j]), we check the length of the subarray:

*   If len is 2, it means we have only two elements that are the same, so the length of the palindromic subsequence is 2.

*   If len is greater than 2, we add 2 to the length of the longest palindromic subsequence of the subarray arr[i+1][j-1], as the first and last elements are the same.

*   If the first and last elements are different, we take the maximum length of the palindromic subsequence by either excluding the last element (dp[i][j-1]) or excluding the first element (dp[i+1][j]).

Finally, the length of the longest palindromic subsequence is stored in dp[0][n-1], where n is the size of the array.

In the provided example, the array is {1, 2, 3, 2, 1, 5}, and the longest palindromic subsequence is {1, 2, 2, 1} with a length of 4, which is the output of the program.

Note: This solution assumes that the array contains only integer elements. For other data types, you may need to modify the comparison operations accordingly.

# 44

# Array Longest Bitonic Subarray

To find the longest bitonic subarray in an array using dynamic programming, you can follow these steps:

1.  Initialize two arrays: increasing[] and decreasing[] with the same size as the input array. These arrays will store the length of the longest increasing and decreasing subarrays ending at each index, respectively.

2.  Initialize the increasing[] array with all 1s since a subarray of length 1 is always increasing. Initialize the decreasing[] array with all 1s as well since a subarray of length 1 is also decreasing.

3.  Traverse the input array from left to right and update the increasing[] array. For each index i, compare the element at index i with the previous elements. If the current element is greater than the previous element, set increasing[i] = increasing[i – 1] + 1, indicating an increasing subarray is extended. Otherwise, set increasing[i] = 1, as the subarray starting at index i is not increasing.

4.  Traverse the input array from right to left and update the decreasing[] array. For each index i, compare the element at index i with the next elements. If the current element is greater than the next element, set decreasing[i] = decreasing[i + 1] + 1, indicating a decreasing subarray is extended. Otherwise, set decreasing[i] = 1, as the subarray starting at index i is not decreasing.

5.  Initialize variables maxLen and startIdx to keep track of the maximum length of the bitonic subarray and its starting index, respectively. Iterate over the array and compare the sum of increasing[i] and decreasing[i] – 1 (excluding the current element) with maxLen. If it is greater, update maxLen and startIdx accordingly.

6.  The length of the longest bitonic subarray will be maxLen. You can print the elements of the subarray by iterating from startIdx to startIdx + maxLen.

Here’s a C++ implementation of the above algorithm:

#include <iostream>
using namespace std;

void findLongestBitonicSubarray(int arr[], int n) {
    int increasing[n];
    int decreasing[n];

    increasing[0] = 1;
    decreasing[n - 1] = 1;

    for (int i = 1; i < n; i++) {
        increasing[i] = (arr[i] > arr[i - 1]) ? increasing[i - 1] + 1 : 1;
    }

    for (int i = n - 2; i >= 0; i--) {
        decreasing[i] = (arr[i] > arr[i + 1]) ? decreasing[i + 1] + 1 : 1;
    }

    int maxLen = 1;
    int startIdx = 0;

    for (int i = 0; i < n; i++) {
        int len = increasing[i] + decreasing[i] - 1;
        if (len > maxLen) {
            maxLen = len;
            startIdx = i - increasing[i] + 1;
        }
    }

    cout << "Longest bitonic subarray: ";
    for (int i = startIdx; i < startIdx + maxLen; i++) {
        cout << arr[i] << " ";
    }
}

int main() {
    int arr[] = {3, 5, 8, 4, 5, 9, 10, 8, 5, 3, 4};
    int n = sizeof(arr) / sizeof(arr[0]);

    findLongestBitonicSubarray(arr, n);

    return 0;
}

In the example above, the input array is {3, 5, 8, 4, 5, 9, 10, 8, 5, 3, 4}. The longest bitonic subarray is {4, 5, 9, 10, 8, 5, 3}, which starts at index 3 and has a length of 7.

# 45

# Array Maximum Sum Subarray

Here’s a C++ program that uses Kadane’s algorithm to find the maximum sum subarray in an array:

#include <iostream>
#include <climits>

// Function to find the maximum sum subarray using Kadane's algorithm
int maxSubarraySum(int arr[], int size) {
    int maxSum = INT_MIN;
    int currentSum = 0;

    for (int i = 0; i < size; i++) {
        currentSum += arr[i];

        if (currentSum > maxSum)
            maxSum = currentSum;

        if (currentSum < 0)
            currentSum = 0;
    }

    return maxSum;
}

int main() {
    int arr[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
    int size = sizeof(arr) / sizeof(arr[0]);

    int maxSum = maxSubarraySum(arr, size);

    std::cout << "Maximum sum of subarray: " << maxSum << std::endl;

    return 0;
}

Explanation: Kadane’s algorithm is an efficient algorithm to solve the maximum subarray sum problem in linear time complexity. It uses a dynamic programming approach.

The algorithm scans the array from left to right, keeping track of the maximum sum found so far (maxSum) and the current sum of the subarray (currentSum).

At each element, the algorithm adds the current element to currentSum. If currentSum becomes greater than maxSum, it updates maxSum to the new value of currentSum. This step ensures that maxSum always stores the maximum sum encountered so far.

If currentSum becomes negative, it means that including the current element will only decrease the sum, so the algorithm resets currentSum to 0\. This step allows the algorithm to discard any negative sum subarrays, as they cannot contribute to the maximum sum.

Finally, the algorithm returns the value of maxSum, which represents the maximum sum subarray in the given array.

In the example program, the array arr is defined with some sample values. The maxSubarraySum function is called to find the maximum sum subarray, and the result is printed to the console.

Running this program will output:

Maximum sum of subarray: 7

This indicates that the maximum sum subarray in the given array is [4, -1, -2, 1, 5].

# 46

# Array Circular Subarray Sum

To find the maximum sum of a circular subarray in an array, we can modify Kadane’s algorithm slightly. Kadane’s algorithm is used to find the maximum sum of a subarray in a linear array. By modifying it, we can handle circular subarrays as well.

Here’s how you can write a C++ program to find the maximum sum of a circular subarray using the modified Kadane’s algorithm:

#include <iostream>
#include <vector>
#include <algorithm>

int kadane(std::vector<int>& arr) {
    int maxSum = arr[0];
    int currentSum = arr[0];

    for (int i = 1; i < arr.size(); i++) {
        currentSum = std::max(arr[i], currentSum + arr[i]);
        maxSum = std::max(maxSum, currentSum);
    }

    return maxSum;
}

int maxCircularSubarraySum(std::vector<int>& arr) {
    int linearMaxSum = kadane(arr);  // Maximum sum of a linear subarray

    // If all elements are negative, linearMaxSum is the answer
    if (linearMaxSum < 0)
        return linearMaxSum;

    int arraySum = 0;
    for (int i = 0; i < arr.size(); i++) {
        arraySum += arr[i];
        arr[i] = -arr[i];  // Negate the elements of the array
    }

    int circularMaxSum = arraySum + kadane(arr);
    return std::max(linearMaxSum, circularMaxSum);
}

int main() {
    std::vector<int> arr = { 8, -4, 3, -5, 4 };
    int maxSum = maxCircularSubarraySum(arr);
    std::cout << "Maximum circular subarray sum: " << maxSum << std::endl;
    return 0;
}

In this program, the kadane function is the modified Kadane’s algorithm that finds the maximum sum of a linear subarray. The maxCircularSubarraySum function first calculates the maximum sum of a linear subarray using kadane and stores it in linearMaxSum. If the linearMaxSum is negative, it means that all elements in the array are negative, and in this case, we return the linearMaxSum as the result.

Otherwise, we calculate the total sum of all elements in the array and negate each element. Then, we pass this modified array to kadane to find the maximum sum of a subarray that wraps around from the end to the beginning of the array. The sum of this circular subarray is calculated by adding the total sum of the array to the maximum sum of the modified array.

Finally, we return the maximum of the linearMaxSum and circularMaxSum as the result, which represents the maximum sum of a circular subarray in the given array.

In the example above, the maximum circular subarray sum is 15, which corresponds to the subarray [3, -5, 4, 8, -4].

# 47

# Array Kth Smallest Element

To find the Kth smallest element in an array using sorting or partitioning algorithms, you can follow these steps:

1.  Sorting Algorithm Approach:

*   Initialize the array with the given elements.

*   Sort the array in ascending order using any efficient sorting algorithm, such as quicksort, mergesort, or heapsort.

*   The Kth smallest element will then be located at the index (K – 1) in the sorted array, considering 0-based indexing.

*   Return the element at that index.

Here’s an example implementation using the sorting approach:

#include <iostream>
#include <algorithm>

int findKthSmallest(int arr[], int size, int k) {
    std::sort(arr, arr + size);  // Sort the array

    return arr[k - 1];  // Return the Kth smallest element
}

int main() {
    int arr[] = {10, 2, 8, 4, 6, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    int kthSmallest = findKthSmallest(arr, size, k);
    std::cout << "The " << k << "th smallest element is: " << kthSmallest << std::endl;

    return 0;
}

In this example, we have an array arr with elements [10, 2, 8, 4, 6, 5]. We want to find the 3rd smallest element (k = 3) using the sorting algorithm. After sorting the array in ascending order, we get [2, 4, 5, 6, 8, 10]. The 3rd smallest element is 5, so the program outputs “The 3rd smallest element is: 5”.

1.  Partitioning Algorithm Approach (Quickselect):

*   Initialize the array with the given elements.

*   Apply the Quickselect algorithm to partition the array around a pivot element.

*   By choosing an appropriate pivot, you can efficiently find the Kth smallest element without fully sorting the entire array.

*   If the pivot index is equal to (K – 1), return the pivot element.

*   Otherwise, recursively apply the Quickselect algorithm on either the left or right partition depending on the pivot index and K value.

Here’s an example implementation using the partitioning approach:

#include <iostream>
#include <algorithm>

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            std::swap(arr[i], arr[j]);
        }
    }
    std::swap(arr[i + 1], arr[high]);
    return i + 1;
}

int quickselect(int arr[], int low, int high, int k) {
    if (low < high) {
        int pivotIndex = partition(arr, low, high);

        if (pivotIndex == k - 1)
            return arr[pivotIndex];
        else if (pivotIndex > k - 1)
            return quickselect(arr, low, pivotIndex - 1, k);
        else
            return quickselect(arr, pivotIndex + 1, high, k);
    }
    return arr[low];
}

int findKthSmallest(int arr[], int size, int k) {
    return quickselect(arr, 0, size - 1, k);
}

int main() {
    int arr[] = {10, 2, 8, 4, 6, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    int kthSmallest = findKthSmallest(arr, size, k);
    std::cout << "The " << k << "th smallest element is: " << kthSmallest << std::endl;

    return 0;
}

In this example, we have the same array arr as before. We again want to find the 3rd smallest element (k = 3) but using the partitioning algorithm. After applying the Quickselect algorithm, the 3rd smallest element is found to be 5, so the program outputs “The 3rd smallest element is: 5”.

Both approaches can be used to find the Kth smallest element in an array. The sorting approach has a time complexity of O(n log n), where n is the size of the array. The partitioning approach using Quickselect has an average time complexity of O(n) but can degrade to O(n^2) in the worst case. However, Quickselect is often faster than sorting when K is relatively small compared to the size of the array.

# 48

# Array Consecutive Elements

Here’s an example program in C++ that checks if an array contains consecutive elements:

#include <iostream>
#include <algorithm>

bool isConsecutive(int arr[], int size) {
    // Sort the array in ascending order
    std::sort(arr, arr + size);

    // Check if each element is consecutive with its adjacent element
    for (int i = 0; i < size - 1; i++) {
        if (arr[i] + 1 != arr[i + 1])
            return false;
    }

    return true;
}

int main() {
    int size;
    std::cout << "Enter the size of the array: ";
    std::cin >> size;

    int* arr = new int[size];
    std::cout << "Enter the elements of the array: ";
    for (int i = 0; i < size; i++) {
        std::cin >> arr[i];
    }

    if (isConsecutive(arr, size)) {
        std::cout << "The array contains consecutive elements." << std::endl;
    } else {
        std::cout << "The array does not contain consecutive elements." << std::endl;
    }

    delete[] arr;
    return 0;
}

Explanation:

1.  The function isConsecutive takes an array (arr) and its size (size) as parameters and returns a boolean value indicating whether the array contains consecutive elements or not.

2.  Inside the isConsecutive function, we use the std::sort function from the <algorithm> library to sort the array in ascending order. Sorting the array is necessary because it brings the consecutive elements together.

3.  After sorting the array, we iterate through the elements from the first element to the second-to-last element using a for loop.

4.  Within the loop, we check if the current element (arr[i]) plus 1 is equal to the next element (arr[i + 1]). If they are not consecutive, we return false immediately.

5.  If we complete the loop without finding any non-consecutive elements, we return true, indicating that the array contains consecutive elements.

6.  In the main function, we first prompt the user to enter the size of the array.

7.  Then, we dynamically allocate an array of integers using the new operator and store the user-provided values.

8.  We call the isConsecutive function with the array and its size and display an appropriate message based on the returned boolean value.

9.  Finally, we release the dynamically allocated memory using the delete[] operator.

Note: This program assumes that the input array contains distinct elements. If the array can have duplicates and you still want to consider it as containing consecutive elements, you can modify the comparison in the isConsecutive function to if (arr[i] != arr[i + 1]) instead of if (arr[i] + 1 != arr[i + 1]).

# 49

# Array Peaks and Valleys

To rearrange the elements of an array in a “peaks and valleys” pattern, you can follow these steps:

1.  Define a function, let’s call it peaksAndValleys, that takes an array and its size as input parameters.

2.  Traverse the array from index 1 to index n-2 (where n is the size of the array) in steps of 2\. This step ensures that you visit every other element in the array.

3.  For each element at index i, compare it with its adjacent elements at indices i-1 and i+1.

4.  If the current element is smaller than both its adjacent elements, swap it with the larger of the two adjacent elements.

5.  If the current element is larger than both its adjacent elements, swap it with the smaller of the two adjacent elements.

Here’s a sample implementation in C++:

#include <iostream>

void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

void peaksAndValleys(int arr[], int size) {
    for (int i = 1; i < size - 1; i += 2) {
        if (arr[i] < arr[i - 1] && arr[i] < arr[i + 1]) {
            if (arr[i - 1] > arr[i + 1])
                swap(arr[i], arr[i - 1]);
            else
                swap(arr[i], arr[i + 1]);
        }
        else if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
            if (arr[i - 1] < arr[i + 1])
                swap(arr[i], arr[i - 1]);
            else
                swap(arr[i], arr[i + 1]);
        }
    }
}

int main() {
    int arr[] = {5, 3, 1, 2, 3};
    int size = sizeof(arr) / sizeof(arr[0]);

    peaksAndValleys(arr, size);

    std::cout << "Array after rearranging in peaks and valleys pattern: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}

In the above example, the initial array is {5, 3, 1, 2, 3}. After applying the peaksAndValleys function, the array will be rearranged to {3, 5, 1, 3, 2}.

Note that this implementation assumes the array has at least three elements. If the array has fewer elements, you may need to add additional checks to handle such cases.

# 50

# Array Majority Elements

Here’s an example program in C++ that uses the Boyer-Moore Voting Algorithm to find the majority elements in an array:

#include <iostream>
#include <vector>

std::vector<int> findMajorityElements(std::vector<int>& nums) {
    int n = nums.size();
    int num1 = 0, num2 = 0;  // Potential candidates for majority elements
    int count1 = 0, count2 = 0;  // Count of occurrences for each candidate

    // Step 1: Find potential candidates using Boyer-Moore Voting Algorithm
    for (int num : nums) {
        if (num1 == num) {
            count1++;
        } else if (num2 == num) {
            count2++;
        } else if (count1 == 0) {
            num1 = num;
            count1 = 1;
        } else if (count2 == 0) {
            num2 = num;
            count2 = 1;
        } else {
            count1--;
            count2--;
        }
    }

    // Step 2: Count the occurrences of potential candidates
    count1 = count2 = 0;
    for (int num : nums) {
        if (num == num1) {
            count1++;
        } else if (num == num2) {
            count2++;
        }
    }

    // Step 3: Check if the potential candidates are majority elements
    std::vector<int> result;
    if (count1 > n / 3) {
        result.push_back(num1);
    }
    if (count2 > n / 3) {
        result.push_back(num2);
    }

    return result;
}

int main() {
    std::vector<int> nums = {3, 1, 3, 1, 2, 2, 2};  // Sample array

    std::vector<int> majorityElements = findMajorityElements(nums);

    std::cout << "Majority Elements: ";
    for (int element : majorityElements) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}

Explanation:

The Boyer-Moore Voting Algorithm is an efficient algorithm to find the majority element in an array. It is based on the observation that for an array to have a majority element (appearing more than n/2 times), there can be at most two majority elements.

The algorithm extends this concept to find majority elements appearing more than n/3 times. Here’s how it works:

1.  Initialize two potential candidates, num1 and num2, and their corresponding counts, count1 and count2, to 0.

2.  Traverse the array and perform the following operations:

*   If the current number is equal to num1, increment count1.

*   If the current number is equal to num2, increment count2.

*   If count1 is 0, update num1 with the current number and set count1 to 1.

*   If count2 is 0, update num2 with the current number and set count2 to 1.

*   If none of the above conditions match, decrement count1 and count2 by 1.

1.  After the traversal, we have two potential candidates, num1 and num2, but they may not necessarily be majority elements. To determine if they are indeed majority elements, we need to count their occurrences in the array again.

2.  Traverse the array and count the occurrences of num1 and num2 in separate variables, count1 and count2.

3.  Check if count1 is greater than n/3 (where n is the size of the array). If it is, num1 is a majority element, so add it to the result vector.

4.  Check if count2 is greater than n/3\. If it is, num2 is a majority element, so add it to the result vector.

5.  Return the result vector containing the majority elements.

In the example program, we initialize an array nums and call the findMajorityElements function to find the majority elements in the array. Finally, we print the majority elements obtained from the function.

Note: This implementation assumes that there can be at most two majority elements appearing more than n/3 times in the array. If you need to handle a different threshold or a different number of potential majority elements, you would need to modify the code accordingly.

# 51

# Array Leader Elements

Here’s an example program in C++ that finds the leader elements in an array by iterating through the array from right to left:

#include <iostream>
#include <vector>

std::vector<int> findLeaderElements(const std::vector<int>& arr) {
    std::vector<int> leaders;  // Stores the leader elements

    int currentLeader = arr.back();  // Initialize the current leader with the last element

    // Iterate through the array from right to left
    for (int i = arr.size() - 1; i >= 0; i--) {
        // If the current element is greater than the current leader, it becomes the new leader
        if (arr[i] > currentLeader) {
            currentLeader = arr[i];
            leaders.push_back(currentLeader);
        }
    }

    // Reverse the order of leaders to match the original array order
    std::reverse(leaders.begin(), leaders.end());

    return leaders;
}

int main() {
    std::vector<int> array = {16, 17, 4, 3, 5, 2};

    std::vector<int> leaders = findLeaderElements(array);

    std::cout << "Leader elements in the array are: ";
    for (int leader : leaders) {
        std::cout << leader << " ";
    }
    std::cout << std::endl;

    return 0;
}

Explanation:

1.  The findLeaderElements function takes an array arr as input and returns a vector containing the leader elements found.

2.  It starts by initializing an empty vector leaders to store the leader elements.

3.  The variable currentLeader is initialized with the last element of the array arr.back(), assuming it is the leader.

4.  The loop iterates through the array from right to left using a decrementing loop counter i.

5.  In each iteration, it checks if the current element arr[i] is greater than the currentLeader.

6.  If it is greater, it means that the current element is a new leader. It updates the currentLeader and adds it to the leaders vector.

7.  After the loop finishes, the leaders vector is reversed to match the original order of the array.

8.  In the main function, a sample array is created, and the findLeaderElements function is called to find the leader elements.

9.  The leader elements are then printed on the console.

For the given sample array {16, 17, 4, 3, 5, 2}, the output will be:

Leader elements in the array are: 17 5 2

These are the elements that are greater than all the elements to their right in the array.

# 52

# Array Equilibrium Index

Here’s an example program in C++ that finds the equilibrium index of an array:

#include <iostream>
#include <vector>

int findEquilibriumIndex(const std::vector<int>& arr) {
    int n = arr.size();

    // Calculate prefix sums
    std::vector<int> prefixSum(n, 0);
    prefixSum[0] = arr[0];
    for (int i = 1; i < n; i++) {
        prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    // Iterate through the array to find the equilibrium index
    for (int i = 0; i < n; i++) {
        int leftSum = i > 0 ? prefixSum[i - 1] : 0;
        int rightSum = prefixSum[n - 1] - prefixSum[i];

        if (leftSum == rightSum) {
            return i;
        }
    }

    return -1;  // No equilibrium index found
}

int main() {
    std::vector<int> arr = {-7, 1, 5, 2, -4, 3, 0};
    int equilibriumIndex = findEquilibriumIndex(arr);

    if (equilibriumIndex != -1) {
        std::cout << "Equilibrium index found at index " << equilibriumIndex << std::endl;
    } else {
        std::cout << "No equilibrium index found." << std::endl;
    }

    return 0;
}

Explanation:

1.  We define a function findEquilibriumIndex that takes an array arr as input and returns the equilibrium index. The function first calculates the prefix sums of the array.

2.  To calculate prefix sums, we create a new vector prefixSum of the same size as arr and initialize its first element with arr[0]. Then, we iterate through the array starting from index 1, and at each step, we add the current element to the sum of previous elements to get the prefix sum. This way, prefixSum[i] will contain the sum of elements from arr[0] to arr[i] for each index i.

3.  After calculating the prefix sums, we iterate through the array again to find the equilibrium index. For each index i, we calculate the sum of elements to the left (leftSum) and the sum of elements to the right (rightSum). The left sum is the prefix sum at index i-1, and the right sum is the total sum of the array minus the prefix sum at index i.

4.  If the left sum is equal to the right sum, we have found an equilibrium index, so we return that index.

5.  If no equilibrium index is found after iterating through the entire array, we return -1.

In the main function, we create a sample array arr and call the findEquilibriumIndex function. If an equilibrium index is found, we print its value; otherwise, we indicate that no equilibrium index was found. In this example, the output would be “Equilibrium index found at index 3” since the equilibrium index is at index 3 where the sum of elements to the left (-7+1+5) is equal to the sum of elements to the right (-4+3+0).

# 53

# Array Rearrangement

Here’s a C++ program that rearranges the elements of an array so that even elements appear before odd elements using two pointers:

#include <iostream>
using namespace std;

void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

void rearrangeArray(int arr[], int size) {
    int left = 0;
    int right = size - 1;

    while (left < right) {
        while (arr[left] % 2 == 0 && left < right)
            left++;

        while (arr[right] % 2 == 1 && left < right)
            right--;

        if (left < right) {
            swap(arr[left], arr[right]);
            left++;
            right--;
        }
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << "Original Array: ";
    printArray(arr, size);

    rearrangeArray(arr, size);

    cout << "Rearranged Array: ";
    printArray(arr, size);

    return 0;
}

In this program, we use the two-pointer technique to swap the elements and maintain the desired order. The rearrangeArray function takes an array (arr) and its size (size) as input and performs the rearrangement.

We start with two pointers, left and right, pointing to the first and last elements of the array, respectively. We then iterate until the two pointers meet or cross each other.

Inside the while loop, we move the left pointer to the right until we find an odd number or until the left and right pointers meet. Similarly, we move the right pointer to the left until we find an even number or until the left and right pointers meet.

If the left pointer is still to the left of the right pointer, we swap the elements at the left and right indices and increment the left pointer by one and decrement the right pointer by one.

After the rearrangement is complete, we print the rearranged array using the printArray function.

The output of the above program will be:

Original Array: 1 2 3 4 5 6 7 8 9 10
Rearranged Array: 2 4 6 8 10 5 7 3 9 1

As you can see, the even elements are now placed before the odd elements while maintaining the original order of even and odd elements in the array.

# 54

# Array Max Consecutive Ones

Here’s an example program in C++ that finds the maximum number of consecutive ones in an array of zeros and ones:

#include <iostream>

int findMaxConsecutiveOnes(int arr[], int size) {
    int maxConsecutiveOnes = 0;
    int currentConsecutiveOnes = 0;

    for (int i = 0; i < size; i++) {
        if (arr[i] == 1) {
            currentConsecutiveOnes++;
            if (currentConsecutiveOnes > maxConsecutiveOnes) {
                maxConsecutiveOnes = currentConsecutiveOnes;
            }
        } else {
            currentConsecutiveOnes = 0;
        }
    }

    return maxConsecutiveOnes;
}

int main() {
    int arr[] = {1, 1, 0, 1, 1, 1, 0, 1, 0, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    int maxConsecutiveOnes = findMaxConsecutiveOnes(arr, size);

    std::cout << "Maximum consecutive ones: " << maxConsecutiveOnes << std::endl;

    return 0;
}

In this program, the findMaxConsecutiveOnes function takes an array arr and its size size as input and returns the maximum number of consecutive ones found in the array.

We use two variables: maxConsecutiveOnes to keep track of the maximum consecutive ones encountered so far, and currentConsecutiveOnes to keep track of the current count of consecutive ones.

We iterate through the array using a for loop. If the current element arr[i] is equal to 1, it means we have encountered a consecutive one. We increment currentConsecutiveOnes by 1\. Then, we check if currentConsecutiveOnes is greater than maxConsecutiveOnes. If it is, we update maxConsecutiveOnes with the new value.

If the current element is 0, it means the consecutive ones sequence has ended. We reset currentConsecutiveOnes to 0 to start counting a new sequence.

After iterating through the entire array, we return the value of maxConsecutiveOnes as the result.

In the main function, we define an example array arr and calculate its size. We then call the findMaxConsecutiveOnes function with the array and its size as arguments. Finally, we print the result to the console.

When you run this program, it will output:

Maximum consecutive ones: 3

indicating that the maximum number of consecutive ones in the array is 3.

# 55

# Array Zigzag Traversal

To traverse a 2D array in a zigzag pattern, you can use nested loops and conditional statements in C++. Here’s an example program that demonstrates the zigzag traversal:

#include <iostream>

const int ROWS = 3;
const int COLS = 4;

void zigzagTraversal(int arr[ROWS][COLS]) {
    bool isMovingUp = true; // Flag to indicate the direction of traversal

    for (int i = 0; i < ROWS; i++) {
        // For even rows, traverse from left to right
        if (isMovingUp) {
            for (int j = 0; j < COLS; j++) {
                std::cout << arr[i][j] << " ";
            }
        }
        // For odd rows, traverse from right to left
        else {
            for (int j = COLS - 1; j >= 0; j--) {
                std::cout << arr[i][j] << " ";
            }
        }

        isMovingUp = !isMovingUp; // Toggle the direction flag
    }
}

int main() {
    int arr[ROWS][COLS] = {{1, 2, 3, 4},
                           {5, 6, 7, 8},
                           {9, 10, 11, 12}};

    zigzagTraversal(arr);

    return 0;
}

In this program, we define a zigzagTraversal function that takes a 2D array as a parameter. We also define a flag isMovingUp to keep track of the traversal direction.

Inside the zigzagTraversal function, we iterate over each row of the array using a for loop. For even rows (starting from index 0), we traverse the columns from left to right. For odd rows, we traverse the columns from right to left.

We use an if-else statement to determine the traversal direction based on the isMovingUp flag. If the flag is true, we traverse the columns from left to right. If the flag is false, we traverse the columns from right to left.

After traversing a row, we toggle the isMovingUp flag by using isMovingUp = !isMovingUp, which switches the direction for the next row.

In the main function, we create a sample 2D array arr and call the zigzagTraversal function to perform the zigzag traversal.

When you run this program, it will output the elements of the 2D array in a zigzag pattern:

1 2 3 4 8 7 6 5 9 10 11 12

That’s how you can achieve a zigzag traversal of a 2D array using nested loops and conditional statements in C++.

# 56

# Array Spiral Traversal

Below is an example of a C++ program that performs a spiral traversal of a 2D array using four pointers to define the boundaries:

#include <iostream>
#include <vector>

using namespace std;

void spiralTraversal(const vector<vector<int>>& matrix) {
    int rows = matrix.size();
    int cols = matrix[0].size();

    int top = 0; // top boundary
    int bottom = rows - 1; // bottom boundary
    int left = 0; // left boundary
    int right = cols - 1; // right boundary

    while (top <= bottom && left <= right) {
        // Traverse top row
        for (int i = left; i <= right; ++i) {
            cout << matrix[top][i] << " ";
        }
        top++;

        // Traverse right column
        for (int i = top; i <= bottom; ++i) {
            cout << matrix[i][right] << " ";
        }
        right--;

        // Check if there are remaining rows or columns
        if (top <= bottom) {
            // Traverse bottom row
            for (int i = right; i >= left; --i) {
                cout << matrix[bottom][i] << " ";
            }
            bottom--;
        }

        if (left <= right) {
            // Traverse left column
            for (int i = bottom; i >= top; --i) {
                cout << matrix[i][left] << " ";
            }
            left++;
        }
    }
}

int main() {
    vector<vector<int>> matrix = {
        { 1, 2, 3, 4 },
        { 5, 6, 7, 8 },
        { 9, 10, 11, 12 },
        { 13, 14, 15, 16 }
    };

    spiralTraversal(matrix);

    return 0;
}

In this program, the spiralTraversal function takes a 2D matrix as input and performs the spiral traversal. It initializes four pointers: top, bottom, left, and right, which represent the boundaries of the spiral.

The traversal is performed in a clockwise manner, starting from the top left corner and moving towards the right.

1.  First, it traverses the top row from left to right using a for loop. The top pointer is then incremented to exclude this row from future iterations.

2.  Next, it traverses the right column from top to bottom using another for loop. The right pointer is decremented to exclude this column from future iterations.

3.  It then checks if there are remaining rows by comparing top and bottom pointers. If there are, it traverses the bottom row from right to left and decrements the bottom pointer.

4.  Finally, it checks if there are remaining columns by comparing left and right pointers. If there are, it traverses the left column from bottom to top and increments the left pointer.

The process continues until all elements of the matrix have been traversed.

In the main function, a sample matrix is created, and the spiralTraversal function is called to perform the traversal. The output is printed to the console.

You can modify the program by changing the input matrix to test it with different 2D arrays.

# 57

# Array Pascal’s Triangle

Here’s an example program in C++ that generates Pascal’s triangle as a 2D array:

#include <iostream>
using namespace std;

const int MAX_ROWS = 10;

int main() {
    int pascalTriangle[MAX_ROWS][MAX_ROWS];

    // Initialize the first row with 1
    pascalTriangle[0][0] = 1;

    // Generate Pascal's triangle
    for (int i = 1; i < MAX_ROWS; i++) {
        // First element of each row is always 1
        pascalTriangle[i][0] = 1;

        // Calculate the rest of the elements based on the previous row
        for (int j = 1; j < i; j++) {
            pascalTriangle[i][j] = pascalTriangle[i - 1][j - 1] + pascalTriangle[i - 1][j];
        }

        // Last element of each row is always 1
        pascalTriangle[i][i] = 1;
    }

    // Display Pascal's triangle
    for (int i = 0; i < MAX_ROWS; i++) {
        // Print leading spaces to create a triangular shape
        for (int k = 0; k < MAX_ROWS - i - 1; k++) {
            cout << " ";
        }

        // Print the elements of each row
        for (int j = 0; j <= i; j++) {
            cout << pascalTriangle[i][j] << " ";
        }

        cout << endl;
    }

    return 0;
}

Let’s go through the code:

1.  We start by defining a constant MAX_ROWS to specify the maximum number of rows in Pascal’s triangle. You can change this value as per your requirement.

2.  We declare a 2D array pascalTriangle with dimensions MAX_ROWS x MAX_ROWS to store the triangle elements.

3.  We initialize the first element of the first row with 1 because it is always 1 in Pascal’s triangle.

4.  We use nested loops to generate the triangle. The outer loop (i) runs from 1 to MAX_ROWS - 1 and represents each row of the triangle.

5.  Inside the outer loop, we set the first element of each row to 1 since it is always 1.

6.  The inner loop (j) runs from 1 to i - 1 and calculates each element of the current row based on the elements of the previous row.

*   Each element in Pascal’s triangle is the sum of the two elements above it in the previous row. So, we access the required elements from the previous row using pascalTriangle[i - 1][j - 1] and pascalTriangle[i - 1][j]. We add them together and store the result in pascalTriangle[i][j].

1.  After calculating all the elements of the current row, we set the last element of the row to 1 since it is always 1.

2.  Finally, we use another set of nested loops to display the triangle. The outer loop (i) iterates over each row, and the inner loop (j) iterates over each element in the row.

3.  Before printing each row, we add leading spaces to create a triangular shape. We print (MAX_ROWS - i - 1) spaces to align the elements correctly.

4.  Inside the inner loop, we simply print each element of the triangle followed by a space.

5.  After printing each row, we move to the next line using cout << endl;.

That’s it! When you run this program, it will generate and display Pascal’s triangle as a 2D array. Adjust the MAX_ROWS constant as per your preference to generate a larger triangle if desired.

# 58

# Array Rotated Sorted Search

To search for a target element in a rotated sorted array using a modified binary search algorithm, you can follow these steps in C++:

1.  Define a function, let’s call it search, that takes in the rotated sorted array, the target element, the start index, and the end index as parameters. The initial call to this function can be made with search(arr, target, 0, size-1) where arr is the rotated sorted array and size is the size of the array.

2.  Check if the start index is greater than the end index. If it is, return -1 to indicate that the target element was not found in the array.

3.  Calculate the middle index as (start + end) / 2.

4.  Check if the middle element is equal to the target element. If it is, return the middle index as the position of the target element in the array.

5.  If the first half of the array (from the start index to the middle index) is sorted, perform a binary search on that half. Check if arr[start] <= arr[mid] to determine if the first half is sorted.a. If the target element falls within the range of the sorted first half (i.e., target >= arr[start] and target <= arr[mid]), make a recursive call to search(arr, target, start, mid-1).b. If the target element does not fall within the range of the sorted first half, make a recursive call to search(arr, target, mid+1, end) to search in the second half of the array.

6.  If the second half of the array (from the middle index to the end index) is sorted, perform a binary search on that half. Check if arr[mid] <= arr[end] to determine if the second half is sorted.a. If the target element falls within the range of the sorted second half (i.e., target >= arr[mid] and target <= arr[end]), make a recursive call to search(arr, target, mid+1, end).b. If the target element does not fall within the range of the sorted second half, make a recursive call to search(arr, target, start, mid-1) to search in the first half of the array.

7.  If the target element is not found in either the first half or the second half, return -1 to indicate that it was not found in the array.

Here’s an example implementation of the search function in C++:

int search(vector<int>& arr, int target, int start, int end) {
    if (start > end)
        return -1;

    int mid = (start + end) / 2;

    if (arr[mid] == target)
        return mid;

    if (arr[start] <= arr[mid]) {
        if (target >= arr[start] && target <= arr[mid])
            return search(arr, target, start, mid - 1);
        else
            return search(arr, target, mid + 1, end);
    }

    if (arr[mid] <= arr[end]) {
        if (target >= arr[mid] && target <= arr[end])
            return search(arr, target, mid + 1, end);
        else
            return search(arr, target, start, mid - 1);
    }

    return -1;
}

You can use this search function to search for a target element in a rotated sorted array by passing the array, target element, start index (0), and end index (size-1) as arguments. The function will return the index of the target element if found or -1 if not found.

Note: This implementation assumes that the rotated sorted array does not contain any duplicate elements.

# 59

# Array Maximal Square

Here’s a C++ program that uses dynamic programming to find the size of the largest square of ones in a binary matrix:

#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int maximalSquare(vector<vector<int>>& matrix) {
    int rows = matrix.size();
    if (rows == 0) return 0;

    int cols = matrix[0].size();
    if (cols == 0) return 0;

    vector<vector<int>> dp(rows, vector<int>(cols, 0));
    int maxSquareSize = 0;

    // Initialize the first row
    for (int i = 0; i < cols; i++) {
        dp[0][i] = matrix[0][i];
        maxSquareSize = max(maxSquareSize, dp[0][i]);
    }

    // Initialize the first column
    for (int i = 0; i < rows; i++) {
        dp[i][0] = matrix[i][0];
        maxSquareSize = max(maxSquareSize, dp[i][0]);
    }

    // Fill in the remaining cells of the dp matrix
    for (int i = 1; i < rows; i++) {
        for (int j = 1; j < cols; j++) {
            if (matrix[i][j] == 1) {
                // Take the minimum value of the adjacent cells and add 1
                dp[i][j] = min(dp[i-1][j], min(dp[i][j-1], dp[i-1][j-1])) + 1;
                maxSquareSize = max(maxSquareSize, dp[i][j]);
            }
        }
    }

    return maxSquareSize * maxSquareSize;
}

int main() {
    vector<vector<int>> matrix = {
        {1, 0, 1, 0, 0},
        {1, 0, 1, 1, 1},
        {1, 1, 1, 1, 1},
        {1, 0, 0, 1, 0}
    };

    int largestSquareSize = maximalSquare(matrix);
    cout << "Size of the largest square of ones: " << largestSquareSize << endl;

    return 0;
}

Explanation:

1.  We define a function maximalSquare that takes a 2D binary matrix as input and returns the size of the largest square of ones.

2.  We first check the number of rows and columns in the matrix. If either of them is zero, it means the matrix is empty, and we return 0.

3.  We create a 2D vector dp of the same size as the input matrix to store the dynamic programming values. Each cell dp[i][j] represents the size of the largest square with the bottom-right corner at position (i, j).

4.  We initialize the first row and the first column of dp with the corresponding values from the input matrix. We also update the maxSquareSize variable accordingly.

5.  Starting from the second row and the second column, we iterate over each cell of the input matrix. If the current cell is 1, we take the minimum value of the adjacent cells (left, up, and diagonal-left) in dp and add 1 to it. This is because if all the adjacent cells are part of a square, we can extend the square by one unit.

6.  While filling the dp matrix, we keep track of the maximum square size encountered so far in the maxSquareSize variable.

7.  Finally, we return the square of maxSquareSize, as the variable represents the length of the sides of the square.

In the given example, the output will be:

Size of the largest square of ones: 4

This means there is a square of size 4×4 in the binary matrix.

# 60

# Array Frequency Count

There are multiple ways to track element frequencies in C++, either by using a map or an array. Let me explain both approaches to you.

1.  Using a Map: Using a map allows you to associate each element of the array with its frequency. The key of the map represents the element, and the corresponding value represents its frequency.

Here’s an example code that counts the frequency of each element in an array using a map:

#include <iostream>
#include <map>

int main() {
    int arr[] = {1, 2, 3, 1, 2, 2, 4, 3, 1, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::map<int, int> frequencyMap;

    // Count the frequency of each element
    for (int i = 0; i < size; i++) {
        frequencyMap[arr[i]]++;
    }

    // Print the frequencies
    for (const auto& pair : frequencyMap) {
        std::cout << "Element " << pair.first << ": Frequency " << pair.second << std::endl;
    }

    return 0;
}

In this code, we define a map frequencyMap where the keys are the elements from the array, and the values are the corresponding frequencies. We iterate over the array, incrementing the frequency for each element in the map. Finally, we print the frequencies by iterating over the map and accessing the key-value pairs.

1.  Using an Array: Another approach is to use an array to track the element frequencies. This approach works when the elements in the array have a limited range, such as integers in a specific range.

Here’s an example code that counts the frequency of each element in an array using an array:

#include <iostream>

const int MAX_RANGE = 1000; // Maximum range of elements in the array

int main() {
    int arr[] = {1, 2, 3, 1, 2, 2, 4, 3, 1, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    int frequency[MAX_RANGE] = {0}; // Initialize the frequency array with zeros

    // Count the frequency of each element
    for (int i = 0; i < size; i++) {
        frequency[arr[i]]++;
    }

    // Print the frequencies
    for (int i = 0; i < MAX_RANGE; i++) {
        if (frequency[i] > 0) {
            std::cout << "Element " << i << ": Frequency " << frequency[i] << std::endl;
        }
    }

    return 0;
}

In this code, we define an array frequency of size MAX_RANGE to track the frequencies. The index of the array represents the element, and the value at that index represents its frequency. We iterate over the array, incrementing the frequency at the corresponding index. Finally, we print the frequencies by iterating over the frequency array and checking for non-zero values.

Both approaches, using a map or an array, have their advantages and disadvantages. Using a map is more flexible and can handle elements with a wide range of values, but it requires extra memory to store the map. On the other hand, using an array is more memory-efficient but requires a limited range of elements.

# 61

# Array Median

Here’s a C++ program that finds the median element in an array:

#include <iostream>
#include <algorithm>

double findMedian(int arr[], int size) {
    // Sort the array
    std::sort(arr, arr + size);

    // Determine the median
    if (size % 2 == 0) {
        // If the size is even, average the middle two elements
        int midIndex = size / 2;
        return (arr[midIndex - 1] + arr[midIndex]) / 2.0;
    } else {
        // If the size is odd, return the middle element
        return arr[size / 2];
    }
}

int main() {
    // Example usage
    int array[] = {5, 3, 9, 1, 7};
    int size = sizeof(array) / sizeof(array[0]);

    double median = findMedian(array, size);
    std::cout << "Median: " << median << std::endl;

    return 0;
}

Explanation:

1.  The findMedian function takes an array (arr) and its size (size) as input.

2.  It uses the std::sort function from the <algorithm> library to sort the array in ascending order.

3.  After sorting, it checks if the size of the array is even or odd.

4.  If the size is even, it calculates the average of the two middle elements (arr[midIndex - 1] and arr[midIndex]), where midIndex is size / 2.

5.  If the size is odd, it directly returns the middle element (arr[size / 2]).

6.  In the main function, an example array is defined (array) along with its size (size).

7.  The findMedian function is called with the array and size as arguments, and the result is stored in the median variable.

8.  Finally, the median is printed to the console.

Note: This program assumes that the array elements are of integer type. If you want to find the median of an array with elements of a different type, you would need to modify the program accordingly.

# 62

# Array Inversion Count

Here’s an example program in C++ that counts the number of inversions in an array using the modified merge sort algorithm:

#include <iostream>
#include <vector>

using namespace std;

long long mergeAndCount(vector<int>& arr, vector<int>& temp, int left, int mid, int right) {
    int i = left;
    int j = mid + 1;
    int k = left;
    long long inversionCount = 0;

    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
            inversionCount += mid - i + 1; // Count inversions
        }
    }

    while (i <= mid) {
        temp[k++] = arr[i++];
    }

    while (j <= right) {
        temp[k++] = arr[j++];
    }

    for (i = left; i <= right; i++) {
        arr[i] = temp[i];
    }

    return inversionCount;
}

long long mergeSortAndCount(vector<int>& arr, vector<int>& temp, int left, int right) {
    long long inversionCount = 0;

    if (left < right) {
        int mid = left + (right - left) / 2;

        inversionCount += mergeSortAndCount(arr, temp, left, mid);
        inversionCount += mergeSortAndCount(arr, temp, mid + 1, right);
        inversionCount += mergeAndCount(arr, temp, left, mid, right);
    }

    return inversionCount;
}

long long countInversions(vector<int>& arr) {
    int n = arr.size();
    vector<int> temp(n);
    return mergeSortAndCount(arr, temp, 0, n - 1);
}

int main() {
    vector<int> arr = {5, 3, 2, 4, 1};
    long long inversionCount = countInversions(arr);
    cout << "Number of inversions: " << inversionCount << endl;

    return 0;
}

In this program, we use a modified merge sort algorithm to count the number of inversions in the array. The mergeAndCount function merges two sorted subarrays and counts the inversions. The mergeSortAndCount function recursively divides the array into smaller subarrays, performs merge sort, and accumulates the inversion counts. Finally, the countInversions function is a wrapper function that initializes the temporary array and starts the merge sort process.

To solve this problem using a Fenwick tree (also known as a Binary Indexed Tree or BIT), we can modify the merge sort algorithm as follows:

1.  Create a Fenwick tree data structure that supports efficient range sum queries and point updates. The Fenwick tree should be initialized with all zeros.

2.  Initialize a variable inversionCount to 0.

3.  Traverse the array from right to left.

4.  For each element arr[i], query the Fenwick tree for the sum of elements less than arr[i]. Add this sum to inversionCount.

5.  Update the Fenwick tree by incrementing the value at index arr[i] by 1.

Here’s an example implementation:

#include <iostream>
#include <vector>

using namespace std;

class FenwickTree {
private:
    vector<int> BIT;

public:
    FenwickTree(int size) {
        BIT.resize(size + 1, 0);
    }

    void update(int index, int value) {
        while (index < BIT.size()) {
            BIT[index] += value;
            index += index & (-index);
        }
    }

    int query(int index) {
        int sum = 0;
        while (index > 0) {
            sum += BIT[index];
            index -= index & (-index);
        }
        return sum;
    }
};

long long countInversions(vector<int>& arr) {
    int n = arr.size();
    FenwickTree bit(n);
    long long inversionCount = 0;

    for (int i = n - 1; i >= 0; i--) {
        inversionCount += bit.query(arr[i] - 1);
        bit.update(arr[i], 1);
    }

    return inversionCount;
}

int main() {
    vector<int> arr = {5, 3, 2, 4, 1};
    long long inversionCount = countInversions(arr);
    cout << "Number of inversions: " << inversionCount << endl;

    return 0;
}

In this implementation, we define a FenwickTree class that encapsulates the Fenwick tree operations. The update function updates the tree by incrementing the value at the given index, and the query function calculates the sum of elements up to the given index.

In the countInversions function, we iterate over the array in reverse order. For each element, we query the Fenwick tree for the sum of elements less than the current element, add it to inversionCount, and update the Fenwick tree accordingly.

Both the modified merge sort and Fenwick tree approaches have a time complexity of O(n log n), where n is the size of the array. The modified merge sort has a slightly larger constant factor, but it may be easier to understand and implement in certain scenarios. The Fenwick tree approach requires additional space to store the Fenwick tree itself.

# 63

# Array Next Permutation

In C++, you can use the std::next_permutation algorithm from the <algorithm> library to find the lexicographically next permutation of an array. Here’s an example program that demonstrates its usage:

#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    // Create an array or vector with elements
    std::vector<int> arr = {1, 2, 3};

    // Find the next permutation
    std::next_permutation(arr.begin(), arr.end());

    // Print the next permutation
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this example, the initial array is {1, 2, 3}. The std::next_permutation function is called with the range of the array, arr.begin() and arr.end(). It modifies the array to the next lexicographically greater permutation if it exists, and returns true. If the array is already the highest possible permutation, it rearranges it to the lowest possible permutation and returns false. In our case, the next permutation is {1, 3, 2}, so it will be printed.

If you don’t have access to the std::next_permutation function or want to understand how it works internally, you can implement the next permutation manually. Here’s an example of how you can achieve that:

#include <iostream>
#include <vector>
#include <algorithm>

void nextPermutation(std::vector<int>& nums) {
    int n = nums.size();
    int i = n - 2;

    // Find the first element from the right that is smaller than its next element
    while (i >= 0 && nums[i] >= nums[i + 1]) {
        i--;
    }

    if (i >= 0) {
        // Find the element just larger than nums[i] to swap with
        int j = n - 1;
        while (j > i && nums[j] <= nums[i]) {
            j--;
        }

        // Swap nums[i] and nums[j]
        std::swap(nums[i], nums[j]);
    }

    // Reverse the remaining elements
    std::reverse(nums.begin() + i + 1, nums.end());
}

int main() {
    // Create an array or vector with elements
    std::vector<int> arr = {1, 2, 3};

    // Find the next permutation
    nextPermutation(arr);

    // Print the next permutation
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}

In this manual implementation, the nextPermutation function takes a reference to the array and modifies it in place. It follows the logic of finding the next permutation:

1.  Starting from the right, find the first element that is smaller than its next element. Let’s call its index i.

2.  If i is greater than or equal to zero, find the element just larger than nums[i] from the right. Let’s call its index j.

3.  Swap nums[i] and nums[j].

4.  Reverse the elements from index i + 1 to the end of the array.

This sequence of steps guarantees that we obtain the next lexicographically greater permutation.

Both the std::next_permutation function and the manual implementation provide a way to find the next permutation of an array efficiently. You can choose either approach based on your preference and requirements.

# 64

# Array Three Sum

To solve the Array Three Sum problem using sorting and the two-pointers technique in C++, you can follow these steps:

1.  Sort the given array in non-decreasing order. This step is crucial for the two-pointers technique to work efficiently.

2.  Initialize an empty vector to store the unique triplets that add up to the target sum.

3.  Iterate through the sorted array up to the second-to-last element. For each element at index i, perform the two-pointers technique on the remaining array elements to find pairs that add up to the target sum.

4.  Within the iteration, set two pointers: left pointing to i+1, and right pointing to the last element of the array.

5.  While left is less than right, perform the following steps:

*   Calculate the current sum as arr[i] + arr[left] + arr[right].

*   If the current sum is equal to the target sum, add the triplet [arr[i], arr[left], arr[right]] to the result vector and increment left and decrement right to find more possible solutions.

*   If the current sum is less than the target sum, increment left to increase the sum.

*   If the current sum is greater than the target sum, decrement right to decrease the sum.

1.  Continue the iteration until all possible combinations have been examined.

Here’s the C++ implementation of the above algorithm:

#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<vector<int>> threeSum(vector<int>& nums, int target) {
    vector<vector<int>> result;
    int n = nums.size();

    // Sort the array in non-decreasing order
    sort(nums.begin(), nums.end());

    // Iterate through the array
    for (int i = 0; i < n - 2; i++) {
        // Two-pointers technique
        int left = i + 1;
        int right = n - 1;

        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];

            if (sum == target) {
                result.push_back({nums[i], nums[left], nums[right]});

                // Skip duplicates for left pointer
                while (left < right && nums[left] == nums[left + 1])
                    left++;

                // Skip duplicates for right pointer
                while (left < right && nums[right] == nums[right - 1])
                    right--;

                left++;
                right--;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }

        // Skip duplicates for the current element
        while (i < n - 2 && nums[i] == nums[i + 1])
            i++;
    }

    return result;
}

int main() {
    vector<int> nums = {-1, 0, 1, 2, -1, -4};
    int target = 0;

    vector<vector<int>> triplets = threeSum(nums, target);

    // Display the triplets that add up to the target sum
    for (const auto& triplet : triplets) {
        for (int num : triplet) {
            cout << num << " ";
        }
        cout << endl;
    }

    return 0;
}

In the above example, the input array nums contains [-1, 0, 1, 2, -1, -4], and the target sum is 0\. The program finds the unique triplets that add up to the target sum using the sorting and two-pointers technique and displays them as output.

# 65

# Array Two Sum

Approach 1: Using a Map

1.  Initialize an empty map, let’s call it “numMap,” where the key will be the array element, and the value will be its index.

2.  Iterate through the array elements using a loop.

3.  For each element, calculate the difference between the target sum and the current element. Let’s call this difference “complement.”

4.  Check if the complement exists in the map. If it does, return the indices of the current element and its complement.

5.  If the complement is not found in the map, insert the current element and its index into the map.

6.  If the loop finishes without finding a solution, it means there are no two elements that add up to the target sum.

Here’s the code implementation:

#include <iostream>
#include <unordered_map>
#include <vector>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::unordered_map<int, int> numMap;
    std::vector<int> result;

    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        if (numMap.count(complement)) {
            result.push_back(numMap[complement]);
            result.push_back(i);
            break;
        }
        numMap[nums[i]] = i;
    }

    return result;
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    std::vector<int> result = twoSum(nums, target);

    if (result.size() == 2) {
        std::cout << "Indices: " << result[0] << ", " << result[1] << std::endl;
        std::cout << "Elements: " << nums[result[0]] << ", " << nums[result[1]] << std::endl;
    } else {
        std::cout << "No solution found." << std::endl;
    }

    return 0;
}

Approach 2: Using Two Pointers

1.  Sort the array in non-decreasing order.

2.  Initialize two pointers, “left” and “right,” pointing to the beginning and end of the array, respectively.

3.  Iterate while the “left” pointer is less than the “right” pointer.

4.  Calculate the sum of the elements at the “left” and “right” pointers.

5.  If the sum is equal to the target, return the indices of the elements at the “left” and “right” pointers.

6.  If the sum is less than the target, increment the “left” pointer.

7.  If the sum is greater than the target, decrement the “right” pointer.

8.  If the loop finishes without finding a solution, it means there are no two elements that add up to the target sum.

Here’s the code implementation:

#include <iostream>
#include <vector>
#include <algorithm>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::vector<int> result;
    std::vector<int> sortedNums = nums; // Create a copy of the input array
    std::sort(sortedNums.begin(), sortedNums.end()); // Sort the array in non-decreasing order

    int left = 0;
    int right = sortedNums.size() - 1;

    while (left < right) {
        int sum = sortedNums[left] + sortedNums[right];
        if (sum == target) {
            // Find the indices of the elements in the original array
            int indexLeft = std::find(nums.begin(), nums.end(), sortedNums[left]) - nums.begin();
            int indexRight = std::find(nums.begin(), nums.end(), sortedNums[right]) - nums.begin();

            result.push_back(indexLeft);
            result.push_back(indexRight);
            break;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return result;
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    std::vector<int> result = twoSum(nums, target);

    if (result.size() == 2) {
        std::cout << "Indices: " << result[0] << ", " << result[1] << std::endl;
        std::cout << "Elements: " << nums[result[0]] << ", " << nums[result[1]] << std::endl;
    } else {
        std::cout << "No solution found." << std::endl;
    }

    return 0;
}

Both approaches will give you the indices of two elements in the array that add up to the target sum. You can modify the code according to your requirements and input format.

# 66

# Array Valid Mountain

To determine if an array represents a valid mountain in C++, we need to check the following conditions:

1.  The array must have at least three elements.

2.  The elements of the array must be strictly increasing until a peak is reached.

3.  After reaching the peak, the elements must be strictly decreasing until the end of the array.

To traverse the array and check these conditions, we can follow these steps:

1.  Initialize an index variable, “i,” to 0 and check if the array size is less than 3\. If it is, return false as it cannot form a valid mountain.

2.  Increment the index “i” while the elements at the current and next positions are in increasing order. This step ensures that we traverse the array until we reach the peak or the end of the increasing sequence.

3.  Check if “i” is at the beginning or end of the array. If it is, return false as a mountain should have both an increasing and decreasing part.

4.  Increment the index “i” while the elements at the current and next positions are in decreasing order. This step ensures that we traverse the array from the peak until the end, checking for the decreasing part.

5.  If “i” reaches the end of the array, return true as all conditions for a valid mountain have been met. Otherwise, return false.

Here’s the C++ code implementing the above algorithm:

#include <iostream>
#include <vector>

bool isValidMountain(std::vector<int>& arr) {
    int n = arr.size();
    int i = 0;

    // Condition 1: Array must have at least 3 elements
    if (n < 3) {
        return false;
    }

    // Increasing sequence until peak is reached
    while (i < n - 1 && arr[i] < arr[i + 1]) {
        i++;
    }

    // Condition 2: Check if "i" is at the beginning or end
    if (i == 0 || i == n - 1) {
        return false;
    }

    // Decreasing sequence after the peak
    while (i < n - 1 && arr[i] > arr[i + 1]) {
        i++;
    }

    // Condition 3: Check if "i" reaches the end of the array
    return i == n - 1;
}

int main() {
    std::vector<int> arr = {1, 2, 3, 4, 5, 4, 3, 2, 1};

    if (isValidMountain(arr)) {
        std::cout << "The array represents a valid mountain." << std::endl;
    } else {
        std::cout << "The array does not represent a valid mountain." << std::endl;
    }

    return 0;
}

In this example, the array {1, 2, 3, 4, 5, 4, 3, 2, 1} represents a valid mountain, so the output will be “The array represents a valid mountain.”

# 67

# Array Sliding Window Maximum

Here’s an example program in C++ that finds the maximum element in every contiguous subarray of size k using a deque:

#include <iostream>
#include <deque>
#include <vector>

using namespace std;

vector<int> findMaxSlidingWindow(const vector<int>& nums, int k) {
    vector<int> result;
    deque<int> dq;

    // Process the first k elements separately
    for (int i = 0; i < k; i++) {
        // Remove all elements smaller than the current element
        while (!dq.empty() && nums[i] >= nums[dq.back()])
            dq.pop_back();

        dq.push_back(i);
    }

    // Process the remaining elements
    for (int i = k; i < nums.size(); i++) {
        // The front element of the deque is the maximum for the previous window
        result.push_back(nums[dq.front()]);

        // Remove elements outside the current window
        while (!dq.empty() && dq.front() <= i - k)
            dq.pop_front();

        // Remove all elements smaller than the current element
        while (!dq.empty() && nums[i] >= nums[dq.back()])
            dq.pop_back();

        dq.push_back(i);
    }

    // Add the maximum of the last window
    result.push_back(nums[dq.front()]);

    return result;
}

int main() {
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;

    vector<int> result = findMaxSlidingWindow(nums, k);

    cout << "Maximum elements in every subarray of size " << k << " are: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}

Explanation:

1.  We use a deque (double-ended queue) to store the indices of elements in the array. The deque stores indices in a way that the maximum element for the current window is always at the front of the deque.

2.  We process the first k elements separately and maintain the deque such that it only contains indices with elements in descending order. This ensures that the front element of the deque is the maximum for the window.

3.  Then, for each subsequent window, we add the maximum of the previous window to the result vector, remove any indices that are outside the current window from the front of the deque, and remove any indices with elements smaller than the current element from the back of the deque. We push the current index to the back of the deque.

4.  After processing all windows, we add the maximum of the last window to the result vector.

5.  Finally, we return the result vector containing the maximum elements for each subarray.

The time complexity of this algorithm is O(n), where n is the size of the input array, as we only iterate through the array once. The deque operations take constant time, and each element is pushed and popped from the deque at most once.

# 68

# Array Dutch National Flag

The Dutch National Flag problem is a sorting problem that involves arranging an array containing only three distinct elements (0s, 1s, and 2s) in a specific order. The problem gets its name from the Dutch national flag, which consists of three horizontal stripes: red, white, and blue, each representing the values 0, 1, and 2, respectively.

To solve this problem, you can use three pointers to partition the array into three sections: the “low” pointer, the “mid” pointer, and the “high” pointer.

Here’s an example program in C++ that sorts the array using the Dutch National Flag algorithm:

#include <iostream>
using namespace std;

void dutchNationalFlag(int arr[], int size) {
    int low = 0;      // Pointer for elements less than 1
    int mid = 0;      // Pointer for elements equal to 1
    int high = size - 1; // Pointer for elements greater than 1

    while (mid <= high) {
        if (arr[mid] == 0) {
            swap(arr[low], arr[mid]);
            low++;
            mid++;
        } else if (arr[mid] == 1) {
            mid++;
        } else if (arr[mid] == 2) {
            swap(arr[mid], arr[high]);
            high--;
        }
    }
}

int main() {
    int arr[] = {2, 0, 1, 1, 0, 2, 1, 0};
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << "Before sorting: ";
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }

    dutchNationalFlag(arr, size);

    cout << "\nAfter sorting: ";
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}

In this program, the dutchNationalFlag function takes the array and its size as parameters. The three pointers, low, mid, and high, are initially set to the start, start, and end of the array, respectively.

The algorithm works as follows:

1.  If the element at mid is 0, swap it with the element at low, increment both low and mid.

2.  If the element at mid is 1, just increment mid to move forward.

3.  If the element at mid is 2, swap it with the element at high, decrement high to move backward (since we know the element at high is greater than 1). Do not increment mid in this case since the swapped element at mid still needs to be processed.

The loop continues until mid crosses or meets high, ensuring that the array is partitioned correctly.

When you run the program, it will output the sorted array as:

Before sorting: 2 0 1 1 0 2 1 0
After sorting: 0 0 0 1 1 1 2 2

The Dutch National Flag algorithm efficiently sorts the array in a single pass by maintaining three pointers, avoiding multiple iterations and achieving a time complexity of O(n), where n is the size of the array.

# 69

# Array Next Greater Element

The Next Greater Element problem involves finding the next greater element for each element in an array. We can solve this problem efficiently using a stack data structure. Here’s how you can implement it in C++:

#include <iostream>
#include <stack>
#include <vector>

using namespace std;

vector<int> findNextGreaterElement(const vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n, -1);  // Initialize the result vector with -1
    stack<int> st;

    for (int i = 0; i < n; i++) {
        while (!st.empty() && arr[i] > arr[st.top()]) {
            // arr[i] is the next greater element for elements at indices stored in the stack
            result[st.top()] = arr[i];
            st.pop();
        }
        st.push(i);  // Push the index onto the stack
    }

    return result;
}

int main() {
    vector<int> arr = {4, 2, 8, 6, 1, 5, 10};
    vector<int> nextGreater = findNextGreaterElement(arr);

    cout << "Element\tNext Greater Element" << endl;
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << "\t\t";
        if (nextGreater[i] != -1)
            cout << nextGreater[i] << endl;
        else
            cout << "Not found" << endl;
    }

    return 0;
}

Let’s go through the implementation:

1.  We define a function findNextGreaterElement that takes the input array arr and returns a vector result containing the next greater elements.

2.  We initialize the result vector with -1 to indicate that a greater element is not found yet for any element.

3.  We use a stack, st, to store the indices of elements for which we haven’t found the next greater element yet.

4.  We iterate through the array from left to right. For each element arr[i], we compare it with the elements at the indices stored in the stack.

5.  If arr[i] is greater than the element at the top of the stack, it means that arr[i] is the next greater element for the elements at the indices stored in the stack. We update the corresponding positions in the result vector and pop those indices from the stack.

6.  After comparing arr[i] with all the elements in the stack, we push the index i onto the stack as we haven’t found the next greater element for it yet.

7.  Finally, we return the result vector, which contains the next greater elements for each element in the input array.

In the main function, we demonstrate the usage of the findNextGreaterElement function. We initialize an example array and print the corresponding elements along with their next greater elements.

Running this program will produce the following output:

Element    Next Greater Element
4                8
2                8
8                10
6                10
1                5
5                10
10              Not found

Here, we can see that for each element in the array, the program correctly identifies the next greater element.

# 70

# Array Subarray with Given Sum

Here’s a C++ program that uses the prefix sum technique to find a subarray with a given sum in an array:

#include <iostream>
#include <unordered_map>
#include <vector>

std::vector<int> findSubarrayWithSum(const std::vector<int>& arr, int targetSum) {
    std::unordered_map<int, int> prefixSum; // Store prefix sums and their corresponding indices
    std::vector<int> result;

    int currentSum = 0;
    for (int i = 0; i < arr.size(); ++i) {
        currentSum += arr[i];

        // Check if a subarray with the target sum ends at the current index
        if (currentSum == targetSum) {
            result = std::vector<int>(arr.begin(), arr.begin() + i + 1);
            break;
        }

        // If a prefix sum (currentSum - targetSum) is found,
        // it means a subarray with the target sum exists between its index + 1 and the current index
        if (prefixSum.find(currentSum - targetSum) != prefixSum.end()) {
            int startIndex = prefixSum[currentSum - targetSum] + 1;
            result = std::vector<int>(arr.begin() + startIndex, arr.begin() + i + 1);
            break;
        }

        prefixSum[currentSum] = i;
    }

    return result;
}

int main() {
    std::vector<int> arr = {1, 4, 20, 3, 10, 5};
    int targetSum = 33;

    std::vector<int> subarray = findSubarrayWithSum(arr, targetSum);

    if (!subarray.empty()) {
        std::cout << "Subarray with sum " << targetSum << " found: ";
        for (int num : subarray) {
            std::cout << num << " ";
        }
        std::cout << std::endl;
    } else {
        std::cout << "Subarray with sum " << targetSum << " not found." << std::endl;
    }

    return 0;
}

Explanation:

1.  We start by initializing an unordered map prefixSum to store the prefix sums and their corresponding indices.

2.  We iterate through the array arr and calculate the cumulative sum currentSum by adding each element.

3.  We check if currentSum is equal to the targetSum. If it is, we store the subarray from the beginning of arr to the current index in the result vector and break out of the loop.

4.  If the current sum is not equal to the target sum, we check if a prefix sum currentSum - targetSum exists in the prefixSum map. If it does, it means a subarray with the target sum exists between the index stored in the map and the current index. We extract this subarray and store it in the result vector.

5.  Finally, if no subarray is found, the result vector remains empty.

6.  In the main function, we test the findSubarrayWithSum function with a sample array arr and the target sum targetSum.

7.  If a subarray with the target sum is found, we print its elements. Otherwise, we print a message indicating that no subarray was found.

The prefix sum technique allows us to solve this problem with a time complexity of O(n), where n is the size of the input array arr. By storing the prefix sums and their corresponding indices in the prefixSum map, we can quickly check if a subarray with the target sum exists by looking up the prefix sums while traversing the array only once.

# 71

# Array Product of Array Except Self

To solve the problem of calculating the product of every element in an array except itself, we can use prefix and suffix product arrays. The prefix product array stores the product of all elements to the left of each index, and the suffix product array stores the product of all elements to the right of each index.

Here’s a C++ program that demonstrates this approach:

#include <iostream>
#include <vector>

using namespace std;

vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> prefix(n, 1);  // Initialize prefix product array with 1
    vector<int> suffix(n, 1);  // Initialize suffix product array with 1

    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] * nums[i - 1];  // Calculate prefix product
    }

    for (int i = n - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1] * nums[i + 1];  // Calculate suffix product
    }

    vector<int> result(n);
    for (int i = 0; i < n; i++) {
        result[i] = prefix[i] * suffix[i];  // Calculate the product except self
    }

    return result;
}

int main() {
    vector<int> nums = {1, 2, 3, 4, 5};
    vector<int> result = productExceptSelf(nums);

    cout << "Product array except self: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}

In this program, we define two additional vectors: prefix and suffix, each of size n (where n is the length of the input array nums). We initialize both prefix and suffix arrays with 1 because the product of no elements is 1.

Next, we iterate over the nums array and calculate the prefix product for each index i. The prefix product at index i is obtained by multiplying the prefix product at index i-1 with the number at index i-1\. We start the loop from index 1 because the prefix product at index 0 is already 1.

Similarly, we iterate over the nums array in reverse order to calculate the suffix product for each index i. The suffix product at index i is obtained by multiplying the suffix product at index i+1 with the number at index i+1\. We start the loop from n-2 because the suffix product at index n-1 is already 1.

Finally, we calculate the product except self for each index i by multiplying the prefix product at index i with the suffix product at index i. We store these values in the result vector.

In the main function, we create an example array nums and call the productExceptSelf function. We then print the resulting array to verify the correctness of our solution.

When executed, the program will output:

Product array except self: 120 60 40 30 24

This indicates that the product of every element in the nums array, except itself, is [120, 60, 40, 30, 24].

# 72

# Array First Missing Positive

Here’s an example C++ program that finds the first missing positive integer in an unsorted array using swapping and indexing techniques:

#include <iostream>
#include <vector>

int firstMissingPositive(std::vector<int>& nums) {
    int n = nums.size();

    // Swap positive integers to their correct positions
    for (int i = 0; i < n; i++) {
        while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
            std::swap(nums[i], nums[nums[i] - 1]);
        }
    }

    // Find the first missing positive integer
    for (int i = 0; i < n; i++) {
        if (nums[i] != i + 1) {
            return i + 1;
        }
    }

    return n + 1;
}

int main() {
    std::vector<int> arr = {3, 4, -1, 1};
    int missing = firstMissingPositive(arr);
    std::cout << "The first missing positive integer is: " << missing << std::endl;

    return 0;
}

In this program, we use the swapping and indexing techniques to rearrange the positive integers in the array such that each positive integer i should be at index i-1\. We iterate through the array and swap the current number to its correct position by swapping it with the number at index nums[i] – 1\. This process continues until all positive integers are at their correct positions.

After the rearrangement, we iterate through the array again and check if each number is equal to its corresponding index plus one. If we find a mismatch, we return the index plus one as the first missing positive integer. If no mismatches are found, we return n + 1, where n is the size of the array, indicating that all positive integers from 1 to n are present in the array.

In the given example, the input array is {3, 4, -1, 1}. After the rearrangement, the array becomes {1, -1, 3, 4}. The first missing positive integer is 2, so the output of the program is:

The first missing positive integer is: 2

You can modify the main function to test the program with different arrays.

# 73

# Array Game of Life

Conway’s Game of Life is a cellular automaton devised by mathematician John Conway. It is played on a two-dimensional grid of cells, where each cell can be in one of two states: alive or dead. The grid evolves over time based on a set of rules.

Here’s an example implementation of Conway’s Game of Life in C++:

#include <iostream>
#include <vector>

// Function to print the current state of the grid
void printGrid(const std::vector<std::vector<bool>>& grid) {
    for (const auto& row : grid) {
        for (bool cell : row) {
            std::cout << (cell ? "O " : ". ");
        }
        std::cout << std::endl;
    }
}

// Function to update the grid based on the rules of the game
void updateGrid(std::vector<std::vector<bool>>& grid) {
    int numRows = grid.size();
    int numCols = grid[0].size();

    std::vector<std::vector<bool>> newGrid(numRows, std::vector<bool>(numCols));

    // Iterate over each cell in the grid
    for (int i = 0; i < numRows; ++i) {
        for (int j = 0; j < numCols; ++j) {
            // Count the number of live neighbors
            int liveNeighbors = 0;

            // Check the eight neighboring cells
            for (int x = -1; x <= 1; ++x) {
                for (int y = -1; y <= 1; ++y) {
                    if (x == 0 && y == 0) {
                        continue;  // Skip the current cell
                    }

                    int neighborRow = i + x;
                    int neighborCol = j + y;

                    // Check if the neighbor is within the grid bounds
                    if (neighborRow >= 0 && neighborRow < numRows &&
                        neighborCol >= 0 && neighborCol < numCols) {
                        liveNeighbors += grid[neighborRow][neighborCol] ? 1 : 0;
                    }
                }
            }

            // Apply the rules of the game
            if (grid[i][j]) {
                // Cell is alive
                if (liveNeighbors < 2 || liveNeighbors > 3) {
                    // Underpopulation or overpopulation, cell dies
                    newGrid[i][j] = false;
                } else {
                    // Cell survives to the next generation
                    newGrid[i][j] = true;
                }
            } else {
                // Cell is dead
                if (liveNeighbors == 3) {
                    // Cell is born
                    newGrid[i][j] = true;
                } else {
                    newGrid[i][j] = false;
                }
            }
        }
    }

    // Update the original grid with the new grid
    grid = newGrid;
}

int main() {
    // Define the size of the grid
    int numRows = 10;
    int numCols = 10;

    // Create the initial grid with random alive or dead cells
    std::vector<std::vector<bool>> grid(numRows, std::vector<bool>(numCols));
    for (auto& row : grid) {
        for (bool& cell : row) {
            cell = rand() % 2 == 0;
        }
    }

    // Perform 10 iterations of the game
    for (int i = 0; i < 10; ++i) {
        std::cout << "Generation " << i << std::endl;
        printGrid(grid);
        updateGrid(grid);
        std::cout << std::endl;
    }

    return 0;
}

In this implementation, the grid is represented as a 2D vector of booleans, where true represents a live cell and false represents a dead cell.

The printGrid function simply prints the current state of the grid, displaying live cells as “O” and dead cells as “.”.

The updateGrid function applies the rules of the game to update the grid. It iterates over each cell in the grid, counts its live neighbors, and applies the rules to determine whether the cell should live, die, or be born in the next generation. The new state of the grid is stored in a separate newGrid vector, and then copied back to the original grid.

The main function initializes the grid with random live or dead cells, prints the initial state, performs 10 iterations of the game by calling updateGrid, and prints each generation’s state.

You can adjust the size of the grid and the number of iterations in the main function to suit your needs.

# 74

# Array Jump Game

Here’s an example of how you can write a C++ program to determine if it is possible to reach the last index of an array by jumping through its elements:

#include <iostream>
#include <vector>

bool canJump(const std::vector<int>& nums) {
    int lastPosition = nums.size() - 1;

    for (int i = nums.size() - 2; i >= 0; i--) {
        if (i + nums[i] >= lastPosition) {
            lastPosition = i;
        }
    }

    return lastPosition == 0;
}

int main() {
    // Example usage
    std::vector<int> nums = {2, 3, 1, 1, 4};
    bool result = canJump(nums);

    if (result) {
        std::cout << "It is possible to reach the last index." << std::endl;
    } else {
        std::cout << "It is not possible to reach the last index." << std::endl;
    }

    return 0;
}

In this program, we use a greedy approach to solve the problem. The basic idea is to iterate through the array from right to left, starting from the second-to-last element. We maintain a variable lastPosition, which represents the rightmost index from which we can reach the last index.

At each iteration, we check if the current index i plus the value at that index (nums[i]) is greater than or equal to lastPosition. If it is, it means we can jump from index i to a position that is at least as far as the current lastPosition, so we update lastPosition to i. By the end of the loop, lastPosition should be 0 if it is possible to reach the last index, indicating that we can start from the beginning of the array and reach the last index.

This approach is considered greedy because at each step, we make the locally optimal choice by jumping to the index that allows us to reach the farthest position. The algorithm does not look ahead or consider future positions, but the greedy choice turns out to be sufficient to determine if it is possible to reach the last index.

Dynamic programming, on the other hand, is not required for this problem since the solution can be achieved using a simpler greedy approach, as shown above. Dynamic programming techniques are typically useful when the problem exhibits overlapping subproblems and optimal substructure, which are not the case in this particular problem.

# 75

# Array Max Points on a Line

To find the maximum number of points that lie on the same line in a given array of points, we can use either hashing or slope calculation techniques. Let’s go through both approaches:

Hashing Technique:

*   Create a hash map or a hash table to store the frequency of each slope.

*   Iterate through each point in the array and calculate the slope with respect to every other point.

*   Increment the count of the corresponding slope in the hash map.

*   Keep track of the maximum frequency of any slope encountered.

*   Return the maximum frequency as the result.

Here’s the C++ code that implements the hashing technique:

#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

struct Point {
    int x;
    int y;
    Point(int a, int b) : x(a), y(b) {}
};

int maxPointsOnLine(vector<Point>& points) {
    int n = points.size();
    if (n <= 2)
        return n; // If there are 0, 1, or 2 points, they will always lie on the same line.

    int maxPoints = 0;
    for (int i = 0; i < n; i++) {
        unordered_map<double, int> slopeFreq; // Slope -> Frequency

        int samePoints = 1; // Count of points overlapping with the current point
        int verticalPoints = 0; // Count of vertical points (same x-coordinate)

        for (int j = i + 1; j < n; j++) {
            if (points[i].x == points[j].x) {
                if (points[i].y == points[j].y)
                    samePoints++;
                else
                    verticalPoints++;
            } else {
                double slope = (double)(points[j].y - points[i].y) / (points[j].x - points[i].x);
                slopeFreq[slope]++;
            }
        }

        int localMax = verticalPoints; // Maximum points on line passing through the current point

        for (auto it = slopeFreq.begin(); it != slopeFreq.end(); it++) {
            if (it->second > localMax)
                localMax = it->second;
        }

        localMax += samePoints; // Add the count of overlapping points
        if (localMax > maxPoints)
            maxPoints = localMax;
    }

    return maxPoints;
}

int main() {
    vector<Point> points;
    points.push_back(Point(1, 1));
    points.push_back(Point(2, 2));
    points.push_back(Point(3, 3));
    points.push_back(Point(1, 2));
    points.push_back(Point(2, 1));
    points.push_back(Point(3, 4));

    int result = maxPointsOnLine(points);
    cout << "Maximum points on the same line: " << result << endl;

    return 0;
}

The output will be:

Maximum points on the same line: 4

Slope Calculation Technique:

*   Iterate through each pair of points and calculate the slope between them.

*   Use a nested loop to compare each point with every other point to check if they lie on the same line.

*   Keep track of the maximum count of points that lie on the same line.

*   Return the maximum count as the result.

Here’s the C++ code that implements the slope calculation technique:

#include <iostream>
#include <vector>

using namespace std;

struct Point {
    int x;
    int y;
    Point(int a, int b) : x(a), y(b) {}
};

int maxPointsOnLine(vector<Point>& points) {
    int n = points.size();
    if (n <= 2)
        return n; // If there are 0, 1, or 2 points, they will always lie on the same line.

    int maxPoints = 0;
    for (int i = 0; i < n; i++) {
        int samePoints = 1; // Count of points overlapping with the current point

        for (int j = i + 1; j < n; j++) {
            int sameSlopePoints = 0; // Count of points with the same slope

            for (int k = 0; k < n; k++) {
                if (k != i && k != j) {
                    // Check if points k, i, and j are collinear (lie on the same line)
                    if ((points[j].y - points[i].y) * (points[k].x - points[i].x) ==
                        (points[k].y - points[i].y) * (points[j].x - points[i].x)) {
                        sameSlopePoints++;
                    }
                }
            }

            maxPoints = max(maxPoints, sameSlopePoints);
        }

        maxPoints = max(maxPoints, samePoints);
    }

    return maxPoints + 1; // Add 1 for the current point itself
}

int main() {
    vector<Point> points;
    points.push_back(Point(1, 1));
    points.push_back(Point(2, 2));
    points.push_back(Point(3, 3));
    points.push_back(Point(1, 2));
    points.push_back(Point(2, 1));
    points.push_back(Point(3, 4));

    int result = maxPointsOnLine(points);
    cout << "Maximum points on the same line: " << result << endl;

    return 0;
}

The output will be the same as in the previous approach:

Maximum points on the same line: 4

Both approaches will yield the same result, but the hashing technique has a better time complexity of O(n^2) compared to the slope calculation technique, which has a time complexity of O(n^3). Therefore, the hashing technique is more efficient when dealing with larger arrays of points.

# 76

# Array Merge Intervals

Here’s an example program in C++ that merges overlapping intervals in an array:

#include <iostream>
#include <vector>
#include <algorithm>

struct Interval {
    int start;
    int end;

    Interval(int s, int e) : start(s), end(e) {}
};

bool compareIntervals(const Interval& a, const Interval& b) {
    return a.start < b.start;
}

std::vector<Interval> mergeIntervals(const std::vector<Interval>& intervals) {
    if (intervals.empty()) {
        return {};
    }

    std::vector<Interval> mergedIntervals;
    std::vector<Interval> sortedIntervals = intervals;

    // Sort the intervals based on their start points
    std::sort(sortedIntervals.begin(), sortedIntervals.end(), compareIntervals);

    mergedIntervals.push_back(sortedIntervals[0]);

    for (int i = 1; i < sortedIntervals.size(); i++) {
        if (sortedIntervals[i].start <= mergedIntervals.back().end) {
            // The current interval overlaps with the previous one, so merge them
            mergedIntervals.back().end = std::max(mergedIntervals.back().end, sortedIntervals[i].end);
        } else {
            // The current interval doesn't overlap with the previous one, so add it to the merged intervals
            mergedIntervals.push_back(sortedIntervals[i]);
        }
    }

    return mergedIntervals;
}

void printIntervals(const std::vector<Interval>& intervals) {
    for (const auto& interval : intervals) {
        std::cout << "[" << interval.start << ", " << interval.end << "] ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<Interval> intervals = {Interval(1, 3), Interval(2, 6), Interval(8, 10), Interval(15, 18)};
    std::cout << "Original intervals: ";
    printIntervals(intervals);

    std::vector<Interval> merged = mergeIntervals(intervals);
    std::cout << "Merged intervals: ";
    printIntervals(merged);

    return 0;
}

In this program, we represent each interval using the Interval struct, which stores the start and end points. The function compareIntervals is used as a custom comparison function for sorting the intervals.

The mergeIntervals function takes a vector of intervals as input and returns a new vector with the merged intervals. It first checks if the input vector is empty and returns an empty vector if it is.

Then, it creates a copy of the input vector called sortedIntervals and sorts it using std::sort with the compareIntervals comparison function. This step ensures that the intervals are sorted based on their start points.

Next, the function iterates through the sorted intervals. If the current interval overlaps with the last merged interval (i.e., its start point is less than or equal to the previous interval’s end point), it updates the end point of the last merged interval to be the maximum of its current end point and the end point of the current interval.

If the current interval doesn’t overlap with the last merged interval, it adds the current interval to the mergedIntervals vector.

Finally, the function returns the mergedIntervals vector.

The printIntervals function is a helper function that prints the intervals in the format [start, end].

In the main function, we create a vector of intervals, print the original intervals, call the mergeIntervals function to obtain the merged intervals, and then print the merged intervals.

When you run this program, the output will be:

Original intervals: [1, 3] [2, 6] [8, 10] [15, 18]
Merged intervals: [1, 6] [8, 10] [15, 18]

As you can see, the overlapping intervals [1, 3] and [2, 6] are merged into [1, 6] to produce the final result. The non-overlapping intervals remain unchanged.

# 77

# Array Plus One

Here’s a program in C++ that adds one to the value represented by an array of digits and handles carry operations and array resizing:

#include <iostream>
#include <vector>

std::vector<int> addOneToArray(std::vector<int>& digits) {
    int carry = 1;  // Start with a carry of 1
    int n = digits.size();

    // Traverse the array in reverse order
    for (int i = n - 1; i >= 0; --i) {
        int sum = digits[i] + carry;
        digits[i] = sum % 10;  // Update the current digit

        carry = sum / 10;  // Calculate the carry

        // If there is no carry, we can stop the traversal
        if (carry == 0) {
            break;
        }
    }

    // If there is still a carry after the traversal, we need to resize the array
    if (carry > 0) {
        digits.insert(digits.begin(), carry);
    }

    return digits;
}

int main() {
    std::vector<int> digits = {9, 9, 9};  // Example array representing 999

    std::cout << "Original Array: ";
    for (int digit : digits) {
        std::cout << digit << " ";
    }
    std::cout << std::endl;

    std::vector<int> result = addOneToArray(digits);

    std::cout << "Modified Array: ";
    for (int digit : result) {
        std::cout << digit << " ";
    }
    std::cout << std::endl;

    return 0;
}

Explanation:

1.  The addOneToArray function takes a reference to the array of digits as input and returns a modified array.

2.  It starts with a carry value of 1 because we want to add one to the given value.

3.  The function traverses the array in reverse order, starting from the last digit.

4.  For each digit, it adds the carry to the current digit and stores the result in the same position.

5.  The carry is updated by dividing the sum by 10 (to get the carry value).

6.  If the carry becomes zero during the traversal, it means there is no further carry operation required, and the function breaks out of the loop.

7.  After the traversal, if there is still a carry remaining (carry > 0), it means the array needs to be resized to accommodate the additional digit. In such a case, we insert the carry value at the beginning of the array using the insert function.

8.  Finally, the modified array is returned.

9.  In the main function, we create an example array digits representing the value 999.

10.  The original array is printed.

11.  The addOneToArray function is called, and the modified array is stored in the result.

12.  The modified array is printed.

The output of the above program will be:

Original Array: 9 9 9
Modified Array: 1 0 0 0

The program correctly adds one to the given value, handles carry operations, and resizes the array if necessary.

# 78

# Array Triplet Sum Closest

Here’s a C++ program that finds the triplet with the closest sum to a given target in an array using sorting and the two-pointer technique:

#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

int findClosestTripletSum(vector<int>& nums, int target) {
    int n = nums.size();
    if (n < 3)
        return 0;

    sort(nums.begin(), nums.end()); // Sort the array in ascending order
    int closestSum = INT_MAX;

    for (int i = 0; i < n - 2; i++) {
        int left = i + 1; // Pointer to the element next to nums[i]
        int right = n - 1; // Pointer to the last element

        while (left < right) {
            int currentSum = nums[i] + nums[left] + nums[right];
            if (currentSum == target)
                return target;

            if (abs(currentSum - target) < abs(closestSum - target))
                closestSum = currentSum;

            if (currentSum < target)
                left++;
            else
                right--;
        }
    }

    return closestSum;
}

int main() {
    vector<int> nums = { -1, 2, 1, -4 };
    int target = 1;

    int closestSum = findClosestTripletSum(nums, target);
    cout << "Closest sum: " << closestSum << endl;

    return 0;
}

Explanation:

1.  First, we sort the given array nums in ascending order. Sorting the array helps us in leveraging the two-pointer technique efficiently.

2.  We initialize closestSum with a large value (INT_MAX) to keep track of the closest sum encountered so far.

3.  We iterate through the array nums using a loop variable i from 0 to n - 2 (where n is the size of nums). This is because we need at least three elements to form a triplet.

4.  Inside the loop, we initialize two pointers, left and right, pointing to the elements next to nums[i] and the last element, respectively.

5.  While left is less than right, we calculate the sum of the triplet (currentSum) as nums[i] + nums[left] + nums[right].

6.  If the currentSum is equal to the target, we directly return the target as the closest sum.

7.  If the absolute difference between currentSum and target is smaller than the absolute difference between closestSum and target, we update closestSum with currentSum. This keeps track of the closest sum encountered so far.

8.  Based on the comparison of currentSum and target, we move the left or right pointer. If currentSum is smaller than the target, we increment left to consider a larger element. Otherwise, we decrement right to consider a smaller element.

9.  After the loop ends, we return closestSum, which represents the closest sum to the target among all the triplets.

In the example given in the main function, the array nums contains [-1, 2, 1, -4], and the target is 1\. The closest sum to the target among all the triplets is 2 (-1 + 2 + 1), so the program will output “Closest sum: 2” when executed.

# 79

# Array Subsets

To generate all possible subsets of an array in C++, you can use either backtracking or bit manipulation. Let’s explore both approaches:

Backtracking Approach: Backtracking involves systematically exploring all possible solutions by incrementally building a solution and undoing the choices when necessary. Here’s how you can generate subsets of an array using backtracking:

#include <iostream>
#include <vector>

using namespace std;

void generateSubsets(vector<int>& nums, vector<int>& subset, int index) {
    // Print the current subset
    for (int num : subset) {
        cout << num << " ";
    }
    cout << endl;

    // Generate subsets by including each element after the current index
    for (int i = index; i < nums.size(); i++) {
        subset.push_back(nums[i]); // Include the current element
        generateSubsets(nums, subset, i + 1); // Recur for the next index
        subset.pop_back(); // Exclude the current element
    }
}

void generateAllSubsets(vector<int>& nums) {
    vector<int> subset;
    generateSubsets(nums, subset, 0);
}

int main() {
    vector<int> nums = {1, 2, 3};
    generateAllSubsets(nums);
    return 0;
}

This program generates all possible subsets of the array [1, 2, 3]. The generateSubsets function uses backtracking to include each element after the current index and recursively generate subsets. The generateAllSubsets function initializes an empty subset and starts the backtracking process from index 0.

Bit Manipulation Approach: Bit manipulation is an efficient way to generate subsets using bitwise operations. Each element in the array can be represented by a bit, where 1 indicates inclusion in the subset, and 0 indicates exclusion. Here’s an example:

#include <iostream>
#include <vector>

using namespace std;

void generateAllSubsets(vector<int>& nums) {
    int n = nums.size();
    int totalSubsets = 1 << n;

    for (int i = 0; i < totalSubsets; i++) {
        vector<int> subset;
        for (int j = 0; j < n; j++) {
            if (i & (1 << j)) {
                subset.push_back(nums[j]);
            }
        }

        // Print the current subset
        for (int num : subset) {
            cout << num << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<int> nums = {1, 2, 3};
    generateAllSubsets(nums);
    return 0;
}

In this program, the generateAllSubsets function iterates from 0 to 2^n (where n is the number of elements in the array) and uses bitwise operations to determine the inclusion of each element in the subset. The subset vector stores the elements included in the current subset, which are then printed.

Both approaches yield the same output, which is the set of all possible subsets of the given array [1, 2, 3]. Choose the approach that suits your requirements and constraints.

# 80

# Array Unique Paths

Here’s a C++ program that uses dynamic programming to find the number of unique paths from the top-left to the bottom-right of a given grid:

#include <iostream>
#include <vector>

int uniquePaths(int m, int n) {
    // Create a 2D grid with size m x n
    std::vector<std::vector<int>> dp(m, std::vector<int>(n, 0));

    // Initialize the first row and first column with 1
    for (int i = 0; i < m; ++i)
        dp[i][0] = 1;
    for (int j = 0; j < n; ++j)
        dp[0][j] = 1;

    // Calculate the number of unique paths for each cell
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            // The number of unique paths to reach cell (i, j) is
            // the sum of paths from the cell above (i-1, j) and
            // the cell to the left (i, j-1)
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }

    // Return the number of unique paths to reach the bottom-right cell
    return dp[m-1][n-1];
}

int main() {
    int m, n;
    std::cout << "Enter the number of rows: ";
    std::cin >> m;
    std::cout << "Enter the number of columns: ";
    std::cin >> n;

    int paths = uniquePaths(m, n);
    std::cout << "Number of unique paths: " << paths << std::endl;

    return 0;
}

Explanation:

In this program, we use a dynamic programming approach to solve the problem. We create a 2D grid (dp) of size m x n, where each cell dp[i][j] represents the number of unique paths to reach that cell from the top-left corner.

We initialize the first row and first column of the grid with 1 because there is only one way to reach any cell in the first row or first column (by moving either right or down).

Then, we iterate over the remaining cells of the grid (starting from the second row and second column) and calculate the number of unique paths to reach each cell. The number of unique paths to reach cell (i, j) is the sum of paths from the cell above (i-1, j) and the cell to the left (i, j-1).

Finally, we return the number of unique paths to reach the bottom-right cell, which is dp[m-1][n-1].

By using this dynamic programming approach, we avoid redundant calculations and efficiently find the number of unique paths in the given grid.

# 81

# Array Submatrix Sum

To find the maximum sum of a submatrix within a given matrix, you can use the concept of prefix sums along with nested loops. Here’s a step-by-step explanation of how you can solve this problem using C++:

1.  Define the dimensions of the given matrix, let’s say it has ‘n’ rows and ‘m’ columns.

2.  Create a prefix sum matrix ‘prefixSum’ of the same dimensions as the given matrix. Initialize all the elements of ‘prefixSum’ to 0.

3.  Iterate over each row of the given matrix using a variable ‘i’ from 0 to n-1.

4.  Within the above loop, iterate over each column of the given matrix using a variable ‘j’ from 0 to m-1.

5.  Compute the prefix sum of the current element by adding it to the prefix sum of the element directly above it and the element directly to its left, and subtracting the prefix sum of the element diagonally above and to the left. Store this sum in the corresponding position of ‘prefixSum’.prefixSum[i][j] = prefixSum[i-1][j] + prefixSum[i][j-1] – prefixSum[i-1][j-1] + matrix[i][j]Note: For the first row and column, you won’t have any element above or to the left. So, handle these cases separately.

6.  Initialize a variable ‘maxSum’ to a very small value, e.g., INT_MIN, to keep track of the maximum sum encountered so far.

7.  Iterate over each submatrix starting from the top-left corner using two nested loops. The outer loop will iterate over the starting row of the submatrix, and the inner loop will iterate over the starting column of the submatrix.For each submatrix, calculate its sum by subtracting the appropriate prefix sums. Compare this sum with ‘maxSum’ and update ‘maxSum’ if the current sum is greater.currentSum = prefixSum[i + k][j + l] – prefixSum[i + k][j – 1] – prefixSum[i – 1][j + l] + prefixSum[i – 1][j – 1] maxSum = max(maxSum, currentSum)Here, ‘k’ and ‘l’ represent the size of the submatrix, which can vary from 1 to min(n, m).

8.  After the nested loops complete, ‘maxSum’ will contain the maximum sum of a submatrix within the given matrix.

Here’s an example C++ code snippet that implements the above algorithm:

#include <iostream>
#include <climits>
using namespace std;

int main() {
    // Define the dimensions of the matrix
    int n, m;
    cin >> n >> m;

    // Create the matrix
    int matrix[n][m];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> matrix[i][j];
        }
    }

    // Create the prefix sum matrix
    int prefixSum[n][m] = {0};

    // Compute prefix sums
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (i == 0 && j == 0) {
                prefixSum[i][j] = matrix[i][j];
            } else if (i == 0) {
                prefixSum[i][j] = prefixSum[i][j - 1] + matrix[i][j];
            } else if (j == 0) {
                prefixSum[i][j] = prefixSum[i - 1][j] + matrix[i][j];
            } else {
                prefixSum[i][j] = prefixSum[i - 1][j] + prefixSum[i][j - 1] - prefixSum[i - 1][j - 1] + matrix[i][j];
            }
        }
    }

    int maxSum = INT_MIN;

    // Calculate maximum sum of submatrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            for (int k = i; k < n; k++) {
                for (int l = j; l < m; l++) {
                    int currentSum;
                    if (i == 0 && j == 0) {
                        currentSum = prefixSum[k][l];
                    } else if (i == 0) {
                        currentSum = prefixSum[k][l] - prefixSum[k][j - 1];
                    } else if (j == 0) {
                        currentSum = prefixSum[k][l] - prefixSum[i - 1][l];
                    } else {
                        currentSum = prefixSum[k][l] - prefixSum[k][j - 1] - prefixSum[i - 1][l] + prefixSum[i - 1][j - 1];
                    }
                    maxSum = max(maxSum, currentSum);
                }
            }
        }
    }

    cout << "Maximum submatrix sum: " << maxSum << endl;

    return 0;
}

Make sure to compile and run this code with a C++ compiler to see the results.

# 82

# Array Spiral Matrix Generation

Here’s a C++ program that generates a matrix in a spiral pattern:

#include <iostream>
#include <vector>

using namespace std;

vector<vector<int>> generateSpiralMatrix(int n) {
    vector<vector<int>> matrix(n, vector<int>(n, 0)); // Initialize matrix with zeroes

    int value = 1; // Starting value for the spiral
    int top = 0, bottom = n - 1, left = 0, right = n - 1;

    while (top <= bottom && left <= right) {
        // Traverse from left to right
        for (int i = left; i <= right; i++) {
            matrix[top][i] = value;
            value++;
        }
        top++;

        // Traverse from top to bottom
        for (int i = top; i <= bottom; i++) {
            matrix[i][right] = value;
            value++;
        }
        right--;

        if (top <= bottom) {
            // Traverse from right to left
            for (int i = right; i >= left; i--) {
                matrix[bottom][i] = value;
                value++;
            }
            bottom--;
        }

        if (left <= right) {
            // Traverse from bottom to top
            for (int i = bottom; i >= top; i--) {
                matrix[i][left] = value;
                value++;
            }
            left++;
        }
    }

    return matrix;
}

void printMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) {
        for (int element : row) {
            cout << element << "\t";
        }
        cout << endl;
    }
}

int main() {
    int n;
    cout << "Enter the size of the matrix: ";
    cin >> n;

    vector<vector<int>> spiralMatrix = generateSpiralMatrix(n);

    cout << "Spiral Matrix:" << endl;
    printMatrix(spiralMatrix);

    return 0;
}

In this program, we define a function generateSpiralMatrix that takes an integer n as input and returns a 2D vector representing the spiral matrix. We also define a helper function printMatrix to display the matrix.

The algorithm works by iterating through the matrix in a spiral pattern, updating the row and column boundaries as we go along. The variable value keeps track of the current value to be assigned to each element in the matrix.

We start by initializing the boundaries top, bottom, left, and right to represent the outermost layer of the spiral. Then, in each iteration of the while loop, we traverse the top row, right column, bottom row (if applicable), and left column (if applicable), assigning values to the corresponding elements in the matrix.

After each traversal, we adjust the boundaries accordingly to move to the next layer of the spiral. The while loop continues until the top boundary exceeds the bottom boundary or the left boundary exceeds the right boundary.

Finally, we print the generated spiral matrix by calling the printMatrix function.

Note: The program assumes that the input n is a positive integer. You can add input validation code to handle invalid inputs if necessary.

# 83

# Array Target Sum

To find all pairs of elements in an array that add up to a given target sum, you can use either the hashing technique or the two-pointer approach. Let me explain both methods to you:

Hashing Approach:

*   Create an empty hash table (unordered_set or unordered_map) to store elements as you traverse the array.

*   Iterate through the array:

*   For each element num in the array:

*   Calculate the complement as targetSum - num.

*   Check if the complement exists in the hash table.

*   If it does, you have found a pair (num, complement) that adds up to the target sum.

*   If it doesn’t, insert num into the hash table for future lookups.

*   Repeat the above steps until you traverse the entire array.

*   The pairs found during the process will be the pairs that add up to the target sum.

Here’s a C++ implementation of the hashing approach:

#include <iostream>
#include <unordered_set>
#include <vector>

void findPairsWithTargetSum(const std::vector<int>& arr, int targetSum) {
    std::unordered_set<int> hashSet;
    std::vector<std::pair<int, int>> pairs;

    for (int num : arr) {
        int complement = targetSum - num;
        if (hashSet.find(complement) != hashSet.end()) {
            pairs.emplace_back(num, complement);
        }
        hashSet.insert(num);
    }

    // Print the pairs
    for (const auto& pair : pairs) {
        std::cout << pair.first << ", " << pair.second << std::endl;
    }
}

int main() {
    std::vector<int> arr = {1, 2, 3, 4, 5, 6};
    int targetSum = 7;
    findPairsWithTargetSum(arr, targetSum);

    return 0;
}

Two-Pointer Approach:

*   Sort the array in non-decreasing order.

*   Initialize two pointers, left and right, pointing to the start and end of the array, respectively.

*   While left is less than right:

*   Calculate the sum of the elements at left and right.

*   If the sum is equal to the target sum, you have found a pair.

*   If the sum is less than the target sum, move the left pointer to the right (increasing the sum).

*   If the sum is greater than the target sum, move the right pointer to the left (decreasing the sum).

*   Repeat the above steps until the pointers cross each other.

*   The pairs found during the process will be the pairs that add up to the target sum.

Here’s a C++ implementation of the two-pointer approach:

#include <iostream>
#include <algorithm>
#include <vector>

void findPairsWithTargetSum(const std::vector<int>& arr, int targetSum) {
    std::vector<std::pair<int, int>> pairs;
    int left = 0;
    int right = arr.size() - 1;

    // Sort the array
    std::vector<int> sortedArr = arr;
    std::sort(sortedArr.begin(), sortedArr.end());

    while (left < right) {
        int sum = sortedArr[left] + sortedArr[right];
        if (sum == targetSum) {
            pairs.emplace_back(sortedArr[left], sortedArr[right]);
            left++;
            right--;
        } else if (sum < targetSum) {
            left++;
        } else {
            right--;
        }
    }

    // Print the pairs
    for (const auto& pair : pairs) {
        std::cout << pair.first << ", " << pair.second << std::endl;
    }
}

int main() {
    std::vector<int> arr = {6, 4, 5, 3, 2, 1};
    int targetSum = 7;
    findPairsWithTargetSum(arr, targetSum);

    return 0;
}

Both approaches have a time complexity of O(n) since they traverse the array only once. However, the hashing approach may have some additional space complexity due to the hash table used to store elements.

Feel free to choose the approach that suits your needs and integrate it into your program accordingly.

# 84

# Array Maximum Subarray Product

Here’s a C++ program that finds the maximum product of a subarray in an array using dynamic programming:

#include <iostream>
#include <vector>

using namespace std;

int maxProductSubarray(vector<int>& nums) {
    int n = nums.size();

    // Initialize the variables to track the maximum and minimum product
    int maxProduct = nums[0];
    int minProduct = nums[0];

    // Variable to store the maximum product subarray
    int maxSubarrayProduct = nums[0];

    for (int i = 1; i < n; i++) {
        // If the current number is negative, swap the max and min products
        if (nums[i] < 0)
            swap(maxProduct, minProduct);

        // Update the max and min products for the current number
        maxProduct = max(nums[i], maxProduct * nums[i]);
        minProduct = min(nums[i], minProduct * nums[i]);

        // Update the maximum product of a subarray
        maxSubarrayProduct = max(maxSubarrayProduct, maxProduct);
    }

    return maxSubarrayProduct;
}

int main() {
    vector<int> nums = {2, 3, -2, 4};

    int maxProduct = maxProductSubarray(nums);

    cout << "Maximum product of a subarray: " << maxProduct << endl;

    return 0;
}

Explanation: The dynamic programming approach to solve this problem involves using two variables, maxProduct and minProduct, to keep track of the maximum and minimum product of subarrays ending at the current index. We also maintain a separate variable, maxSubarrayProduct, to store the maximum product found so far.

We iterate through the array starting from the second element (index 1) and update the maxProduct and minProduct based on the current element. If the current element is negative, we swap maxProduct and minProduct because multiplying a negative number with the minimum product could potentially yield the maximum product.

For each element, we calculate the maximum and minimum product by comparing the current element with the product of the previous maximum/minimum product and the current element. We take the maximum of these values and update maxProduct accordingly.

At each iteration, we also update maxSubarrayProduct with the maximum value between maxSubarrayProduct and maxProduct, ensuring that it always holds the maximum product of a subarray encountered so far.

Finally, we return maxSubarrayProduct, which represents the maximum product of a subarray in the given array.

In the provided example, the output would be:

Maximum product of a subarray: 6

which corresponds to the subarray [2, 3].

# 85

# Array Kth Largest Element

Here’s an example program in C++ that finds the Kth largest element in an array using a priority queue:

#include <iostream>
#include <queue>
using namespace std;

int findKthLargest(int arr[], int size, int k) {
    // Create a max heap using priority_queue
    priority_queue<int> pq(arr, arr + size);

    // Extract the k-1 largest elements
    for (int i = 0; i < k - 1; i++) {
        pq.pop();
    }

    // The top of the priority queue will be the kth largest element
    return pq.top();
}

int main() {
    int arr[] = {3, 1, 7, 5, 9, 2};
    int size = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    int kthLargest = findKthLargest(arr, size, k);

    cout << "The " << k << "th largest element is: " << kthLargest << endl;

    return 0;
}

Explanation:

1.  The findKthLargest function takes three parameters: the array arr, its size size, and the value of k indicating the kth largest element to find.

2.  Inside the function, a priority_queue is created using the elements of the array. By default, priority_queue creates a max heap, so the largest element will always be at the top.

3.  We extract the k-1 largest elements from the priority_queue by calling pop() k-1 times.

4.  The top of the priority_queue after extracting k-1 elements will be the kth largest element, so we return it.

5.  In the main function, an example array is defined, and the findKthLargest function is called with the array, its size, and the desired value of k.

6.  The kth largest element is then printed to the console.

Now, let’s explain how you can solve the problem using the quickselect algorithm:

#include <iostream>
using namespace std;

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j <= high - 1; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }

    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

int quickSelect(int arr[], int low, int high, int k) {
    if (low < high) {
        int pivotIndex = partition(arr, low, high);

        // If the pivot is the kth largest element, return it
        if (pivotIndex == k - 1)
            return arr[pivotIndex];

        // If the pivot is greater than the kth largest element, search in the left partition
        else if (pivotIndex > k - 1)
            return quickSelect(arr, low, pivotIndex - 1, k);

        // If the pivot is smaller than the kth largest element, search in the right partition
        else
            return quickSelect(arr, pivotIndex + 1, high, k);
    }

    // If the array has only one element, return it
    return arr[low];
}

int findKthLargest(int arr[], int size, int k) {
    return quickSelect(arr, 0, size - 1, k);
}

int main() {
    int arr[] = {3, 1, 7, 5, 9, 2};
    int size = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    int kthLargest = findKthLargest(arr, size, k);

    cout << "The " << k << "th largest element is: " << kthLargest << endl;

    return 0;
}

Explanation:

1.  The partition function is a helper function used in the quickselect algorithm to rearrange elements in the array such that all elements smaller than the pivot are placed to its left, and all elements larger are placed to its right. It returns the index of the pivot element after partitioning.

2.  The quickSelect function recursively partitions the array and selects a pivot until the pivot element is the kth largest element. It uses the partition function to rearrange the array.

3.  The findKthLargest function serves as a wrapper function for quickSelect and is called from the main function.

4.  In the main function, an example array is defined, and the findKthLargest function is called with the array, its size, and the desired value of k.

5.  The kth largest element is then printed to the console.

Both methods, priority queues and quickselect, can be used to find the kth largest element in an array efficiently. The choice between them depends on the specific requirements and constraints of your problem. Priority queues offer a simpler implementation and a time complexity of O(n log k), where n is the size of the array. Quickselect, on the other hand, has an average time complexity of O(n) and can be faster in practice, but it has a worst-case time complexity of O(n^2) if the pivot selection is poor.

# 86

# Array Subarray with Equal 0s and 1s

To find the longest subarray with an equal number of 0s and 1s in a binary array, we can use the prefix sums technique along with hashing. Here’s a step-by-step explanation of the approach:

1.  First, let’s understand the concept of prefix sums. For each index i in the given binary array, the prefix sum sum at that index represents the difference between the number of 1s and 0s encountered from the start of the array up to index i. We can compute the prefix sums array prefixSum using the following formula: prefixSum[i] = prefixSum[i - 1] + (arr[i] == 0 ? -1 : 1)

2.  Create a hash table (unordered map) named sumMap to store the first occurrence of each unique sum encountered during the iteration of the prefix sums array.

3.  Initialize two variables, maxLength and endIndex, to keep track of the maximum length of the subarray and the ending index of that subarray, respectively. Set maxLength to 0 and endIndex to -1.

4.  Traverse the prefixSum array from left to right:

*   If prefixSum[i] is 0, it means the subarray from index 0 to i has an equal number of 0s and 1s. Update maxLength to i + 1 and endIndex to i.

*   If prefixSum[i] is already present in sumMap, it means there is a subarray with the same sum encountered before. Calculate the length of the current subarray as i - sumMap[prefixSum[i]] and check if it is greater than maxLength. If so, update maxLength and endIndex.

*   If prefixSum[i] is not present in sumMap, insert it into the map with its corresponding index.

1.  Finally, check if endIndex is still -1\. If so, there is no subarray with an equal number of 0s and 1s. Otherwise, the longest subarray with equal 0s and 1s will be from index endIndex - maxLength + 1 to endIndex.

Here’s the C++ code implementing the above approach:

#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

int findMaxLength(vector<int>& nums) {
    int n = nums.size();
    vector<int> prefixSum(n);
    unordered_map<int, int> sumMap;
    int maxLength = 0;
    int endIndex = -1;

    prefixSum[0] = nums[0] == 0 ? -1 : 1;
    sumMap[prefixSum[0]] = 0;

    for (int i = 1; i < n; i++) {
        prefixSum[i] = prefixSum[i - 1] + (nums[i] == 0 ? -1 : 1);

        if (prefixSum[i] == 0) {
            maxLength = i + 1;
            endIndex = i;
        } else if (sumMap.find(prefixSum[i]) != sumMap.end()) {
            int length = i - sumMap[prefixSum[i]];
            if (length > maxLength) {
                maxLength = length;
                endIndex = i;
            }
        } else {
            sumMap[prefixSum[i]] = i;
        }
    }

    if (endIndex == -1) {
        // No subarray found
        cout << "No subarray found" << endl;
    } else {
        int startIndex = endIndex - maxLength + 1;
        cout << "Longest subarray with equal 0s and 1s: [" << startIndex << ", " << endIndex << "]" << endl;
    }

    return maxLength;
}

int main() {
    vector<int> nums = {0, 1, 0, 0, 1, 1, 0};
    int maxLength = findMaxLength(nums);

    cout << "Length of the longest subarray: " << maxLength << endl;

    return 0;
}

When you run this program, it will output the starting and ending indices of the longest subarray with an equal number of 0s and 1s, as well as the length of that subarray.

Note: This approach assumes that the input array nums contains only 0s and 1s. If the array may contain other values, you may need to modify the code accordingly.

# 87

# Array Minimum Size Subarray Sum

Here’s an example of a C++ program that finds the minimum size of a subarray with a sum greater than or equal to a given target using the two-pointer technique:

#include <iostream>
#include <vector>
#include <limits>

int minSubarraySize(int target, const std::vector<int>& nums) {
    int n = nums.size();
    int left = 0;  // left pointer
    int sum = 0;   // current sum of subarray elements
    int minLength = std::numeric_limits<int>::max(); // initialize with maximum value

    for (int right = 0; right < n; ++right) {  // right pointer
        sum += nums[right];

        while (sum >= target) {  // shrink the subarray from the left
            minLength = std::min(minLength, right - left + 1);
            sum -= nums[left];
            left++;
        }
    }

    return (minLength == std::numeric_limits<int>::max()) ? 0 : minLength;
}

int main() {
    std::vector<int> nums = {2, 3, 1, 2, 4, 3};
    int target = 7;

    int result = minSubarraySize(target, nums);

    std::cout << "Minimum size of subarray with sum >= " << target << " is " << result << std::endl;

    return 0;
}

Explanation:

1.  We define two pointers, left and right, initially pointing to the first element of the array.

2.  The sum variable keeps track of the current sum of the elements between the two pointers.

3.  We initialize minLength with a very large value to ensure it gets updated correctly later.

4.  We iterate the right pointer over the array. For each iteration, we add the value at nums[right] to the sum.

5.  Inside the main loop, we have a nested loop that checks if the sum is greater than or equal to the target. If it is, we update the minLength by comparing it with the current subarray length (right - left + 1).

6.  We shrink the subarray from the left by subtracting nums[left] from the sum and incrementing left.

7.  We repeat steps 4-6 until the right pointer reaches the end of the array.

8.  Finally, we return the minimum subarray length found. If no subarray is found, we return 0.

9.  In the main function, we create a sample nums array and set the target to 7\. We call the minSubarraySize function and print the result.

When using the two-pointer technique, we maintain a window (subarray) defined by the left and right pointers. By moving these pointers strategically, we can efficiently search for the desired subarray. In this case, we start with a window of size 1 (the right pointer initially coincides with the left pointer). As we move the right pointer forward, we expand the window by adding elements to the sum. If the sum exceeds the target, we shrink the window from the left until the sum is less than the target. This process allows us to find the minimum size subarray that satisfies the given condition.

# 88

# Array Sort Colors

The Dutch National Flag problem is a classic sorting problem where we need to sort an array containing 0s, 1s, and 2s in-place without using any extra space. We can solve this problem using three pointers to partition the array.

Here’s the C++ code to solve the problem:

#include <iostream>
#include <vector>

using namespace std;

void sortColors(vector<int>& nums) {
    int low = 0;            // pointer to keep track of 0s
    int mid = 0;            // pointer to keep track of 1s
    int high = nums.size() - 1; // pointer to keep track of 2s

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums[low], nums[mid]);
            low++;
            mid++;
        }
        else if (nums[mid] == 1) {
            mid++;
        }
        else if (nums[mid] == 2) {
            swap(nums[mid], nums[high]);
            high--;
        }
    }
}

int main() {
    vector<int> nums = {2, 0, 1, 2, 1, 0};

    cout << "Original array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    sortColors(nums);

    cout << "Sorted array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}

Explanation:

1.  We initialize three pointers: low, mid, and high. The low pointer keeps track of the next position to place 0, the mid pointer scans the array, and the high pointer keeps track of the next position to place 2.

2.  We iterate over the array while the mid pointer is less than or equal to the high pointer.

3.  If nums[mid] is 0, we swap it with the element at the low pointer and increment both low and mid pointers. This ensures that all 0s are placed at the beginning of the array.

4.  If nums[mid] is 1, we simply increment the mid pointer and leave the element as it is since 1s should be in the middle of the sorted array.

5.  If nums[mid] is 2, we swap it with the element at the high pointer and decrement the high pointer. This ensures that all 2s are placed at the end of the array.

6.  We repeat steps 3 to 5 until mid pointer crosses the high pointer, which means the array has been sorted.

After running the program, you will see the original array and the sorted array printed on the console.

Note: This algorithm is known as the Dutch National Flag algorithm because it was used to sort an array representing the colors of the Dutch national flag, which has three colors: red, white, and blue, represented by 0, 1, and 2, respectively.

# 89

# Array Sort Colors

The Dutch National Flag problem is a classic sorting problem where we need to sort an array containing 0s, 1s, and 2s in-place without using any extra space. We can solve this problem using three pointers to partition the array.

Here’s the C++ code to solve the problem:

#include <iostream>
#include <vector>

using namespace std;

void sortColors(vector<int>& nums) {
    int low = 0;            // pointer to keep track of 0s
    int mid = 0;            // pointer to keep track of 1s
    int high = nums.size() - 1; // pointer to keep track of 2s

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums[low], nums[mid]);
            low++;
            mid++;
        }
        else if (nums[mid] == 1) {
            mid++;
        }
        else if (nums[mid] == 2) {
            swap(nums[mid], nums[high]);
            high--;
        }
    }
}

int main() {
    vector<int> nums = {2, 0, 1, 2, 1, 0};

    cout << "Original array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    sortColors(nums);

    cout << "Sorted array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}

Explanation:

1.  We initialize three pointers: low, mid, and high. The low pointer keeps track of the next position to place 0, the mid pointer scans the array, and the high pointer keeps track of the next position to place 2.

2.  We iterate over the array while the mid pointer is less than or equal to the high pointer.

3.  If nums[mid] is 0, we swap it with the element at the low pointer and increment both low and mid pointers. This ensures that all 0s are placed at the beginning of the array.

4.  If nums[mid] is 1, we simply increment the mid pointer and leave the element as it is since 1s should be in the middle of the sorted array.

5.  If nums[mid] is 2, we swap it with the element at the high pointer and decrement the high pointer. This ensures that all 2s are placed at the end of the array.

6.  We repeat steps 3 to 5 until mid pointer crosses the high pointer, which means the array has been sorted.

After running the program, you will see the original array and the sorted array printed on the console.

Note: This algorithm is known as the Dutch National Flag algorithm because it was used to sort an array representing the colors of the Dutch national flag, which has three colors: red, white, and blue, represented by 0, 1, and 2, respectively.

# 90

# Array Maximum Frequency Element

To find the element with the maximum frequency in an array using hashing in C++, you can follow these steps:

1.  Create a hash table or a hash map to store the frequencies of each element in the array.

2.  Iterate through the given array and for each element, update its frequency in the hash table.

3.  Initialize two variables: maxFrequency to keep track of the maximum frequency found so far, and maxElement to store the element with the maximum frequency.

4.  Traverse the hash table and for each key-value pair, check if the frequency is greater than the current maxFrequency. If so, update maxFrequency and maxElement accordingly.

5.  After traversing the entire hash table, the variable maxElement will contain the element with the maximum frequency.

Here’s an example implementation in C++:

#include <iostream>
#include <unordered_map>

int findMaxFrequencyElement(int arr[], int size) {
    std::unordered_map<int, int> frequencyMap;
    int maxFrequency = 0;
    int maxElement = arr[0]; // Assuming the first element as the maximum frequency element initially

    for (int i = 0; i < size; i++) {
        int element = arr[i];
        frequencyMap[element]++;
        if (frequencyMap[element] > maxFrequency) {
            maxFrequency = frequencyMap[element];
            maxElement = element;
        }
    }

    return maxElement;
}

int main() {
    int arr[] = {1, 2, 3, 2, 4, 1, 3, 4, 2, 2, 2};
    int size = sizeof(arr) / sizeof(arr[0]);

    int maxFrequencyElement = findMaxFrequencyElement(arr, size);

    std::cout << "Element with maximum frequency: " << maxFrequencyElement << std::endl;

    return 0;
}

In this code, we use an unordered_map (frequencyMap) to store the frequencies of each element in the array. We iterate through the array, update the frequencies in the hash map, and keep track of the element with the maximum frequency (maxElement). Finally, we print the maxFrequencyElement as the result.

Note that unordered_map provides a constant time complexity for insertion and retrieval operations on average, which makes it efficient for this problem.

# 91

# Array Maximum Subarray Sum with No Adjacent Elements

Here’s a C++ program that finds the maximum sum of a subarray in an array, with the constraint that no adjacent elements can be included. The program uses dynamic programming to solve the problem.

#include <iostream>
#include <vector>

using namespace std;

int maxSubarraySum(vector<int>& arr) {
    int n = arr.size();

    if (n == 0) {
        return 0;
    }

    if (n == 1) {
        return arr[0];
    }

    int incl = arr[0];
    int excl = 0;

    for (int i = 1; i < n; i++) {
        int temp = max(incl, excl);  // Choose the maximum sum so far

        incl = excl + arr[i];        // Include the current element, but exclude the previous adjacent element
        excl = temp;                 // Exclude the current element and take the maximum sum so far
    }

    return max(incl, excl);          // Return the maximum sum
}

int main() {
    vector<int> arr = {2, 4, 6, 8, 5, 9, 3};
    int maxSum = maxSubarraySum(arr);

    cout << "Maximum subarray sum with no adjacent elements: " << maxSum << endl;

    return 0;
}

Explanation:

*   The program takes an input array arr and finds the maximum sum of a subarray with no adjacent elements.

*   We initialize two variables, incl and excl, to store the maximum sum including and excluding the current element, respectively.

*   We iterate over the array starting from the second element (index 1) and update the values of incl and excl.

*   For each iteration, we calculate the maximum sum so far (temp) by choosing the maximum of incl and excl.

*   To update incl, we add the current element to excl, as we cannot include adjacent elements.

*   To update excl, we assign it the value of temp, which represents the maximum sum obtained so far.

*   Finally, we return the maximum of incl and excl, which represents the maximum sum of a subarray with no adjacent elements.

In the provided example, the maximum subarray sum with no adjacent elements is 27, which corresponds to the subarray {2, 6, 5, 3}.

# 92

# Array Perfect Peak

To find a perfect peak element in an array using C++, you can follow these steps:

1.  Iterate through the array from the second element to the second-to-last element.

2.  For each element, compare it with its adjacent elements.

3.  If the current element is greater than both its adjacent elements, it is a perfect peak.

4.  Return the index or value of the first perfect peak element found, or any other desired output.

Here’s the C++ code implementing the above approach:

#include <iostream>
#include <vector>

// Function to find a perfect peak element in an array
int findPerfectPeak(const std::vector<int>& arr) {
    int n = arr.size();

    for (int i = 1; i < n - 1; i++) {
        if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
            return arr[i]; // Return the value of the perfect peak element
            // Alternatively, you can return the index by replacing the above line with:
            // return i;
        }
    }

    return -1; // Return -1 if no perfect peak element is found
}

int main() {
    std::vector<int> arr = {1, 3, 5, 4, 2};

    int peak = findPerfectPeak(arr);
    if (peak != -1) {
        std::cout << "Perfect peak element: " << peak << std::endl;
    } else {
        std::cout << "No perfect peak element found." << std::endl;
    }

    return 0;
}

In the findPerfectPeak function, we iterate through the array from the second element (i = 1) to the second-to-last element (i < n - 1). For each element at index i, we compare it with its adjacent elements: arr[i - 1] (previous element) and arr[i + 1] (next element). If the current element is greater than both its adjacent elements, we return it as the perfect peak element. If no perfect peak element is found, we return -1.

In the main function, we create a sample array arr and call the findPerfectPeak function to find the perfect peak element. The result is then printed to the console.

Note: This implementation assumes that there is at least one perfect peak element in the array. If there could be multiple perfect peaks and you want to find all of them, you can modify the code accordingly.

# 93

# Array Repeated Number

To find the repeated number in an array of integers from 1 to n, where n is the size of the array, you can use either the pigeonhole principle or hashing. Here’s an explanation of how both methods can be used to solve this problem:

1.  Pigeonhole Principle: The pigeonhole principle states that if you have more pigeons than pigeonholes, then at least one pigeonhole must contain more than one pigeon. In the context of this problem, the array can be seen as the pigeonholes, and the numbers from 1 to n can be seen as the pigeons. Since there are n numbers and n-1 pigeonholes, at least one number must repeat.

Here’s an implementation using the pigeonhole principle in C++:

#include <iostream>
#include <vector>

int findRepeatedNumber(const std::vector<int>& nums) {
    int n = nums.size() - 1; // The size of the array is n, so the last number is n

    // Create a vector to keep track of the frequency of each number
    std::vector<int> frequency(n + 1, 0);

    // Iterate through the array and increment the frequency count
    for (int num : nums) {
        frequency[num]++;
        // If a number is repeated, its frequency will be more than 1
        if (frequency[num] > 1) {
            return num;
        }
    }

    // No repeated number found
    return -1;
}

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 4, 5}; // Example array with a repeated number

    int repeatedNumber = findRepeatedNumber(nums);
    if (repeatedNumber != -1) {
        std::cout << "The repeated number is: " << repeatedNumber << std::endl;
    } else {
        std::cout << "No repeated number found." << std::endl;
    }

    return 0;
}

1.  Hashing: Hashing involves using a hash table or a similar data structure to store elements and efficiently perform lookup operations. In this case, you can use a hash set to store the numbers as you iterate through the array. Whenever you encounter a number that already exists in the set, it means that number is repeated.

Here’s an implementation using hashing in C++:

#include <iostream>
#include <unordered_set>
#include <vector>

int findRepeatedNumber(const std::vector<int>& nums) {
    std::unordered_set<int> numSet;

    // Iterate through the array
    for (int num : nums) {
        // Check if the number already exists in the set
        if (numSet.count(num) > 0) {
            return num;
        }

        // Add the number to the set
        numSet.insert(num);
    }

    // No repeated number found
    return -1;
}

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 4, 5}; // Example array with a repeated number

    int repeatedNumber = findRepeatedNumber(nums);
    if (repeatedNumber != -1) {
        std::cout << "The repeated number is: " << repeatedNumber << std::endl;
    } else {
        std::cout << "No repeated number found." << std::endl;
    }

    return 0;
}

Both the pigeonhole principle and hashing provide efficient solutions for finding the repeated number in an array. The time complexity for both approaches is O(n) since you need to iterate through the array once. However, the space complexity for the pigeonhole principle approach is O(n) due to the additional vector, while the hashing approach has a space complexity of O(n) due to the hash set.

# 94

# Array Subarray with Maximum XOR

To find the maximum XOR value of a subarray in an array of integers, we can use a trie data structure or utilize the concept of prefix XOR. Let’s first understand how to solve the problem using the trie data structure:

Create a TrieNode structure that consists of an array of two pointers, representing the left and right child nodes, respectively.

struct TrieNode {
    TrieNode* child[2];
    TrieNode() {
        child[0] = nullptr;
        child[1] = nullptr;
    }
};

Create a function to insert numbers into the trie. The function takes two arguments: the root of the trie and the number to be inserted.

void insertNumber(TrieNode* root, int num) {
    TrieNode* curr = root;
    for (int i = 31; i >= 0; i--) {
        int bit = (num >> i) & 1;
        if (curr->child[bit] == nullptr)
            curr->child[bit] = new TrieNode();
        curr = curr->child[bit];
    }
}

Create a function to find the maximum XOR value. This function takes the root of the trie and the array of integers as input.

int findMaxXOR(TrieNode* root, vector<int>& nums) {
    int maxXOR = 0;
    for (int num : nums) {
        TrieNode* curr = root;
        int currXOR = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (curr->child[bit ^ 1] != nullptr) {
                currXOR |= (1 << i);
                curr = curr->child[bit ^ 1];
            } else {
                curr = curr->child[bit];
            }
        }
        maxXOR = max(maxXOR, currXOR);
    }
    return maxXOR;
}

Finally, in the main function, create the root of the trie and call the above functions to find the maximum XOR value.

int main() {
    vector<int> nums = {3, 10, 5, 25, 2, 8};
    TrieNode* root = new TrieNode();
    for (int num : nums)
        insertNumber(root, num);
    int maxXOR = findMaxXOR(root, nums);
    cout << "Maximum XOR value of a subarray: " << maxXOR << endl;
    return 0;
}

Using the trie data structure, we iterate through each number in the array and insert it into the trie, considering each bit of the number. While inserting, we try to follow a different path in the trie to maximize the XOR value. Finally, we find the maximum XOR value by comparing each number with the trie.

Alternatively, we can solve this problem using the concept of prefix XOR:

Create a prefixXOR array that stores the XOR of all elements from index 0 to the current index.

vector<int> prefixXOR(nums.size());
prefixXOR[0] = nums[0];
for (int i = 1; i < nums.size(); i++)
    prefixXOR[i] = prefixXOR[i - 1] ^ nums[i];

Initialize a variable maxXOR with 0.

int maxXOR = 0;

Iterate through each element of the prefixXOR array and find the maximum XOR value by checking all possible subarrays.

for (int i = 0; i < prefixXOR.size(); i++) {
    for (int j = i; j < prefixXOR.size(); j++) {
        int subarrayXOR = prefixXOR[i] ^ prefixXOR[j];
        maxXOR = max(maxXOR, subarrayXOR);
    }
}

Finally, maxXOR will store the maximum XOR value of a subarray.

Using the prefix XOR approach, we calculate the XOR of subarrays efficiently by XORing the prefix XOR values of the elements. By checking all possible subarrays, we can find the maximum XOR value.

Note: The prefix XOR approach has a higher time complexity compared to the trie data structure, but it is simpler to implement. The trie approach is more efficient for large arrays with a huge range of numbers.

# 95

# Array Sum of Absolute Differences

To calculate the sum of absolute differences of all elements in an array using prefix sums, you can follow these steps:

1.  Define an array of integers.

2.  Calculate the prefix sum array. Initialize an auxiliary array called prefixSum of the same size as the original array. Set prefixSum[0] to 0 and then iterate through the elements of the original array from index 1 to the end. For each index i, set prefixSum[i] to prefixSum[i-1] + arr[i-1]. This prefix sum array stores the cumulative sum of all elements up to a particular index.

3.  Calculate the suffix sum array. Initialize another auxiliary array called suffixSum of the same size as the original array. Set suffixSum[n-1] to 0 (where n is the size of the array) and then iterate through the elements of the original array in reverse order, from the second-to-last index to the beginning. For each index i, set suffixSum[i] to suffixSum[i+1] + arr[i+1]. This suffix sum array stores the cumulative sum of all elements starting from a particular index.

4.  Initialize a variable called sumOfAbsoluteDifferences to 0\. This variable will store the final result.

5.  Iterate through the original array from index 0 to the end. For each index i, calculate the absolute difference between prefixSum[i] and suffixSum[i], and add it to sumOfAbsoluteDifferences. This step calculates the absolute difference between the sum of elements to the left of the current index and the sum of elements to the right of the current index. Since we already have the prefix and suffix sum arrays, we can perform this calculation efficiently.

6.  At the end of the loop, sumOfAbsoluteDifferences will contain the sum of absolute differences of all elements in the array.

7.  Print or return sumOfAbsoluteDifferences.

Here’s the C++ code implementing the above steps:

#include <iostream>
#include <vector>
#include <cmath>

int main() {
    // Step 1: Define the array
    std::vector<int> arr = {1, 4, 6, 8, 10};

    // Step 2: Calculate the prefix sum array
    std::vector<int> prefixSum(arr.size() + 1, 0);
    for (int i = 1; i <= arr.size(); i++) {
        prefixSum[i] = prefixSum[i - 1] + arr[i - 1];
    }

    // Step 3: Calculate the suffix sum array
    std::vector<int> suffixSum(arr.size() + 1, 0);
    for (int i = arr.size() - 1; i >= 0; i--) {
        suffixSum[i] = suffixSum[i + 1] + arr[i];
    }

    // Step 4: Calculate the sum of absolute differences
    int sumOfAbsoluteDifferences = 0;
    for (int i = 0; i < arr.size(); i++) {
        sumOfAbsoluteDifferences += std::abs(prefixSum[i] - suffixSum[i]);
    }

    // Step 7: Print the result
    std::cout << "Sum of absolute differences: " << sumOfAbsoluteDifferences << std::endl;

    return 0;
}

When you run this code, it will output the sum of absolute differences of all elements in the array. In the provided example, the output will be:

Sum of absolute differences: 28

Note that this code assumes the availability of the <iostream>, <vector>, and <cmath> libraries.

# 96

# Array Wiggle Sort

Here’s an example program in C++ that sorts an array into a wiggle pattern:

#include <iostream>
#include <algorithm>
using namespace std;

void wiggleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        if (i % 2 == 0) {
            // If the current index is even, the element should be smaller than the next element.
            if (arr[i] > arr[i + 1])
                swap(arr[i], arr[i + 1]);
        } else {
            // If the current index is odd, the element should be greater than the next element.
            if (arr[i] < arr[i + 1])
                swap(arr[i], arr[i + 1]);
        }
    }
}

int main() {
    int arr[] = {3, 5, 2, 1, 6, 4};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Original Array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    wiggleSort(arr, n);

    cout << "\nWiggle Sorted Array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}

Explanation:

1.  The function wiggleSort takes an array (arr) and its size (n) as parameters.

2.  It iterates through the array from the first element to the second-to-last element (n - 1), comparing and swapping adjacent elements to achieve the desired wiggle pattern.

3.  If the current index is even (i % 2 == 0), it checks if the current element is greater than the next element. If it is, the elements are swapped.

4.  If the current index is odd (i % 2 == 1), it checks if the current element is smaller than the next element. If it is, the elements are swapped.

5.  After the sorting process, the main function is called. It creates an example array, calls the wiggleSort function, and prints the original and wiggle sorted arrays.

When you run this program, the output will be:

Original Array: 3 5 2 1 6 4
Wiggle Sorted Array: 3 5 1 6 2 4

The elements have been rearranged to alternate between greater than and less than their adjacent elements, forming a wiggle pattern.

# 97

# Array Range Sum Query

To efficiently handle multiple range sum queries on an array, you can use the concept of prefix sums and dynamic programming. This approach allows you to preprocess the array and answer each query in constant time.

Here’s how you can implement it in C++:

#include <iostream>
#include <vector>

using namespace std;

vector<int> calculatePrefixSums(const vector<int>& nums) {
    int n = nums.size();
    vector<int> prefixSums(n + 1, 0);  // Initialize prefix sums with 0
    for (int i = 0; i < n; i++) {
        prefixSums[i + 1] = prefixSums[i] + nums[i];  // Calculate prefix sums
    }
    return prefixSums;
}

int rangeSumQuery(const vector<int>& prefixSums, int left, int right) {
    return prefixSums[right + 1] - prefixSums[left];  // Calculate range sum using prefix sums
}

int main() {
    vector<int> nums = {1, 3, 2, -5, 4, 6, -2};
    vector<int> prefixSums = calculatePrefixSums(nums);

    // Example queries
    cout << rangeSumQuery(prefixSums, 1, 3) << endl;  // Output: 0 (3 + 2 + (-5) = 0)
    cout << rangeSumQuery(prefixSums, 2, 5) << endl;  // Output: 7 (2 + (-5) + 4 + 6 = 7)

    return 0;
}

In this program, the calculatePrefixSums function takes an array nums and returns a vector prefixSums that contains the prefix sums of nums. The prefixSums vector is initialized with an extra element at the beginning as 0, and each subsequent element is calculated by adding the current element in nums to the previous prefix sum.

The rangeSumQuery function takes the prefixSums vector, along with the left and right indices of the range you want to query. It returns the sum of elements in the range by subtracting the prefix sum at the left index from the prefix sum at the right + 1 index. This subtraction cancels out the sum of elements before the left index, giving you the range sum.

In the main function, you can call the rangeSumQuery function to perform range sum queries on the array. You first calculate the prefixSums vector using the calculatePrefixSums function, and then you can pass it along with the desired range to the rangeSumQuery function to get the result.

Using this approach, you preprocess the array once in linear time to calculate the prefix sums. After that, each range sum query can be answered in constant time by subtracting two prefix sums. Thus, the overall time complexity for handling multiple range sum queries becomes O(n) for preprocessing and O(1) for each query, where n is the size of the array.

# 98

# Array Longest Mountain Subarray

Here’s an example of a C++ program that finds the length of the longest mountain subarray in an array:

#include <iostream>
#include <vector>

using namespace std;

int longestMountain(vector<int>& arr) {
    int n = arr.size();
    int maxLength = 0;

    for (int i = 1; i < n - 1; ) {
        if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
            int left = i - 1;
            int right = i + 1;

            while (left > 0 && arr[left] > arr[left - 1]) {
                left--;
            }

            while (right < n - 1 && arr[right] > arr[right + 1]) {
                right++;
            }

            int currentLength = right - left + 1;
            maxLength = max(maxLength, currentLength);

            i = right; // Jump to the end of the mountain
        } else {
            i++;
        }
    }

    return maxLength;
}

int main() {
    vector<int> arr = { 2, 1, 4, 7, 3, 2, 5 };
    int length = longestMountain(arr);
    cout << "Length of the longest mountain subarray: " << length << endl;

    return 0;
}

Explanation:

1.  We start by initializing the maximum length of the mountain subarray (maxLength) to 0.

2.  We iterate through the array starting from the second element until the second-to-last element (indices 1 to n-2).

3.  For each element, we check if it is greater than its previous element (arr[i] > arr[i - 1]) and also greater than its next element (arr[i] > arr[i + 1]), indicating the start of a mountain subarray.

4.  If the current element satisfies the conditions of a mountain subarray, we initialize the left and right pointers (left = i - 1 and right = i + 1).

5.  We then move the left pointer backwards until it reaches the beginning of the array or until the elements are still increasing (arr[left] > arr[left - 1]).

6.  Similarly, we move the right pointer forwards until it reaches the end of the array or until the elements are still decreasing (arr[right] > arr[right + 1]).

7.  We calculate the length of the current mountain subarray as currentLength = right - left + 1.

8.  We update the maxLength if the current mountain subarray is longer.

9.  Finally, we update the loop variable i to right to skip the elements of the mountain subarray and continue the iteration.

10.  After the loop ends, we return the maxLength as the length of the longest mountain subarray.

In the provided example, the array { 2, 1, 4, 7, 3, 2, 5 } has a mountain subarray of length 5 ({ 1, 4, 7, 3, 2 }), so the output will be:

Length of the longest mountain subarray: 5

Note that the program assumes that the input array has at least 3 elements and that there is at least one mountain subarray present. Additional checks can be added to handle such edge cases if necessary.

# 99

# Array Count Inversions

To count the number of inversions in an array, you can indeed use either merge sort or a Fenwick tree. Both approaches provide efficient solutions to this problem. Here’s an explanation of how to implement them:

Using Merge Sort:

1.  Implement a function that performs merge sort on the array. This function should take the array, its start index, and end index as parameters.

2.  Divide the array into two halves and recursively sort each half using merge sort.

3.  Merge the two sorted halves into a single sorted array while counting the inversions. To count inversions during the merge step, whenever an element from the right subarray is smaller than an element from the left subarray, increment the inversion count by the number of remaining elements in the left subarray.

4.  Finally, return the inversion count.

Here’s the C++ code for the merge sort approach:

#include <iostream>
using namespace std;

long long mergeAndCount(int arr[], int temp[], int left, int mid, int right) {
    int i = left;
    int j = mid + 1;
    int k = left;
    long long inversionCount = 0;

    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
            inversionCount += mid - i + 1;
        }
    }

    while (i <= mid) {
        temp[k++] = arr[i++];
    }

    while (j <= right) {
        temp[k++] = arr[j++];
    }

    for (i = left; i <= right; i++) {
        arr[i] = temp[i];
    }

    return inversionCount;
}

long long mergeSort(int arr[], int temp[], int left, int right) {
    long long inversionCount = 0;

    if (left < right) {
        int mid = (left + right) / 2;
        inversionCount += mergeSort(arr, temp, left, mid);
        inversionCount += mergeSort(arr, temp, mid + 1, right);
        inversionCount += mergeAndCount(arr, temp, left, mid, right);
    }

    return inversionCount;
}

long long countInversions(int arr[], int size) {
    int* temp = new int[size];
    return mergeSort(arr, temp, 0, size - 1);
}

int main() {
    int arr[] = {5, 3, 2, 4, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    long long inversionCount = countInversions(arr, size);

    cout << "Number of inversions: " << inversionCount << endl;

    return 0;
}

Using Fenwick Tree:

1.  Implement a Fenwick tree data structure (also known as Binary Indexed Tree) to efficiently count inversions.

2.  Initialize the Fenwick tree with all zeros.

3.  Traverse the given array from right to left. For each element, query the Fenwick tree to find the sum of elements that are greater than the current element.

4.  Add the current element to the Fenwick tree by updating the corresponding index.

5.  Repeat steps 3 and 4 until all elements have been processed.

6.  The total count of inversions will be the sum of inversions obtained in each step.

7.  Return the inversion count.

Here’s the C++ code for the Fenwick tree approach:

#include <iostream>
using namespace std;

int getSum(int BIT[], int index) {
    int sum = 0;
    while (index > 0) {
        sum += BIT[index];
        index -= index & (-index);
    }
    return sum;
}

void updateBIT(int BIT[], int n, int index, int value) {
    while (index <= n) {
        BIT[index] += value;
        index += index & (-index);
    }
}

long long countInversions(int arr[], int size) {
    int maxElement = 0;
    for (int i = 0; i < size; i++) {
        maxElement = max(maxElement, arr[i]);
    }

    int* BIT = new int[maxElement + 1];
    for (int i = 1; i <= maxElement; i++) {
        BIT[i] = 0;
    }

    long long inversionCount = 0;
    for (int i = size - 1; i >= 0; i--) {
        inversionCount += getSum(BIT, arr[i] - 1);
        updateBIT(BIT, maxElement, arr[i], 1);
    }

    delete[] BIT;

    return inversionCount;
}

int main() {
    int arr[] = {5, 3, 2, 4, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    long long inversionCount = countInversions(arr, size);

    cout << "Number of inversions: " << inversionCount << endl;

    return 0;
}

Both approaches will yield the same output:

Number of inversions: 8

Feel free to modify the code as per your requirements and use it to count inversions in different arrays.

# 100

# Array Maximum Area of Histogram

Here’s a C++ program that finds the maximum rectangular area that can be formed from a histogram represented by an array of heights using a stack:

#include <iostream>
#include <stack>
using namespace std;

int findMaxArea(int heights[], int n) {
    stack<int> st;
    int maxArea = 0;
    int area = 0;
    int i = 0;

    while (i < n) {
        if (st.empty() || heights[st.top()] <= heights[i]) {
            st.push(i);
            i++;
        } else {
            int top = st.top();
            st.pop();
            area = heights[top] * (st.empty() ? i : (i - st.top() - 1));

            if (area > maxArea)
                maxArea = area;
        }
    }

    while (!st.empty()) {
        int top = st.top();
        st.pop();
        area = heights[top] * (st.empty() ? i : (i - st.top() - 1));

        if (area > maxArea)
            maxArea = area;
    }

    return maxArea;
}

int main() {
    int heights[] = {2, 1, 5, 6, 2, 3};
    int n = sizeof(heights) / sizeof(heights[0]);

    int maxArea = findMaxArea(heights, n);
    cout << "Maximum rectangular area: " << maxArea << endl;

    return 0;
}

Explanation:

1.  We use a stack to store the indices of the histogram bars in non-decreasing order of their heights.

2.  We iterate through the array of heights and for each height:

*   If the stack is empty or the current height is greater than or equal to the height at the top of the stack, we push the current index onto the stack and move to the next index.

*   If the current height is less than the height at the top of the stack, we calculate the area of the rectangle that can be formed by the bar at the top of the stack and the current index. We do this by considering the top bar as the smallest bar in the rectangle and finding the width of the rectangle as the difference between the current index and the index at the top of the stack. We pop the top bar from the stack and update the maximum area if necessary.

1.  After iterating through all the heights, we handle the remaining bars in the stack by treating them as the smallest bar in a rectangle and calculating their areas similarly.

2.  Finally, we return the maximum area.

In the given example, the histogram heights are [2, 1, 5, 6, 2, 3]. The maximum rectangular area that can be formed from these heights is 10, which corresponds to the rectangle formed by the bars with heights 5 and 6.

# Appendix

Array Declaration

*   Arrays are a collection of elements of the same data type stored in contiguous memory locations.

*   Syntax: data_type array_name[array_size];

Array Initialization

*   Arrays can be initialized during declaration or later using curly braces {}.

*   Example: int myArray[5] = {1, 2, 3, 4, 5};

Array Access

*   Elements of an array can be accessed using their index (starting from 0).

*   Example: int value = myArray[2]; // value = 3

Array Size

*   The number of elements an array can hold is its size.

*   Example: int myArray[5]; // size = 5

Array Modification

*   Individual elements of an array can be modified using their index.

*   Example: myArray[0] = 10;

Array Traversal

*   Looping through an array to access and process each element is called array traversal.

*   Example:

for (int i = 0; i < size; i++) {
    // Process myArray[i]
}

Array Sorting

*   Sorting the elements of an array in ascending or descending order.

*   Example: std::sort(myArray, myArray + size);

Array Searching

*   Searching for a specific element in an array.

*   Example: int pos = std::find(myArray, myArray + size, 3) - myArray;

Array Copying

*   Copying the contents of one array to another.

*   Example: std::copy(sourceArray, sourceArray + size, destinationArray);

Array Concatenation

*   Combining two arrays into a single array.

*   Example: std::copy(array1, array1 + size1, resultArray); std::copy(array2, array2 + size2, resultArray + size1);

Array Reversal

*   Reversing the order of elements in an array.

*   Example: std::reverse(myArray, myArray + size);

Array Comparison

*   Comparing two arrays to check if they are equal.

*   Example: bool isEqual = std::equal(array1, array1 + size, array2);

Array Sum

*   Calculating the sum of all elements in an array.

*   Example:

int sum = 0;
for (int i = 0; i < size; i++) {
    sum += myArray[i];
}

Array Average

*   Calculating the average of elements in an array.

*   Example: double average = sum / static_cast<double>(size);

Array Maximum

*   Finding the maximum value in an array.

*   Example: int max = *std::max_element(myArray, myArray + size);

Array Minimum

*   Finding the minimum value in an array.

*   Example: int min = *std::min_element(myArray, myArray + size);

Array Unique Elements

*   Finding and removing duplicate elements from an array.

*   Example: std::sort(myArray, myArray + size); myArray.erase(std::unique(myArray, myArray + size), myArray + size);

Array Frequency

*   Counting the occurrences of each element in an array.

*   Example:

std::unordered_map<int, int> frequencyMap;
for (int i = 0; i < size; i++) {
    frequencyMap[myArray[i]]++;
}

Array Subarray

*   Extracting a contiguous portion (subarray) of an array.

*   Example: std::vector<int> subArray(myArray + start, myArray + end + 1);

Array Element Swapping

*   Swapping the positions of two elements in an array.

*   Example: std::swap(myArray[i], myArray[j]);

Array Partition

*   Dividing an array into two parts based on a pivot element.

*   Example: std::partition(myArray, myArray + size, [](int x) { return x < pivot; });

Array Shuffling

*   Randomly rearranging the elements in an array.

*   Example: std::random_shuffle(myArray, myArray + size);

Array Rotation

*   Rotating the elements of an array to the left or right by a given number of positions.

*   Example:

std::rotate(myArray, myArray + numPositions, myArray + size); // Left rotation
std::rotate(myArray, myArray + size - numPositions, myArray + size); // Right rotation

Array Insertion

*   Inserting a new element at a specific position in an array.

*   Example: myArray[position] = newValue;

Array Deletion

*   Removing an element from an array by shifting the remaining elements.

*   Example: std::copy(myArray + position + 1, myArray + size, myArray + position);

Array Palindrome

*   Checking if an array is a palindrome (reads the same forwards and backwards).

*   Example: Compare elements from the beginning and end of the array.

Array Intersection

*   Finding common elements between two arrays.

*   Example: std::set_intersection(array1, array1 + size1, array2, array2 + size2, resultArray);

Array Union

*   Combining elements from two arrays without duplicates.

*   Example: std::set_union(array1, array1 + size1, array2, array2 + size2, resultArray);

Array Difference

*   Finding elements present in one array but not in another.

*   Example: std::set_difference(array1, array1 + size1, array2, array2 + size2, resultArray);

Array Subset

*   Checking if one array is a subset of another.

*   Example:

bool isSubset = std::includes(array1, array1 + size1, array2, array2 + size2);

Array Symmetry

*   Checking if an array is symmetric (mirrored around its center).

*   Example: Compare elements from both ends towards the center.

Array Majority Element

*   Finding an element that appears more than half the time in the array.

*   Example: Use Moore’s voting algorithm.

Array Missing Element

*   Finding the missing element in a sequence of numbers in an array.

*   Example: Check for gaps between consecutive elements.

Array Range

*   Finding the range (difference between the maximum and minimum) of elements in an array.

*   Example: int range = max - min;

Array Product

*   Calculating the product of all elements in an array.

*   Example:

int product = 1;
for (int i = 0; i < size; i++) {
    product *= myArray[i];
}

Array Partitioning

*   Dividing an array into equal-sum partitions (subarrays).

*   Example: Use backtracking or dynamic programming.

Array Duplicates

*   Finding duplicate elements in an array.

*   Example: Use a hash set or sorting.

Array Even-Odd Partitioning

*   Rearranging elements in an array such that even elements appear first, followed by odd elements.

*   Example: Use two pointers approach.

Array Zero Sum Subarray

*   Finding subarrays with a sum of zero.

*   Example: Use prefix sum technique or hashing.

Array Longest Increasing Subarray

*   Finding the longest contiguous subarray with elements in strictly increasing order.

*   Example: Use a sliding window or dynamic programming.

Array Longest Common Subsequence

*   Finding the longest sequence that is present in both arrays.

*   Example: Use dynamic programming.

Array Longest Palindromic Subsequence

*   Finding the longest sequence that is a palindrome.

*   Example: Use dynamic programming.

Array Longest Bitonic Subarray

*   Finding the longest subarray with elements first increasing and then decreasing.

*   Example: Use dynamic programming.

Array Maximum Sum Subarray

*   Finding the contiguous subarray with the largest sum.

*   Example: Kadane’s algorithm.

Array Circular Subarray Sum

*   Finding the maximum sum of any possible circular subarray.

*   Example: Consider both non-circular and circular cases.

Array Kth Smallest Element

*   Finding the kth smallest element in an array.

*   Example: Use sorting or priority queues.

Array Consecutive Elements

*   Checking if an array contains consecutive elements.

*   Example: Sort the array and check for consecutive values.

Array Peaks and Valleys

*   Rearranging an array such that each element is greater (peak) or smaller (valley) than its neighbors.

*   Example: Sort the array and swap adjacent elements.

Array Majority Elements

*   Finding elements that appear more than n/3 times in an array.

*   Example: Use Boyer-Moore majority vote algorithm.

Array Leader Elements

*   Finding elements that appear more than the sum of the rest of the elements.

*   Example: Use a stack or iterate from right to left.

Array Equilibrium Index

*   Finding the index where the sum of elements on the left and right sides is equal.

*   Example: Calculate prefix and suffix sums.

Array Rearrangement

*   Rearranging an array such that arr[i] becomes arr[arr[i]].

*   Example: Use arithmetic operations.

Array Max Consecutive Ones

*   Finding the maximum number of consecutive ones in a binary array.

*   Example: Use a counter and iterate through the array.

Array Zigzag Traversal

*   Traversing a matrix in a zigzag pattern.

*   Example: Use direction change logic.

Array Spiral Traversal

*   Traversing a matrix in a spiral pattern.

*   Example: Iterate through the boundaries.

Array Pascal’s Triangle

*   Generating Pascal’s triangle in an array format.

*   Example: Use nested loops.

Array Rotated Sorted Search

*   Searching for an element in a rotated sorted array.

*   Example: Use binary search with modified conditions.

Array Maximal Square

*   Finding the largest square of 1’s in a binary matrix.

*   Example: Use dynamic programming.

Array Frequency Count

*   Counting the frequency of elements and storing them in a separate array.

*   Example: Use a hash map.

Array Median

*   Finding the median (middle) value of elements in an array.

*   Example: Sort the array and find the middle element.

Array Inversion Count

*   Counting the number of inversions in an array (pairs where i < j but arr[i] > arr[j]).

*   Example: Use merge sort with inversion count.

Array Next Permutation

*   Finding the lexicographically next greater permutation of an array.

*   Example: Use std::next_permutation().

Array Three Sum

*   Finding all unique triplets that sum to a given value.

*   Example: Use a three-pointer approach.

Array Two Sum

*   Finding two elements in the array that sum to a given value.

*   Example: Use a hash set.

Array Valid Mountain

*   Checking if an array represents a valid mountain.

*   Example: Traverse up and down the mountain.

Array Sliding Window Maximum

*   Finding the maximum in each contiguous subarray of size k.

*   Example: Use a deque to store indices.

Array Dutch National Flag

*   Rearranging an array of 0s, 1s, and 2s in a specific order.

*   Example: Use three-way partitioning.

Array Next Greater Element

*   Finding the next greater element for each element in the array.

*   Example: Use a stack.

Array Subarray with Given Sum

*   Finding subarrays with a given sum.

*   Example: Use prefix sum and hashing.

Array Product of Array Except Self

*   Finding the product of all elements in the array except the current element.

*   Example: Use two arrays for left and right products.

Array First Missing Positive

*   Finding the first missing positive integer in an unsorted array.

*   Example: Use cyclic sort.

Array Game of Life

*   Implementing Conway’s Game of Life using an array.

*   Example: Use a separate array to store the next state.

Array Jump Game

*   Determining if it is possible to reach the last index from the first index in an array.

*   Example: Use greedy algorithm.

Array Max Points on a Line

*   Finding the maximum number of points lying on the same line in a 2D plane.

*   Example: Use a hash map to store slopes.

Array Merge Intervals

*   Merging overlapping intervals in a 2D array.

*   Example: Sort the intervals and merge them.

Array Plus One

*   Adding one to a number represented as an array of digits.

*   Example: Handle carry from right to left.

Array Triplet Sum Closest

*   Finding the sum of three elements in the array closest to a given target.

*   Example: Use three-pointer approach with sorting.

Array Subsets

*   Generating all possible subsets of an array.

*   Example: Use recursion with backtracking.

Array Unique Paths

*   Finding the number of unique paths from the top-left corner to the bottom-right corner in a 2D matrix.

*   Example: Use dynamic programming.

Array Submatrix Sum

*   Finding the sum of all elements in a submatrix of a 2D array.

*   Example: Use prefix sum for each row.

Array Spiral Matrix Generation

*   Generating a spiral matrix given its size.

*   Example: Traverse in spiral order and update elements.

Array Target Sum

*   Finding pairs of elements that sum to a given target value.

*   Example: Use a hash map to store complements.

Array Maximum Subarray Product

*   Finding the maximum product of any contiguous subarray.

*   Example: Use two pointers or dynamic programming.

Array Kth Largest Element

*   Finding the kth largest element in an unsorted array.

*   Example: Use quick-select algorithm.

Array Subarray with Equal 0s and 1s

*   Finding the maximum length subarray with an equal number of 0s and 1s.

*   Example: Use prefix sum and hashing.

Array Minimum Size Subarray Sum

*   Finding the minimum length subarray with a sum greater than or equal to a given value.

*   Example: Use two pointers.

Array Sort Colors

*   Rearranging an array of 0s, 1s, and 2s in ascending order.

*   Example: Use Dutch National Flag algorithm.

Array Longest Consecutive Sequence

*   Finding the longest consecutive sequence of elements in an unsorted array.

*   Example: Use a hash set.

Array Maximum Frequency Element

*   Finding the element with the highest frequency in an array.

*   Example: Use a hash map.

Array Maximum Subarray Sum with No Adjacent Elements

*   Finding the maximum sum of any subarray with no adjacent elements.

*   Example: Use dynamic programming with an extra array.

Array Perfect Peak

*   Finding an element in an array that is greater than all elements to its left and smaller than all elements to its right.

*   Example: Use two arrays to store maximum and minimum elements.

Array Repeated Number

*   Finding a repeated number in an array containing elements from 1 to n-1.

*   Example: Use Floyd’s cycle-finding algorithm.

Array Subarray with Maximum XOR

*   Finding the maximum XOR value of any two elements in an array.

*   Example: Use a trie data structure.

Array Sum of Absolute Differences

*   Calculating the sum of absolute differences between each element and every other element in the array.

*   Example: Use prefix sum technique.

Array Wiggle Sort

*   Rearranging an array such that nums[0] <= nums[1] >= nums[2] <= nums[3] …

*   Example: Sort the array and swap adjacent elements.

Array Range Sum Query

*   Finding the sum of elements in a range of an array.

*   Example: Use segment trees or prefix sum.

Array Longest Mountain Subarray

*   Finding the length of the longest subarray that is a mountain (increasing followed by decreasing).

*   Example: Use two pointers.

Array Count Inversions

*   Counting the number of inversions in an array (pairs where i < j but arr[i] > arr[j]).

*   Example: Use merge sort with inversion count.

Whew! These are some of the most important concepts and topics related to arrays in C++. Each topic has its own applications and usage scenarios, so understanding them thoroughly can greatly enhance your programming capabilities.