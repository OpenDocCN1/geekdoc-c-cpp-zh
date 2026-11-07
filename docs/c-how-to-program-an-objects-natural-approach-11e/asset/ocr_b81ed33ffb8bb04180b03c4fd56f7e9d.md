```
```cpp
// Fig14_14.cpp
// Demonstrating algorithms gcd, lcm, iota, reduce and partial_sum.
#include <array>
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <numeric>

int main() {
    std::ostream_iterator<int> output{std::cout, " "};

    // calculate the greatest common divisor of two integers
    std::cout << "std::gcd(75, 20): " << std::gcd(75, 20)
              << "\nstd::gcd(17, 13): " << std::gcd(17, 13);
}
```
```

```
```
std::gcd(75, 20): 5
std::gcd(17, 13): 1
```
```

**Fig. 14.14** | Demonstrating algorithms gcd, lcm, iota, reduce and partial_sum.

# ### lcm Algorithm

The lcm algorithm (lines 18 and 19) receives two integer arguments and returns their least common multiple.

```
```cpp
// calculate the least common multiple of two integers
std::cout << "\nstd::lcm(3, 5): " << std::lcm(3, 5)
          << "\nstd::lcm(12, 9): " << std::lcm(12, 9);
```
```

```
```
std::lcm(3, 5): 15
std::lcm(12, 9): 36
```
```

# ### iota Algorithm

The iota algorithm (line 23) fills a common range with a sequence of values starting with the value in the third argument. The first two arguments must be forward iterators representing a common range to fill. The last argument's type must support the ++ operator.

```
```cpp
// fill an array with integers using the std::iota algorithm
std::array<int, 5> ints{};
std::iota(ints.begin(), ints.end(), 1);
std::cout << "\nints: ";
std::ranges::copy(ints, output);
```
```

```
```
ints: 1 2 3 4 5
```
```