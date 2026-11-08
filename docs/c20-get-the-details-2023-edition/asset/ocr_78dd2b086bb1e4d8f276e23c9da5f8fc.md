# 8.1.2.4 Formatting Ranges

C++23 enables it to format ranges.

**Applying the format specification to the elements of a `std::vector`**

```
```cpp
// FormatVector.cpp

#include <format>
#include <iostream>
#include <string>
#include <vector>

int main() {

    std::vector<int> myInts{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    std::cout << std::format("{}\n", myInts);
    std::cout << std::format("{:+}\n", myInts);
    std::cout << std::format("{:02x}\n", myInts);
    std::cout << std::format("{:b}\n", myInts);

    std::cout << '\n';

    std::vector<std::string> myStrings{"Only", "for", "testing", "purpose"};
    std::cout << std::format("{}\n", myStrings);
    std::cout << std::format("{:.3}\n", myStrings);

}
```
```

By default (lines 11 and 19), the `std::vector` is displayed with surrounding square brackets. You can also apply format specifiers to the elements of the range by using an additional colon `:`.

```
```text
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[+1, +2, +3, +4, +5, +6, +7, +8, +9, +10]
[001, 002, 003, 004, 005, 006, 007, 008, 009, 010]
[1, 10, 11, 100, 101, 110, 111, 1000, 1001, 1010]

[Only, for, testing, purpose]
[Onl, for, tes, pur]
```
```

**Applying the format specification to the elements of a `std::vector`**