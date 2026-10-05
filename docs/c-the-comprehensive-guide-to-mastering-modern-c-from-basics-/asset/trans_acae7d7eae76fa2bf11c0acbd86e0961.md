
我声明 `v` 是一个可以包含 `int` 类型值或 `float` 类型值的变体。然后我给 `v` 赋值为 `int` 的 12，我通过 `get<int>` 读取并输出了它。接着又赋值了另一个值，但这次是一个 `float`。我也读取并输出了这个值。`v` 连续包含了一个 `int`，然后包含了一个 `float`。

你不能用 `get` 请求一个 `variant` 未知的类型。`get<double>` 无法编译。

在运行时，如果你查询一个 `variant` 当前未包含的有效类型，将会得到一个错误。你会收到 `bad_variant_access` 异常。

在不使用异常的情况下，你可以用 `holds_alternative<int>(w)` 检查状态。在这里你会得到一个布尔值，指示 `w` 是否持有 `int`。

如果你想对 `variant` 的内容做出反应，可以使用 `index` 查询当前是哪一个类型。然而，更优雅的方法是使用 `visit`，向它传递一个可以处理不同类型的访问者（visitor）。

```
// https://godbolt.org/z/G4zY5E6P
#include <variant>
#include <iostream>
using std::cout;
struct TypeGreeting {
    void operator()(int) const { cout << "Hello int"; }
    void operator()(float) const { cout << "Hello float"; }
};
int main() {
    std::variant<int, float> var;
    var = 12; // 状态 int
    std::visit([](auto a) { cout << a; }, var); // 泛型 lambda
    cout << std::endl;
    var = 3.456f; // 状态 float
    std::visit(TypeGreeting{}, var); // 带重载的函数对象
cout << std::endl;
}
```

**Listing 28.47** 使用访问者检查“variant”。

在第一次 `visit` 中，lambda 是泛型的，并接受任何可以输出到流的参数。

第二次使用 `visit` 取一个函数对象作为参数，该对象对两种可能的类型都有特定的重载。针对 `int` 和 `float` 的 `operator()` 方法可以包含完全不同的实现。

# 28.10 “any” 存储任意类型

如果你对在声明 `variant` 时必须指定所有可能的类型感到不满，那么或许 `any` 适合你。你可以在其中存储任何类型的值。并且你只能通过类型来检索它。如果你尝试使用不同的类型，将会得到异常。然而，你可以分配任何新值以及新类型：

```
// https://cppbolt.org/z/leco9Wcr3
#include <any>
#include <iostream>
#include <vector>
#include <string>
int main() {
std::any a = 5;
std::cout << std::any_cast<int>(a) << '\n';
a = 3.456;
std::cout << std::any_cast<double>(a) << '\n';
using namespace std::literals;
std::vector<std::any> data { 4, 8.976, "Geronimo" };
std::cout << std::any_cast<double>(data[1]) << '\n';
std::cout << data[1].type() << '\n';
}
```

你看到我首先赋值了一个 `int`，然后是一个 `double`。在这里我没有使用 `get`，而是使用 `any_cast` 来检索值，这是一种略有不同的机制。然而，如果你请求错误的类型，将会得到异常。

你也可以将 `any` 放入容器中。`data` 中的三个 `any` 元素在初始化后具有不同的类型。为了信息，你也可以 `type()` 访问当前存储的类型。然而，这更多是为了调试，不是可移植的信息。

注意以下几点：

- `any` 不是模板类。
- 你通过带有或不带值的构造函数或 `make_any` 创建 `any`。
- 你用 `has_value()` 检查 `any` 是否为空。
- 你通过赋值、`emplace`、`reset` 或 `swap` 改变值。
- 你通过 `any_cast<T>` 安全地检索值类型。
- 没有无异常的检查方法来查看 `any` 当前是否包含特定类型。如果你需要这个，请考虑 `variant`。

# 28.11 特殊数学函数

你们中的数学家和物理学家会很高兴，因为标准库已经包含了一些（真的）非常特殊的数学函数，所以你不需要使用第三方库。大多数函数作用于 `float`、`double` 和 `long double`。有时会有多个名称变体；我只提到一个。这些函数位于 `<cmath>` 头文件中。

