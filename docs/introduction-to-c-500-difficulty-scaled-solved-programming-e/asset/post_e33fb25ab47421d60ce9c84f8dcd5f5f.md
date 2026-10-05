
U.6.13 Write a program that reads an integer and displays the number of bits set. For example, if the user enters 30 (binary: 0000000000000000000000111110), the program should display 4.

U.6.14 Write a program that reads eight bits (each bit is 0 or 1) and displays the corresponding unsigned integer, assuming the bits are entered from left to right. For example, if the user enters 10000000 the program should display 128.

U.6.15 Write a program that uses rand() to generate the integers 0 and 1 in a random number. The program should read an integer that corresponds to rand() calls and display the maximum number of successive 0 and 1 pairs in the generated sequence. For example, if the user enters 15, rand() should be called 15 times and, let's say, the generated sequence is 01001101010100, the program should display 2, because that is the maximum number of pairs with successive 01.

U.6.16 What is the output of the following program?

```
#include <iostream>
int main()
{
    int i, j, k = 100;

    for(i = 0; i < 2; i++) {
        std::cout << "One ";
        for(j = 0; j < k; j++) {
            std::cout << "Two ";
            k -= 50;
        }
        return 0;
    }
}
```

U.6.17 Write a program that reads an integer which corresponds to a number of lines. The program should display in each line a number of '*' equal to the line number. For example, if the user enters 5 the program should display:

+   *
**
***
****
*****
******

U.6.18 Write a program that reads an integer which corresponds to a number of lines. Suppose that the user enters 4. The program should add spaces and '*' according to the line number, as shown below (three spaces at left of one '*', two spaces at left of two '*' in the second line, and so on). When the last line is reached, the first line, the program should display in each line one '*' and the spaces at the right of '*', until one '*' is displayed.

+   *
**
***
****
*****
******

**U.6.19** Write a program that reads two integers (e.g., M, N) and produces an M×N grid. Each grid cell should be 3×2 characters wide. For example, see a 3x5 grid:

```
+---+---+----+----+---+
|   |   |   |   |   |
+---+---+----+----+---+
|   |   |   |   |   |
+---+---+----+----+---+
|   |   |   |   |   |
+---+---+----+----+---+
|   |   |   |   |   |
+---+---+----+----+---+
|   |   |   |   |   |
+---+---+----+----+---+
```

The three horizontal characters of each cell are: +- and the two verticals: +|

**U.6.20** Write a program that reads a positive integer (e.g., N) and calculates the sum of:

```
5/3 + 25/9 + 125/27 + ...
```

until it becomes greater than N. The program should display the last valid sum and the number of terms, before it terminates.

**U.6.21** Write a program that reads an integer (e.g., N) and displays the sum of:

```
1/1× + 1/3× + 1/5× + ... + (N-2)×N
```

The program should force the user to enter a positive integer less than 20. Use one loop only.

**U.6.22** Write a program that reads an integer (e.g., N) and displays the sum of: 2²+4²+6²+ + ... + (2×N)².
The program should force the user to enter a positive integer less than 20.

**U.6.23** Write a program that reads 100 integers and displays the number entered the most successive times. If more than one number entered the same most successive times, the program should display the last one.

**U.6.24** Write a program that reads 100 integers and displays the two largest values.

**U.6.25** Write a program that reads an integer and displays the prime numbers that are less than or equal to it. It is reminded that a prime number is any integer greater than 1 with no divisor other 1 and itself.

**U.6.26** Write a program that reads an integer and displays its digits in words. If the number is negative

**U.6.27** Write a program that reads a positive integer and checks if it is an Armstrong number. An Armstrong number is a number that is equal to the sum of its digits raised to the power of the number of digits. For example, the three-digit number 153 is an Armstrong number, because

```
1³ + 5³ + 3³ = 1 + 125 + 27 = 153.
```

# Arrays 7

An array is a data structure that contains values of the same type. In this chapter, we'll discuss how to declare, initialize, and access arrays. We'll also explore multidimensional arrays.

When declaring an array, the compiler allocates a memory block to store the values. Values are stored one another in consecutive memory locations. Typically, this memory block is allocated in stack and it is automatically released when the function that declares the array terminates.

To declare an array, you must specify the name and the number of elements. The size must be a constant expression. For example:

```cpp
int arr[100];
```

The size of the array can be determined using the `sizeof` operator. For example, `sizeof(arr)` will return the total number of bytes occupied by the array.

Elements of an array are accessed using an index, which starts at zero. For example, to access the first element, we use `arr[0]`.

# ONE-DIMENSIONAL ARRAYS

## Declaration

To declare a one-dimensional array, you specify the type, the name, and the number of elements. The size must be a constant expression known at compile time. For example:

```cpp
int numbers[5];
```

## Initialization

An array can be initialized at the time of declaration. For example:

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
```

If the number of elements is not specified, the compiler will determine it based on the list of initializers.

```cpp
int numbers[] = {1, 2, 3, 4, 5};
```

If only some elements are initialized, the remaining elements are initialized to zero.

```cpp
int numbers[5] = {1, 2}; // numbers is {1, 2, 0, 0, 0}
```

## Accessing Elements

To access an element, we write the array’s name followed by the element’s index inside brackets []. The index specifies the position of the element within the array, and it must be an integer constant, variable, or expression. For example:

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
int first = numbers[0]; // first is 10
int third = numbers[2]; // third is 30
```

## Modification

The elements of an array can be modified using the index. For example:

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
numbers[0] = 100; // the first element is now 100
numbers[4] = 0;   // the last element is now 0
```

## Iteration

Arrays can be iterated over using `for` loops. For example:

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
for(int i = 0; i < 5; i++) {
    std::cout << numbers[i] << " ";
}
```

# Multidimensional Arrays

A multidimensional array is an array of arrays. The most common type is the two-dimensional array, which can be thought of as a table of values.

## Declaration

A two-dimensional array is declared by specifying the type, the name, and the number of rows and columns. For example:

```cpp
int matrix[3][4];
```

## Initialization

A two-dimensional array can be initialized using nested lists. For example:

```cpp
int matrix[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

## Accessing Elements

Elements of a two-dimensional array are accessed using two indices. For example:

```cpp
int value = matrix[1][2]; // value is 7 (the element at row 1, column 2)
matrix[0][0] = 10; // the element at row 0, column 0 becomes 10
```

# Three-Dimensional Arrays

A three-dimensional array is an array of multidimensional arrays. It can be thought of as a cube of values.

## Declaration

A three-dimensional array is declared by specifying the type, the name, and the number of layers, rows, and columns. For example:

```cpp
int cube[2][3][4];
```

## Initialization

A three-dimensional array can be initialized using triple nested lists. For example:

```cpp
int cube[2][3][4] = {
    {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}},
    {{13, 14, 15, 16}, {17, 18, 19, 20}, {21, 22, 23, 24}}
};
```

# Arrays and Pointers

In C++, the name of an array acts as a pointer to its first element. This relationship between arrays and pointers is powerful and allows for dynamic memory allocation and efficient passing arrays to functions.

## Dynamic Memory Allocation

To allocate an array on the heap, we use the `new` operator. For example:

```cpp
int size;
std::cin >> size;
int* arr = new int[size];
// ... use the array ...
delete[] arr; // release the memory
```

## Passing Arrays to Functions

When an array is passed to a function, only the pointer to its first element is passed. For example:

```cpp
void printArray(int arr[], int size) {
    for(int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
}

int main() {
    int myArr[] = {1, 2, 3, 4, 5};
    printArray(myArr, 5);
    return 0;
}
```
