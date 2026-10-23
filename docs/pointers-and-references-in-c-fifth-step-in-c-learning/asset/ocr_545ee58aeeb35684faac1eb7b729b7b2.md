# Pointer Dereferencing

Here’s an example program in C++ that demonstrates pointer dereferencing:

```
#include <iostream>

int main() {
    int number = 42;
    int* pointer = &number; // pointer holds the memory address of 'number'

    std::cout << "Value of 'number': " << number << std::endl;
    std::cout << "Value stored at the memory address held by 'pointer': " << *pointer << std::endl;

    return 0;
}
```

In this program, we have an integer variable named number initialized with the value 42. We also declare a pointer named pointer of type int*, which means it can store the memory address of an integer variable.

To assign the memory address of number to pointer, we use the ampersand (&) operator followed by the variable name (&number). This operation is called “taking the address of number.” Now, pointer contains the