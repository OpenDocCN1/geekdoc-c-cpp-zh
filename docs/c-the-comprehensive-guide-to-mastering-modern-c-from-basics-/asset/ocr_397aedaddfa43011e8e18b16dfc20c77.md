# Exception: Algorithms on Numbers

Three functions in <numeric> do not match the pattern as they work on exactly two values and not on iterators:

+   - gcd(n, m)
Returns the greatest common divisor (gcd) of two numbers.

+   - lcm(n, m)
Returns the least common multiple (lcm) of two numbers.

+   - midpoint(n, m)
Determines the midpoint (rounded to n) between n and m starting from C++20. No overflow occurs, which could happen with (n+m)/2, for example. Also works on pointers. For linear interpolation with floating-point numbers, use lerp from <cmath>.

All these functions are constexpr and thus fast with numeric literals. Therefore, they are well-suited for initializing constants.

Consider the following examples.

```
// https://cppbolt.org/z/Y7GPcGwM8
#include <numeric> // accumulate
#include <functional> // multiplies
#include <algorithm> // transform, fold_left
#include <iostream>
#include <vector>
using std::accumulate; using std::cout; using std::vector;
using std::multiplies;
namespace rs = std::ranges;
int main() {
 vector data{2, 3, 5, 10, 20 };
```