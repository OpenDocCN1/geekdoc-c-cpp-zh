![](bbox=[0.117, 0.113, 0.176, 0.152])

# volatile and Multithreading Semantics

volatile is typically used to denote objects that can change independently of the regular program flow. These are, for example, objects in embedded programming that represent an external device (memory-mapped I/O). Because these objects can change independently of the regular program flow and their value is directly written to main memory, no optimized storing in caches takes place. In other words, volatile avoids aggressive optimization and has no multithreading semantics.

# 4.9.2 Range-based for loop with Initializers

With C++20, you can directly use a range-based for loop with an initializer.

Range-based for loop with initializer

```
```cpp
// rangeBasedForLoopInitializer.cpp

#include <iostream>
#include <string>
#include <vector>

int main() {

    for (auto vec = std::vector{1, 2, 3}; auto v : vec) {
        std::cout << v << " ";
    }

    std::cout << "\n\n";

    for (auto initList = {1, 2, 3}; auto e : initList) {
        e *= e;
        std::cout << e << " ";
    }

    std::cout << "\n\n";

    using namespace std::string_literals;
    for (auto str = "Hello World"s; auto c : str) {
        std::cout << c << " ";
    }

    std::cout << '\n';
}
```
```