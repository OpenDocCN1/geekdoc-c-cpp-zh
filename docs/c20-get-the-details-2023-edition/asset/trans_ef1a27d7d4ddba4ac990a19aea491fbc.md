
- 精度：可以使用句点（.）后跟一个非负十进制数或替换字段。

几个示例应有助于你掌握基础知识：

### 应用宽度和精度说明符

```cpp
// formatWidthPrecision.cpp

#include <format>
#include <iostream>
#include <string>

int main() {

    int i = 123456789;
    double d = 123.456789;

    std::cout << "---" << std::format("{}", i) << "---\n";
    std::cout << "---" << std::format("{:15}", i) << "---\n"; // (w = 15)
    std::cout << "---" << std::format("{:{}}", i, 15) << "---\n"; // (w = 15)

    std::cout << '\n';

    std::cout << "---" << std::format("{}", d) << "---\n";
    std::cout << "---" << std::format("{:15}", d) << "---\n"; // (w = 15)
    std::cout << "---" << std::format("{:{}}", d, 15) << "---\n"; // (w = 15)

    std::cout << '\n';

    std::string s = "Only a test";

    std::cout << "---" << std::format("{:10.50}", d) << "---\n"; // (w = 10, p = 50)
    std::cout << "---" << std::format("{:{}.{}}", d, 10, 50) << "---\n"; // (w = 10, p = 50)
    std::cout << "---" << std::format("{:10.5}", d) << "---\n";  // (w = 10, p = 5)
    std::cout << "---" << std::format("{:{}.{}}", d, 10, 5) << "---\n"; // (w = 10, p = 5)

    std::cout << '\n';

    std::cout << "---" << std::format("{:.500}", s) << "---\n";    // (p = 500)
    std::cout << "---" << std::format("{:.{}}", s, 500) << "---\n"; // (p = 500)
    std::cout << "---" << std::format("{:.5}", s) << "---\n";      // (p = 5)

}
```

源代码中的 w 字符表示宽度；类似地，p 字符表示精度。关于这个程序，我有一些有趣的观察。使用替换字段指定宽度时不会添加额外空格（第 14 行）。当指定的精度高于所显示 double 的长度时（第 26 和 27 行），所显示值的长度会反映该精度。这一观察不适用于字符串（第 35 和 36 行）。

![](img/c60a87adb7f61e2e82071d081bbb389a_359_0.png)

应用宽度和精度说明符

此外，你还可以参数化宽度和精度。

### 应用参数化的宽度和精度说明符

```cpp
// formatWidthPrecisionParameterized.cpp

#include <format>
#include <iostream>

int main() {

    std::cout << '\n';

    double doub = 123.456789;

    std::cout << std::format("{}\n", doub);

    std::cout << '\n';

    for (auto precision: {3, 5, 7, 9}) {
        std::cout << std::format("{:.{}f}\n", doub, precision);
    }

    std::cout << '\n';

    int width = 10;
    for (auto precision: {3, 5, 7, 9}) {
        std::cout << std::format("{:{}.{}f}\n", doub, width, precision);
    }

    std::cout << '\n';

}
```

程序 `formatWidthPrecisionParameterized.cpp` 以多种方式显示 double 变量 `doub`。第 12 行应用默认设置。第 17 行将精度从 3 变化到 9。格式字符串的最后一个参数进入格式说明符 `{:{}.{}f}` 的内层 `{}`。最后，第 24 行将所显示 double 的宽度设置为 10。

![](img/c60a87adb7f61e2e82071d081bbb389a_360_0.png)

应用参数化的宽度和精度说明符

### 5.5.2.3.4 类型

一般来说，编译器会推导所使用值的类型。但有时，你希望指定类型。以下是最重要的类型说明符：

- 字符串：`s`
- 整数：
  - `b`：二进制格式
  - `B`：与 `b` 相同，但基数前缀为 `0B`
  - `d`：十进制格式
  - `o`：八进制格式
  - `x`：十六进制格式
  - `X`：与 `x` 相同，但基数前缀为 `0X`
- `char` 和 `wchar_t`：
  - `b`、`B`、`d`、`o`、`x`、`X`：与整数类似
