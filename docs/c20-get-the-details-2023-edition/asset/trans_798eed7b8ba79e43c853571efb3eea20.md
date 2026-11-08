

### 整数的不安全比较已解决

```cpp
// unsafeComparison2.cpp

int main() {
    int x = -3;
    unsigned int y = 7;

    bool val = x < y;
    static_assert(static_cast<unsigned int>(-3) == 4'294'967'293);
}
```

在示例中，我重点关注小于运算符。C++ Insights^11 给了我以下输出：

```cpp
int main()
{
    int x = -3;
    unsigned int y = 7;
    bool val = static_cast<unsigned int>(x) < y;
    /* PASSED: static_assert(static_cast<long>(static_cast<unsigned int>(-3)) == 4294967293L); */
}
```

### 不安全比较分析

以下是正在发生的事情：

- 编译器将表达式 x < y（第 7 行）转换为 static_cast<unsigned int>(x) < y。特别是，有符号的 x 被转换为 unsigned int。
- 由于这次转换，-3 变成 4'294'967'293。
- 4'294'967'293 等于 -3 mod 2^32。
- 在 C++ Insights 上，32 是 unsigned int 的位数。

得益于 C++20，我们有了安全的整数比较。

### 5.4.1.2 整数安全比较

C++20 为整数支持六个比较函数：

### 六个安全比较函数

| 比较函数 | 含义 |
|---|---|
| `std::cmp_equal` | `==` |
| `std::cmp_not_equal` | `!=` |
| `std::cmp_less` | `<` |
| `std::cmp_less_equal` | `<=` |
| `std::cmp_greater` | `>` |
| `std::cmp_greater_equal` | `>=` |

得益于这六个比较函数，我可以轻松地将之前的程序 unsafeComparison.cpp 转换为程序 safeComparison.cpp。新的比较函数需要头文件 `<utility>`。

### 整数的安全比较

```cpp
// safeComparison.cpp

#include <iostream>
#include <utility>

int main() {

    std::cout << '\n';

    std::cout << std::boolalpha;

    int x = -3;
    unsigned int y = 7;

    std::cout << " -3 == 7: " << std::cmp_equal(x, y) << '\n';
    std::cout << " -3 != 7: " << std::cmp_not_equal(x, y) << '\n';
    std::cout << " -3 < 7: " << std::cmp_less(x, y) << '\n';
    std::cout << " -3 <= 7: " << std::cmp_less_equal(x, y) << '\n';
    std::cout << " -3 > 7: " << std::cmp_greater(x, y) << '\n';
    std::cout << " -3 >= 7: " << std::cmp_greater_equal(x, y) << '\n';

    std::cout << '\n';

}
```

此外，我还应用了相等和不相等运算符。

![](img/c60a87adb7f61e2e82071d081bbb389a_337_0.png)

用非整数（例如 double）调用安全比较函数会导致编译期错误。

### unsigned int 与 double 的安全比较

```cpp
// safeComparison.cpp

#include <iostream>
#include <utility>

int main() {

    double x = -3.5;
    unsigned int y = 7;

    std::cout << "-3.5 < 7: " << std::cmp_less(x, y);  // ERROR
}
```

另一方面，你可以用传统方式比较 double 和 unsigned int。程序 `classicalComparison.cpp` 对 double 和 unsigned int 应用传统比较。

### unsigned int 与 double 的传统比较

```cpp
// classicalComparison.cpp

int main() {

    double x = -3.5;
    unsigned int y = 7;

    auto res = x < y;    // true
}
```

这样可行。unsigned int 会被浮点提升[^32]为 double。C++ Insights[^33] 展示了真相：

[^32]: https://en.cppreference.com/w/cpp/language/implicit_conversion  
[^33]: https://cppinsights.io/s/44216566

```cpp
int main()
{
    double x = -3.5;
    unsigned int y = 7;
    bool yes = x < static_cast<double>(y);
}
```

### 浮点提升为 double

此外，函数 `std::in_range<R>(t)` 在 `t` 可以用类型 `R` 表示时返回 true。`std::in_range` 在 `t` 大于或等于类型 `R` 的最小值且小于或等于类型 `R` 的最大值时返回 true。

