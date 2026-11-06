# 27. Prefer if constexpr over SFINAE

SFINAE is kind-of write-only code. if constexpr doesn’t have the same flexibility, but use it when you can.

Let’s take our previous example:

*C++14 divides template.*

```
template <typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator)
{
    return numerator / denominator;
}
```

We now want to add different behavior if we are doing integral division. Before C++17, we would have used SFINAE ("Substitution Failure Is Not An Error"). Essentially this means that if a function fails to compile, then it is removed from overload resolution.

*SFINAE divide function.*

```
#include <stdexcept>
#include <type_traits>
#include <utility>

template <typename Numerator, typename Denominator,
          std::enable_if_t<std::is_integral_v<Numerator> &&
                           std::is_integral_v<Denominator>,
                           int> = 0>
auto divide(Numerator numerator, Denominator denominator) {
    // is integer division
```