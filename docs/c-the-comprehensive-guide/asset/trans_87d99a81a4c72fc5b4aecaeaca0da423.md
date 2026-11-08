
一个 variant 可以取若干类型之一的值。设置某一种类型的值会改变 variant 的状态，因此随后尝试从中读取另一种类型就会失败。因此，它的使用是安全的。

```cpp
// https://godbolt.org/z/baY7Tz91f
#include <variant>
using std::get;
int main() {
    std::variant<int, float> v{};
    v = 12;                  // State changes to int
    auto i = get<int>(v);    // retrieves the int
    std::cout << i << '\n';  // Output: 12
    v = 3.456f;              // State changes to float
    std::cout << get<float>(v) << '\n';  // Output: 3.456
    get<double>(v);          // Error
    get<3>(v);               // Error
    std::variant<int, float> w{};
    w = get<float>(v);       // Access by type
    w = get<1>(v);           // Access is also possible via index
    w = v;                   // entire assignment is also possible
    try {
        get<int>(w);         // triggers exception
    } catch (std::bad_variant_access&) { /* ... */ }
}
```

**列表 28.46** “variant” 的基本功能

这里我把 `v` 声明为一个 variant，它可以包含 `int` 类型的值或 `float` 类型的值。然后我赋给 `v` 一个 `int` 值 `12`，随后用 `get<int>` 读取并输出它。接着我又赋了一个值，但这次是 `float` 类型。我也读取并输出了这个值。这样，`v` 先后依次包含了一个 `int` 和一个 `float`。

你不能用 `get` 请求 variant 不知道的类型。`get<double>` 无法编译。

在运行时，如果你查询 variant 当前未包含的有效类型，就会出错。你会收到 `bad_variant_access` 异常。

在未抛异常的情况下，你可以用 `holds_alternative<int>(w)` 检查状态。这里你会得到一个布尔值，表示 `w` 当前是否持有 `int`。

如果你想对 variant 的内容作出响应，可以用 `index` 查询当前是哪个类型。不过，使用 `visit` 更优雅，你向它传入一个能够处理不同类型的访问器。

```cpp
// https://godbolt.org/z/G4z8Y5E6P
#include <variant>
#include <iostream>
using std::cout;
struct TypeGreeting {
    void operator()(int) const { cout << "Hello int"; }
    void operator()(float) const { cout << "Hello float"; }
};
int main() {
    std::variant<int, float> var{};
    var = 12;                           // State int
    std::visit([](auto a) { cout << a; }, var); // generic lambda
    cout << std::endl;
    var = 3.456f;                       // State float
    std::visit(TypeGreeting(), var);    // Functor with overloads
    cout << std::endl;
}
```

**列表 28.47** 使用访问器检查 “variant”。

在第一次 `visit` 中，lambda 是泛型的，接受任何可以输出到流的参数。

第二次使用 `visit` 时，以一个函数对象作为参数，该函数对象对两种可能的类型都有具体的重载。针对 `int` 和 `float` 的 `operator()` 方法可以包含完全不同的实现。

### 28.10 “any” 可以持有任意类型

如果你不喜欢在声明 variant 时必须指定可能的类型，那么 any 可能适合你。你可以在其中存储任意类型的值。而且你只能取回该类型。如果你尝试用不同的类型，就会得到异常。不过，你可以给 any 赋予一个新值，也可以赋予一个新类型：

```cpp
// https://godbolt.org/z/eco9Wcr3
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
    std::vector<std::any> data { 4, 8.976, "Geronimo"s };
    std::cout << std::any_cast<double>( data[1] ) << '\n';
    std::cout << data[1].type().name() << '\n';
}
```

你可以看到我先赋了一个 `int`，然后又赋了一个 `double`。这里不是使用 `get`，而是使用 `any_cast` 来取回值，这是一种略有不同的机制。然而，如果你请求了错误的类型，就会得到异常。

你也可以将 any 装入容器中。`data` 中的三个 any 元素在初始化后具有不同的类型。此外，你还可以用 `type()` 访问当前存储的类型。不过，这更多是用于调试，并不是可移植的信息。

请注意以下几点：

- any 不是模板类。
- 你可以通过带值或不带值的构造函数或 `make_any` 创建 any。
- 你可以使用 `has_value()` 检查 any 是否为空。
- 你可以通过赋值、`emplace`、`reset` 或 `swap` 更改值。
- 你可以使用 `any_cast<T>` 以类型安全的方式取回值。
- 没有无异常方式检查 any 当前是否包含特定类型。如果你需要这种能力，请考虑使用 variant。

### 28.11 特殊数学函数

