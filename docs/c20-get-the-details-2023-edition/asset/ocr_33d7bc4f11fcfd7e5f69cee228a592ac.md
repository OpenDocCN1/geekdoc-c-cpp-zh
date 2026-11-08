The one-dimensional existing array can be a C-string, a std::initializer_list, or a one-dimensional array of std::pair. The following example is from cppreference.com/to_array².

# **Create a std::array from various one-dimensional arrays**

```
```cpp
// toArray.cpp

#include <iostream>
#include <utility>
#include <array>
#include <memory>

int main() {

    std::cout << '\n';

    auto arr1 = std::to_array("A simple test");
    for (auto a: arr1) std::cout << a;
    std::cout << "\n\n";

    auto arr2 = std::to_array({1, 2, 3, 4, 5});
    for (auto a: arr2) std::cout << a;
    std::cout << "\n\n";

    auto arr3 = std::to_array<double>({0, 1, 3});
    for (auto a: arr3) std::cout << a;
    std::cout << '\n';
    std::cout << "typeid(arr3[0]).name(): " << typeid(arr3[0]).name() << '\n';
    std::cout << '\n';

    auto arr4 = std::to_array<std::pair<int, double>>({ {1, 0.0}, {2, 5.1},
                                                       {3, 5.1} });
    for (auto p: arr4) {
        std::cout << "(" << p.first << ", " << p.second << ")" << '\n';
    }

    std::cout << "\n\n";
}
```
```

I created a std::array from a C-string (line 12), from a std::initializer_list (lines 16 and 20), and from a std::initializer_list of std::pair's (line 26). In general, the compiler can deduce the type of the std::array. Optionally, you can specify the type (lines 20 and 26).

²https://en.cppreference.com/w/cpp/container/array/to_array