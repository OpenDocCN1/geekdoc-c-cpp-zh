# Pointers and References in Templates

Here’s an example program that demonstrates the usage of pointers and references in template classes and functions:

```
#include <iostream>

// Template class with a pointer member
template <typename T>
class PointerClass {
public:
    PointerClass(T* ptr) : ptr_(ptr) {}

    T* getPointer() const {
        return ptr_;
    }

private:
    T* ptr_;
};

// Template function that accepts a reference
```