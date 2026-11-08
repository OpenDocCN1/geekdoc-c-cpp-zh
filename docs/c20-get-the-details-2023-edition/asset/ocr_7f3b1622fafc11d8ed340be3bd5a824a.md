```
```cpp
int main()
{
    double x = -3.5;
    unsigned int y = 7;
    bool yes = x < static_cast<double>(y);
}
```
```

# Floating point promotion to double

Additionally, the function `std::in_range<R>(t)` returns true if `t` can be represented in the type `R`. `std::in_range` returns false if `t` is greater than or equal to the minimum value and less than or equal to the maximum value of type `R`.

The following code snippet shows a possible implementation from [cppreference.com/std::in_range](https://en.cppreference.com/w/cpp/utility/in_range).

Possible implementation of `std::in_range`

```
```cpp
template<class R, class T>
constexpr bool in_range(T t) noexcept {
    return std::cmp_greater_equal(t, std::numeric_limits<R>::min()) &&
           std::cmp_less_equal(t, std::numeric_limits<R>::max());
}
```
```

# 5.4.2 Mathematical Constants

First of all, the constants need the header `<numbers>` and the namespace `std::numbers`. The following table gives you an overview.

**The mathematical constants**

| Mathematical Constant | Description |
|---|---|
| `std::numbers::e` | *e* |
| `std::numbers::log2e` | `log₂ e` |
| `std::numbers::log10e` | `log₁₀ e` |
| `std::numbers::pi` | `π` |
| `std::numbers::inv_pi` | `1/π` |
| `std::numbers::inv_sqrtpi` | `1/√π` |
| `std::numbers::ln2` | `ln 2` |

[^34]: https://en.cppreference.com/w/cpp/utility/in_range