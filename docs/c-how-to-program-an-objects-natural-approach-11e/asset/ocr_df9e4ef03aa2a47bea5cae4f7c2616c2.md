```
```cpp
// fig07_14.cpp
// C++20: Creating std::arrays from string literals with to_array.
#include <format>
#include <iostream>
#include <array>

int main() {
    // lambda to display a collection of items
    const auto display{
        [](const auto& items) {
            for (const auto& item : items) {
                std::cout << std::format("{} ", item);
            }
        }
    };

    // initializing an array with a string literal
    // creates a one-element array<const char*>
    const auto array1{std::array{"abc"}};
    std::cout << std::format("array1.size() = {}\narray1: ",
        array1.size());
    display(array1); // use lambda to display contents

    // creating std::array of characters from a string literal
    const auto array2{std::to_array("C++20")};
    std::cout << std::format("\narray2.size() = {}\narray2: ",
        array2.size());
    display(array2); // use lambda to display contents

    std::cout << '\n';
}
```
```

```
```text
array1.size() = 1
array1: abc

array2.size() = 6
array2: C + + 2 0
```
```

**Fig. 7.14** | C++20: Creating `std::array`s from string literals with `to_array`.

# Initializing a std::array from a String Literal Creates a One-Element array

Line 19 creates a one-element array containing a `const char*` pointing to the C-string "abc".

# Passing a String Literal to to_array Creates a std::array of char

On the other hand, passing to_array a string literal (line 25) creates a std::array of chars containing elements for each character and the terminating null character. Lines 25–26 confirm that the array’s size is 6. Line 27 confirms the array’s contents. The null character does not have a visual representation, so it does not appear in the output.