- `bool`：
  - `s`：`true` 或 `false`
  - `b`、`B`、`d`、`o`、`x`、`X`：与整数类似
- 浮点数：
  - `e`：指数格式
  - `E`：与 `e` 相同，但指数用 `E` 表示
  - `f`、`F`：定点格式；精度为 6
  - `g`、`G`：精度为 6，但指数用 `E` 表示
- 指针：
  - `p`：其地址的十六进制表示法

只有 `void*`、`const void*` 和 `std::nullptr_t` 指针类型是有效的。如果你想显示任意指针的地址，必须将其转换为 `(const) void*`。

#### 指针的输出

```cpp
double d = 123.456789;

std::format("{}", &d);                          // ERROR
std::format("{}", static_cast<void*>(&d));      // okay
std::format("{}", static_cast<const void*>(&d));// okay
std::format("{}", nullptr);                     // okay
```

当你未指定类型时，值的显示方式如下。字符串按字符串显示，整数按十进制格式显示，字符按字符显示，浮点值使用 `std::to_chars`[^32] 显示。

类型说明符让你可以轻松地以不同进制显示 `int`。

[^32]: https://en.cppreference.com/w/cpp/utility/to_chars

#### 应用类型说明符

```cpp
// formatType.cpp

#include <format>
#include <iostream>

int main() {

    int num{2020};

    std::cout << "default:    " << std::format("{}", num) << '\n';
    std::cout << "decimal:    " << std::format("{:d}", num) << '\n';
    std::cout << "binary:     " << std::format("{:b}", num) << '\n';
    std::cout << "octal:      " << std::format("{:o}", num) << '\n';
    std::cout << "hexadecimal: " << std::format("{:x}", num) << '\n';

}
```

![](img/c60a87adb7f61e2e82071d081bbb389a_362_0.png)

到目前为止，我已经格式化了基本类型和字符串。此外，你还可以格式化用户定义类型。

### 5.5.3 用户定义类型

我必须为用户定义类型特化类 `std::formatter`[^43]。特别地，我必须实现成员函数 `parse` 和 `format`。

- **parse**：此函数解析格式字符串，并在出错时抛出 `std::format_error`。函数 `parse` 应为 `constexpr`，以支持编译期解析。它接受一个解析上下文（`std::format_parse_context`），并应返回格式说明符的最后一个字符（即闭合的 `}`）。当你未使用格式说明符时，这也是格式说明符的第一个字符。

  以下几行展示了格式说明符第一个字符的几个示例：

  ```text
  "{}"      // context.begin() points to '}'
  "{:}"     // context.begin() points to '}'
  "{:d}"    // context.begin() points to 'd'
  "{:5.3f}" // context.begin() points to '5.3f'
  "{:x}"    // context.begin() points to 'x'
  "{0} {0}" // context.begin() points to '}'
  ```

  `context.begin()` 指向格式说明符的第一个字符，`context.end()` 指向整个格式字符串的最后一个字符。当你提供格式说明符时，必须解析 `context.begin()` 和 `context.end()` 之间的所有内容，并返回闭合 `}` 的位置。

- **format**：此函数应为 `const`。它接收值 `val` 和 `std::format_context` 上下文。`format` 根据解析后的格式格式化值 `val`，并将其写入 `context.out()`。`context.out()` 的返回值可以直接传给 `std::format_to`。`std::format_to` 必须返回新位置以便继续输出。它返回一个表示输出末尾的迭代器。

[^43]: https://en.cppreference.com/w/cpp/utility/format/formatter

让我应用这些理论，并从第一个示例开始。

#### 5.5.3.1 单值的格式化器

```cpp
// formatSingleValue.cpp

#include <format>
#include <iostream>

class SingleValue {
public:
    SingleValue() = default;
    explicit SingleValue(int s) : singleValue(s) {}
    int getValue() const {
        return singleValue;
    }
private:
    int singleValue;
};

template<>
struct std::formatter<SingleValue> {
    constexpr auto parse(std::format_parse_context& context) {
        return context.begin();
    }
};
```

