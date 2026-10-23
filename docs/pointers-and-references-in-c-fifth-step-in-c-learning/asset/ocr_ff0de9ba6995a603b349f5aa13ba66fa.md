# Pointer to Constant Member Variable

Here’s an example program that demonstrates the use of a pointer to a constant member variable in C++:

```
```cpp
#include <iostream>

class MyClass {
public:
    int myVariable;

    MyClass(int value) : myVariable(value) {}
    int getVariable() const { return myVariable; }
};

int main() {
    MyClass obj(42);
    const MyClass* ptr = &obj;  // Pointer to a constant object

    std::cout << "Value of myVariable: " << ptr->getVariable() << std::endl;

    // Accessing the constant member variable through the pointer
    std::cout << "Accessing constant member variable: " << ptr->myVariable << std::endl;
```
```