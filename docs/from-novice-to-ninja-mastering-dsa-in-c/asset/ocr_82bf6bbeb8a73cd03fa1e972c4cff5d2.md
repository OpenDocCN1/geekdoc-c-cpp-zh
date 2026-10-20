# Function Objects (Functors):

Function objects, also known as functors, are objects that can be called like functions. They are often used with algorithms that require callable entities.

```
#include <iostream>

struct Square {
    int operator()(int x) const {
        return x * x;
    }
};

int main() {
    Square square;
    std::cout << square(5) << std::endl;  // Outputs 25
    return 0;
}
```

# Smart Pointers:

Smart pointers, introduced in C++11, are a part of the STL and provide automatic memory management, helping to avoid memory leaks and improve code safety.

+   Shared Pointer:-

```
#include <memory>

std::shared_ptr<int> sharedInt = std::make_shared<int>(42);
```

+   Unique Pointer:-

```
#include <memory>

std::unique_ptr<double> uniqueDouble =
std::make_unique<double>(3.14);
```

# Conclusion:

The Standard Template Library is a versatile and powerful feature of C++, providing developers with a rich set of tools for data manipulation, algorithms, and resource management. Understanding the STL is essential for writing efficient and maintainable C++ code.