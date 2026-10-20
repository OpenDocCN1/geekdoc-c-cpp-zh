```
std::cout << "Original value: " << x <<
std::endl;  // Outputs "Original value: 42"

return 0;
}
```

# Lambda Expressions in Algorithms

Lambda expressions are commonly used with algorithms from the Standard Template Library (STL), providing a concise way to define custom behaviours.

```
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // Using a lambda expression with std::for_each to square each element
    std::for_each(numbers.begin(), numbers.end(),
    [](int& x) {
        x = x * x;
    });

    // Print the squared values
    for (const auto& num : numbers) {
        std::cout << num << " ";
    }

    return 0;
}
```

Lambda expressions add expressiveness and flexibility to C++, allowing developers to create concise and in-place function objects. Their usage is prevalent in modern C++, especially in combination with algorithms and other functional programming concepts.