以下代码片段展示了来自 [cppreference.com/std::in_range](https://en.cppreference.com/w/cpp/utility/in_range) 的一种可能实现。

### `std::in_range` 的可能实现

```cpp
template<class R, class T>
constexpr bool in_range(T t) noexcept {
    return std::cmp_greater_equal(t, std::numeric_limits<R>::min()) &&
           std::cmp_less_equal(t, std::numeric_limits<R>::max());
}
```

[^34]: https://en.cppreference.com/w/cpp/utility/in_range

## 5.4.2 数学常量

首先，这些常量需要头文件 `<numbers>` 和命名空间 `std::numbers`。下表为你提供概览。

### 数学常量

| 数学常量 | 描述 |
|---|---|
| `std::numbers::e` | *e* |
| `std::numbers::log2e` | `log₂ e` |
| `std::numbers::log10e` | `log₁₀ e` |
| `std::numbers::pi` | `π` |
| `std::numbers::inv_pi` | `1/π` |
| `std::numbers::inv_sqrtpi` | `1/√π` |
| `std::numbers::ln2` | `ln 2` |

```cpp
    std::cout << '\n';
    }
```

以下是使用 MSVC 编译器时程序的输出。

![](img/c60a87adb7f61e2e82071d081bbb389a_340_0.png)

使用所有数学常量

数学常量可用于 float、double 和 long double。默认使用 double，但你也可以指定 float（`std::numbers::pi_v<float>`）或 long double（`std::numbers::pi_v<long double>`）。

## 5.4.3 中点和线性插值

- `std::midpoint(a, b)`：计算整数、浮点数或指针的中点 `(a + (b - a) / 2)`。如果 a 和 b 是指针，它们必须指向同一个数组对象。该函数需要头文件 `<numeric>`。
- `std::lerp(a, b, t)`：计算线性插值 `(a + t(b - a))`。当 t 超出范围 `[0, 1]` 时，它计算线性外插。该函数需要头文件 `<cmath>`。

程序 midpointLerp.cpp 应用了这两个函数。

### 计算数字的中点和线性插值

```cpp
// midpointLerp.cpp

#include <cmath>
#include <numeric>
#include <iostream>

int main() {

    std::cout << '\n';

    std::cout << "std::midpoint(10, 20): " << std::midpoint(10, 20) << '\n';

    std::cout << '\n';

    for (auto v: {0.0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0}) {
        std::cout << "std::lerp(10, 20, " << v << "): " << std::lerp(10, 20, v)
                  << '\n';
    }

    std::cout << '\n';
}
```

该程序连同其输出应该不言自明。

```text
std::midpoint(10, 20): 15

std::lerp(10, 20, 0): 10
std::lerp(10, 20, 0.1): 11
std::lerp(10, 20, 0.2): 12
std::lerp(10, 20, 0.3): 13
std::lerp(10, 20, 0.4): 14
std::lerp(10, 20, 0.5): 15
std::lerp(10, 20, 0.6): 16
std::lerp(10, 20, 0.7): 17
std::lerp(10, 20, 0.8): 18
std::lerp(10, 20, 0.9): 19
std::lerp(10, 20, 1): 20
```

计算数字的中点和线性插值

与使用表达式 `(first + second) / 2` 朴素地计算两个数 first 和 second 的中点相比，`std::midpoint(first, second)` 会自动处理溢出错误。

### 无溢出地计算两个大数的中点

```cpp
// midpoint.cpp

#include <limits>
#include <numeric>
#include <iostream>

int main() {

    std::cout << '\n';

    int first = std::numeric_limits<int>::max();
    int second = std::numeric_limits<int>::max() - 2;

    std::cout << "first: " << first << '\n';
    std::cout << "second: " << second << '\n';

    std::cout << '\n';

    std::cout << "(first + second) / 2: " << (first + second) / 2 << '\n';
    std::cout << "std::midpoint(first, second): " << std::midpoint(first, second) << '\n';

    std::cout << '\n';

}
```

计算 `(first + second) / 2`（第 19 行）会导致溢出，因为变量 `first`（第 19 行）是类型 `int` 的最大可能值，而变量 `second`（第 20 行）与之非常接近。相反，`std::midpoint(first, second)`（第 20 行）返回正确值。

![](img/c60a87adb7f61e2e82071d081bbb389a_342_0.png)

无溢出地计算两个大数的中点

## 5.4.4 位操作

头文件 `<bit>` 支持各种 `constexpr` 函数，用于访问和操作单个位或位序列。

### 5.4.4.1 `std::endian`

得益于新类型 `std::endian`，你可以获得标量类型的字节序。字节序可以是大端序或小端序。大端序意味着最高有效字节在最左边，小端序意味着最低有效字节在最左边。标量类型要么是算术类型、枚举、指针、成员指针，要么是 `std::nullptr_t`。

类 `endian` 提供所有标量类型的字节序：

```cpp
enum class endian
{
    little = /*implementation-defined*/,
    big    = /*implementation-defined*/,
    native = /*implementation-defined*/
};
```

- 如果所有标量类型都是小端序，则 `std::endian::native` 等于 `std::endian::little`。
- 如果所有标量类型都是大端序，则 `std::endian::native` 等于 `std::endian::big`。

甚至边界情况也受支持：

- 如果所有标量类型的 `sizeof` 都为 1，因此字节序无关紧要，则枚举值 `std::endian::little`、`std::endian::big` 和 `std::endian::native` 相同。
- 如果平台使用混合字节序，则 `std::endian::native` 既不等于 `std::endian::big`，也不等于 `std::endian::little`。

当我在 x86 架构上运行以下程序 `getEndianness.cpp` 时，我得到答案 `little-endian`。

```cpp
// getEndianness.cpp

#include <bit>
#include <iostream>

int main() {

    if constexpr (std::endian::native == std::endian::big) {
        std::cout << "big-endian" << '\n';
