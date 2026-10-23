# Pointer to Pointer

Here’s an example program that demonstrates the usage of a pointer to a pointer in C++:

```
```cpp
#include <iostream>

int main() {
    int value = 42;
    int* ptr = &value;             // Pointer to an integer
    int** ptrToPtr = &ptr;         // Pointer to a pointer

    std::cout << "Value: " << value << std::endl;
    std::cout << "Pointer: " << *ptr << std::endl;
    std::cout << "Pointer to Pointer: " << **ptrToPtr << std::endl;

    return 0;
}
```
```

In the above code, we declare a variable value with a value of 42. We then declare a pointer ptr that points to the memory location of value. Next, we declare a pointer to a pointer ptrToPtr and assign it the address of ptr. To declare a pointer to a pointer, you simply use an additional asterisk (*) before the pointer variable name. In