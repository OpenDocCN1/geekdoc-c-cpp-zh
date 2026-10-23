# Pointer Arithmetic

Here’s an example program in C++ that demonstrates arithmetic operations on a pointer variable:

```
#include <iostream>

int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int* ptr = numbers;  // Pointer to the first element of the array

    // Increment the pointer and access the next element
    ptr++;  // Moves the pointer to the next integer in the array
    std::cout << "Next element: " << *ptr << std::endl;

    // Decrement the pointer and access the previous element
    ptr--;  // Moves the pointer back to the previous integer in the array
    std::cout << "Previous element: " << *ptr << std::endl;

    // Perform arithmetic operations on the pointer
    ptr += 2;  // Moves the pointer two positions forward
    std::cout << "Element at index 2: " << *ptr << std::endl;
```