std::reference_wrapper can be used to pass references to functions.

std::reference_wrapper automatically deduces the type and const properties of the object wrapped.

# std::ref

std::ref is a convenience template for creating a reference wrapper for a variable.

```
#include <iostream>
#include <functional>

int main() {
    int x = 5;

    // this creates a reference wrapper for variable x and
    // assigns it to wrapper
    std::reference_wrapper wrapper = std::ref(x);

    std::cout << wrapper << std::endl;
    wrapper++;
    std::cout << wrapper << std::endl;

    return 0;
}
```

+   - output
5
6

If x is a reference wrapper then std::ref simply makes a copy of the variable.

# const Reference Wrappers

std::cref creates a const reference wrapper. That is, the value of the reference variable cannot be changed.