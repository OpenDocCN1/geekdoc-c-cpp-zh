# Pointers and Arrays

Here’s an example program in C++ that demonstrates the use of pointers to access elements of an array:

```
```cpp
#include <iostream>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int* ptr = arr; // Pointer initialized to the start of the array

    // Accessing array elements using pointer
    std::cout << "Array elements: ";
    for (int i = 0; i < 5; i++) {
        std::cout << *ptr << " "; // Dereference the pointer to get the value
        ptr++; // Increment the pointer to access the next element
    }

    std::cout << std::endl;

    return 0;
}
```
```