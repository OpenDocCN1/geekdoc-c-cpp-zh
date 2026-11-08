# Applying the fill character and alignment

```
```cpp
// formatFillAlign.cpp

#include <format>
#include <iostream>

int main() {

    std::cout << '\n';

    int num = 2020;

    std::cout << std::format("{:6}", num) << '\n';
    std::cout << std::format("{:6}", 'x') << '\n';
    std::cout << std::format("{:*^6}", 'x') << '\n';
    std::cout << std::format("{:*<6}", 'x') << '\n';
    std::cout << std::format("{:*>6}", 'x') << '\n';
    std::cout << std::format("{:6d}", num) << '\n';
    std::cout << std::format("{:6}", true) << '\n';

    std::cout << '\n';
}
```
```

The default alignment depends on the used types. In contrast to the iostream operator, boolean values are displayed as true or false.

![](bbox=[0.303, 0.61, 0.697, 0.826])

Applying the fill character and alignment