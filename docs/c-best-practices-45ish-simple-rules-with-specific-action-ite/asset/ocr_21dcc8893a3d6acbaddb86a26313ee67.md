# Concepts in requires clause.

```
#include <stdexcept>
#include <type_traits>
#include <utility>
```

```
// overload resolution will pick the most specific version
template <typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator) requires
(std::integral_v<Numerator> && std::integral_v<Denominator>) {
// is integral division
if (denominator == 0) {
    throw std::runtime_error("divide by 0!");
}
return numerator / denominator;
}
```

```
template <typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator) {
return numerator / denominator;
}
```

This version uses concepts as function parameters. C++20 even has an “auto concept,” which is an implicit template function.

Terse concepts requirement syntax.

```
#include <stdexcept>
#include <concepts>
```

```
auto divide(std::integral auto numerator,
  std::integral auto denominator) {
// is integer division
if (denominator == 0) {
    throw std::runtime_error("divide by 0!");
}
```