- laguerre, assoc_laguerre, legendre, assoc_legendre, hermite
  计算（关联）Laguerre 多项式、（关联）Legendre 多项式（球面函数）和 Hermite 多项式。

- beta, expint
  计算 Euler beta 函数和指数积分函数。

- comp_ellint_1, comp_ellint_2, comp_ellint_3, ellint_1, ellint_2, ellint_3
  计算第一、第二、第三类完全或不完全椭圆积分。

- cyl_bessel_i, cyl_bessel_j, cyl_bessel_k, sph_bessel, sph_legendre, sph_neumann
  正则、非正则和不规则修正的圆柱贝塞尔函数，以及球面贝塞尔函数、勒让函数和内曼函数。

- cyl_neumann
  圆柱内曼函数，也称为第二类贝塞尔函数。

- riemann_zeta
  计算 Riemann $\zeta$ 函数，这可能与质数有关。

# # C++20: 数学常数

从 C++20 开始，你可以访问最有趣的数学常数。在 `<numbers>` 头文件中，定义了以下 `inline constexpr`：e, log2, pi, inv_pi, ln2, ln10, sqrt2, sqrt3, egamma 和 phi。如果你想要这些常数的一个 `float` 或 `long double` 值，在名称后面加上 `v`。

# 28.12 使用 <charconv> 进行快速转换

有许多方法可以将字符串（或 `char*`）转换为数字。在 C++17 中有了另一种选择：来自 `<charconv>` 头文件的 `from_chars`。`from_chars` 的主要重点是性能，因为随着进制分隔符和编码（UTF-16 等）的发展，这变得越来越重要。将字符串转换为 `int` 的现有方法包括：

- scanf
  来自 C；灵活，与 `printf` 相关。
- atol, atoi, atoll
  来自 C；没有方法确定结束或成功。
- strtol, strtof, strtod, strtold, strtol, strtoull
  良好的候选；错误检查尚可，但缺乏溢出检查。
- stringstream
  C++11；灵活，但慢，且缺少溢出检查。
- stol, stoi, stoll, stof, stod
  C；缺少起始位置，通过异常处理。

而且由于 C++17 允许结构化绑定：

```cpp
auto [p, errc] = std::from_chars(begin, end);
```

类型可以是任何整数或浮点类型。`from_chars` 的结果读取到 `value`。因此，变量必须提前声明。返回结果包含 `const char* ptr`。`from_chars` 不处理前空格。这些必须跳过：

```cpp
from_chars(const char* first, char* last, T& value, int base = 10);
```

`from_chars` 返回一个包含 `const char* ptr` 和 `errc` 的结构体。`ptr` 指示读取了多少内容，`errc` 显示潜在的错误。`from_chars` 不处理前导空格。

```cpp
// https://cppbolt.org/z/11n7xcs
#include <charconv>
#include <vector>
#include <iostream>
#include <string>
std::vector<size_t> num_to_vec(const std::string& nums) {
    std::vector<size_t> result;
    // 无末尾空格
    auto end = nums.data() + nums.find_last_of(' ') + 1;
    const char* str = nullptr; // 循环指针
    auto last = nums.data(); // 未翻译字符
    size_t n; // 转换数字
    do {
    for(st = last; (st<end) && *(st==' '); ++st); // 跳过 ' '
    if (last = std::from_chars(st, end, n).ptr; last != st)
    result.push_back(n); // 存储结果
    while (last != st)
    return result;
}

void errorDemo(const char* buf, size_t sz) {
    int n;
    auto [p, ec] = std::from_chars(buf, buf+sz, n);
    if (ec != std::errc()) {
        const auto error = std::error_code(ec);
        std::cout << error.message() << "\n";
    }
}

int main() {
    auto result = num_to_vec("12 33 43");
    for(auto r : result) std::cout << r << " ";
    // 输出: 12 33 43
    errorDemo("XYZ", 4);
    // 输出: Invalid argument
    errorDemo("12312312323", 16);
    // 输出: Numerical result out of range
}
```

