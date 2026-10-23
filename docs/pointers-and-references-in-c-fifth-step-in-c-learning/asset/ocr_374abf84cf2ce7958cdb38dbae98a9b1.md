# Pointers and Dynamic Memory Allocation for Arrays

Here’s an example program in C++ that demonstrates dynamic memory allocation for arrays using the new keyword and accessing the allocated memory through a pointer:

```
```cpp
#include <iostream>

int main() {
    int size;
    std::cout << "Enter the size of the array: ";
    std::cin >> size;

    // Dynamically allocate memory for the array
    int* dynamicArray = new int[size];

    // Access and modify the elements of the array through the pointer
    for (int i = 0; i < size; i++) {
        dynamicArray[i] = i + 1;
    }

    // Print the elements of the array
    std::cout << "Array elements: ";
```
```