你们中的数学家和物理学家会很高兴地发现，标准库已经包含一些（确实）非常特殊的数学函数，因此无需使用第三方库。大多数函数支持 `float`、`double` 和 `long double`。有时存在多个名称变体；我只提其中一个。这些函数位于 `<cmath>` 头文件中。

- **laguerre、assoc_laguerre、legendre、assoc_legendre、hermite**  
  计算（关联）拉盖尔多项式、（关联）勒让德多项式（球函数）和埃尔米特多项式。
- **beta、expint**  
  计算欧拉 beta 函数和指数积分函数。
- **comp_ellint_1、comp_ellint_2、comp_ellint_3、ellint_1、ellint_2、ellint_3**  
  计算第一类、第二类和第三类的完全或不完全椭圆积分。
- **cyl_bessel_i、cyl_bessel_j、cyl_bessel_k、sph_bessel、sph_legendre、sph_neumann**  
  常规、非常规和不规则修正的圆柱贝塞尔函数，以及球贝塞尔函数、勒让德函数和诺伊曼函数。
- **cyl_neumann**  
  圆柱诺伊曼函数，也称为第二类贝塞尔函数。
- **riemann_zeta**  
  计算黎曼-ζ 函数，你可能会在质数相关的问题中用到它。

> **C++20：数学常量**
>
> 从 C++20 开始，你可以使用最有趣的数学常量。
> 在 `<numbers>` 头文件中，`std::numbers` 命名空间内定义了以下内联 `constexpr double` 常量：`e`、`log2e`、`log10e`、`pi`、`inv_pi`、`inv_sqrtpi`、`ln2`、`ln10`、`sqrt2`、`sqrt3`、`inv_sqrt3`、`egamma` 和 `phi`。
>
> 如果你想要其中某个常量的 `float` 或 `long double` 值，请在名称后面加上 `_v` 后缀以获得模板——例如：
>
> `pi_v<long double>`

### 28.12 使用 «charconv» 快速转换

将字符串（或 char*）转换为数字的方法有很多。使用 C++17，还有另一个选项：来自 `<charconv>` 头文件的 `from_chars`。`from_chars` 的主要关注点是性能，随着 XML 和 JSON 应用越来越多，这一点变得越来越重要。

`from_chars` 与转换函数 `to_chars` 一起提供，用于将数字转换为字符串。

`from_chars` 在以下情况下能展现优势：你有一个 char*，已经知道需要解析一个数字，并且不涉及区域设置（不同的小数点符号和千位分隔符）和编码（UTF-16 等）。

现有的将字符串转换为 `int` 或类似类型的方法包括：

- **sscanf**  
  来自 C；灵活，与 `printf` 相关。
- **atol、atoi、atoll、atof**  
  来自 C；无法确定解析的结束位置或是否成功。
- **strtol、strtof、strtod、strtold、strtoll、strtoull**  
  不错的候选；错误检查尚可，但缺少溢出和下溢检查。
- **stringstream**  
  C++；灵活但慢，也缺少溢出和下溢检查。
- **stol、stoi、stoll、stoull、stof、stod、stold**  
  C++11；缺少灵活的起始位置，通过异常进行错误处理。

而自 C++17 起，这一系列方法中还有：

```cpp
from_chars_result
    from_chars(const char* first, const char* last, T& value, int base = 10);
```

类型 `T` 可以是任意整数或浮点类型。结果会被读入输出参数 `value` 中。因此，变量必须事先声明。

返回值是一个包含 `const char* ptr` 和 `errc` 成员的结构体。`ptr` 指示读取了多少内容，`errc` 显示任何潜在错误。好在 C++17 还允许结构化绑定：

```cpp
auto [p, ec] = std::from_chars(pbegin, pend, value);
```

然而，`from_chars` 不会处理前导空白字符。这些空白必须事先跳过：

```cpp
// https://godbolt.org/z/115nE7xsc
#include <charconv>
#include <vector>
#include <iostream>
#include <string>

std::vector<size_t> nums_to_vec(const std::string& nums) {
    std::vector<size_t> result {};
    // without trailing spaces
    const auto end = nums.data() + nums.find_last_not_of(' ') + 1;
    const char* st = nullptr;  // loop pointer
    auto last = nums.data();   // last untranslated character
    size_t n;                  // converted number
    do {
        for(st = last; (st<end)&&( *st==' ' ); ++st); // skip ' '
        if (last = std::from_chars(st, end, n).ptr; last != st)
            result.push_back(n);                      // store number
    } while (last != st);
    return result;
}

void errorDemo(const char* buf, size_t sz) {
    int n;
    auto [p, ec] = std::from_chars(buf, buf+sz, n);
    if (ec != std::errc{}) {
        const auto error = std::make_error_code(ec);
        std::cout << error.message() << '\n';
    }
}
```
