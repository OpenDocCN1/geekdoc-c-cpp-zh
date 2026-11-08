# Converting a view into a `std::views::common`

```
```cpp
// commonView.cpp

#include <iostream>
#include <numeric>
#include <ranges>
#include <vector>

int main() {

    std::cout << '\n';

    auto results = std::views::iota(100) |
                   std::views::take_while([](int i) { return i <= 200; }) |
                   std::views::transform([](int i) { return i * i; });

    /*
    auto results = std::views::iota(100) |
                   std::views::take_while([](int i) { return i <= 200; }) |
                   std::views::transform([](int i) { return i * i; }) |
                   std::views::common;
    */

    auto sum = std::accumulate(results.begin(), results.end(), 0);

    std::cout << "sum: " << sum << '\n';

    std::cout << '\n';
}
```
```

The ranges library provides only pendants to the algorithms of the algorithm³ and the memory⁴ library, but not to the algorithms of the numeric⁵ library. Consequently, I use `std::accumulate` from the numeric library, to sum up all squares (line 24). The compilation of the program fails with a cryptic error message:

+   3. https://en.cppreference.com/w/cpp/header/algorithm
+   4. https://en.cppreference.com/w/cpp/header/memory
+   5. https://en.cppreference.com/w/cpp/numeric