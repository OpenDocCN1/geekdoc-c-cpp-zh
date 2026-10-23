# Pointer to Member Variable

Here’s an example program that demonstrates the usage of a pointer to a member variable in C++:

```
#include <iostream>

class MyClass {
public:
    int myVariable;
};

int main() {
    MyClass obj;
    obj.myVariable = 42;

    int MyClass::*ptr = &MyClass::myVariable;  // Declare a pointer to a member variable

    // Accessing the member variable directly
    std::cout << "Value of myVariable (direct access): " << obj.myVariable << std::endl;

    // Accessing the member variable through the pointer
    std::cout << "Value of myVariable (pointer access): " << obj.*ptr << std::endl;
```