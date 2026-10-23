# Pointer and Reference Casting

Here’s an example program that demonstrates casting between pointers and references of different types in C++:

```
#include <iostream>

class Base {
public:
    virtual void display() {
        std::cout << "Base class" << std::endl;
    }
};

class Derived : public Base {
public:
    void display() override {
        std::cout << "Derived class" << std::endl;
    }
};

int main() {
    // Casting between pointers
```