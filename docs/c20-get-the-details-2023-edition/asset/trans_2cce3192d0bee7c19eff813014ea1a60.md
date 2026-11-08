
```cpp
}
else if constexpr (std::endian::native == std::endian::little) {
    std::cout << "little-endian" << '\n';       // little-endian
}
}
```

constexpr if 使编译器能够有条件地编译源代码。也就是说，编译取决于你的架构的字节序。

## 5.4.4.2 访问或操作位或位序列

下表概述了所有函数。你可以在头文件 `<bit>` 中找到这些函数。

**位操作**

| 函数 | 描述 |
|---|---|
| `std::bit_cast` | 重新解释对象表示 |
| `std::has_single_bit` | 检查一个数是否为 2 的幂 |
| `std::bit_ceil` | 查找不小于给定值的最小 2 的整数次幂 |
| `std::bit_floor` | 查找不大于给定值的最大 2 的整数次幂 |
| `std::bit_width` | 查找表示给定值所需的最少位数 |
| `std::rotl` | 计算按位左旋转 |
| `std::rotr` | 计算按位右旋转 |
| `std::countl_zero` | 从最高有效位开始，统计连续 0 的个数 |
| `std::countl_one` | 从最高有效位开始，统计连续 1 的个数 |
| `std::countr_zero` | 从最低有效位开始，统计连续 0 的个数 |
| `std::countr_one` | 从最低有效位开始，统计连续 1 的个数 |
| `std::popcount` | 统计无符号整数中 1 的个数 |

除 `std::bit_cast` 外，所有函数都要求使用无符号整数类型（unsigned char、unsigned short、unsigned int、unsigned long 或 unsigned long long）。`std::bit_cast` 保证位数适配。当使用负数调用旋转函数 `std::rotl` 或 `std::rotr` 时，旋转方向会改变。

程序 `bit.cpp` 展示了这些函数的应用。

### 位操作

```cpp
// bit.cpp

#include <bit>
#include <bitset>
#include <cstdint>
#include <iostream>

int main() {

    std::uint8_t num{ 0b00110010 };

    std::cout << std::boolalpha;

    std::cout << "std::has_single_bit(0b00110010): " << std::has_single_bit(num)
              << '\n';

    std::cout << "std::bit_ceil(0b00110010): " << std::bitset<8>(std::bit_ceil(num))
              << '\n';
    std::cout << "std::bit_floor(0b00110010): "
              << std::bitset<8>(std::bit_floor(num)) << '\n';

    std::cout << "std::bit_width(5u): " << std::bit_width(5u) << '\n';

    std::cout << "std::rotl(0b00110010, 2): " << std::bitset<8>(std::rotl(num, 2))
              << '\n';
    std::cout << "std::rotr(0b00110010, 2): " << std::bitset<8>(std::rotr(num, 2))
              << '\n';

    std::cout << "std::countl_zero(0b00110010): " << std::countl_zero(num) << '\n';
    std::cout << "std::countl_one(0b00110010): " << std::countl_one(num) << '\n';
    std::cout << "std::countr_zero(0b00110010): " << std::countr_zero(num) << '\n';
    std::cout << "std::countr_one(0b00110010): " << std::countr_one(num) << '\n';
    std::cout << "std::popcount(0b00110010): " << std::popcount(num) << '\n';
}
```

以下是该程序的输出。

```text
std::has_single_bit(0b00110010): false
std::bit_ceil(0b00110010): 01000000
std::bit_floor(0b00110010): 00100000
std::bit_width(5u): 3
std::rotl(0b00110010, 2): 11001000
std::rotr(0b00110010, 2): 10001100
std::countl_zero(0b00110010): 2
std::countl_one(0b00110010): 0
std::countr_zero(0b00110010): 1
std::countr_one(0b00110010): 0
std::popcount(0b00110010): 3
```

### 位操作

下面的程序展示数字 2 到 7 的 `std::bit_floor`、`std::bit_ceil`、`std::bit_width` 和 `std::popcount`。

对几个数字显示 `std::bit_floor`、`std::bit_ceil`、`std::bit_width` 和 `std::popcount`

```cpp
// bitFloorCeil.cpp
#include <bit>
#include <bitset>
#include <iostream>

int main() {

    std::cout << '\n';

    std::cout << std::boolalpha;

    for (auto i = 2u; i < 8u; ++i) {
        std::cout << "bit_floor(" << std::bitset<8>(i) << ") = "
                  << std::bit_floor(i) << '\n';

        std::cout << "bit_ceil(" << std::bitset<8>(i) << ") = "
                  << std::bit_ceil(i) << '\n';

        std::cout << "bit_width(" << std::bitset<8>(i) << ") = "
                  << std::bit_width(i) << '\n';

        std::cout << "popcount(" << std::bitset<8>(i) << ") = "
                  << std::popcount(i) << '\n';

        std::cout << '\n';
    }

    std::cout << '\n';
}
```

```text
bit_floor(00000010) = 2
bit_ceil(00000010) = 2
bit_width(00000010) = 2
popcount(00000010) = 1

bit_floor(00000011) = 2
bit_ceil(00000011) = 4
bit_width(00000011) = 2
popcount(00000011) = 2

bit_floor(00000100) = 4
bit_ceil(00000100) = 4
bit_width(00000100) = 3
popcount(00000100) = 1

bit_floor(00000101) = 4
bit_ceil(00000101) = 8
bit_width(00000101) = 3
popcount(00000101) = 2

bit_floor(00000110) = 4
bit_ceil(00000110) = 8
bit_width(00000110) = 3
popcount(00000110) = 2

bit_floor(00000111) = 4
bit_ceil(00000111) = 8
bit_width(00000111) = 3
popcount(00000111) = 3
```

对几个数字显示 `std::bit_floor`、`std::bit_ceil`、`std::bit_width` 和 `std::popcount`

![](img/c60a87adb7f61e2e82071d081bbb389a_348_0.png)

## 要点提炼

- C++20 中的 `cmp_*` 函数支持整数的安全比较，因为它们能检测有符号整数与无符号整数之间的比较。在比较不安全的情况下，编译会失败。
- 现在定义了许多数学常量，例如 $e$、$\log_2 e$ 或 $\pi$。
- C++20 提供了用于计算两个值的中点或线性插值的工具函数。
- 新增了用于访问和操作单个位或位序列的函数。

## 5.5 格式化库

![](img/c60a87adb7f61e2e82071d081bbb389a_349_0.png)

### 5.5.1 格式化函数

C++20 支持以下格式化函数：

**格式化函数**

| 函数 | 描述 |
|---|---|
| `std::format` | 返回格式化后的字符串 |
| `std::format_to` | 将结果写入输出迭代器 |
| `std::format_to_n` | 最多将 n 个字符写入输出迭代器 |
| `std::vformat` | 返回格式化后的字符串 |
| `std::vformat_to` | 将结果写入输出迭代器 |

函数 `std::format` 和 `std::format_to` 在功能上分别等同于对应的 `std::vformat` 和 `std::vformat_to`，但它们在以下几个方面有所不同：

- `std::format`、`std::format_to` 和 `std::format_to_n`：它们要求格式字符串为编译期值。该格式字符串可以是 constexpr 字符串或字符串字面量。`std::formatted_size` 返回完整格式化字符串的字符数。
- `std::vformat` 和 `std::vformat_to`：其格式字符串可以是左值。参数必须传递给可变参数函数 `std::make_format_args`，例如：`std::vformat(formatString, std::make_format_args(args))`。

这些格式化函数接受任意数量的参数。下面的程序 `format.cpp` 初步展示了函数 `std::format`、`std::format_to` 和 `std::format_to_n` 的用法。

### `std::format`、`std::format_to` 和 `std::format_to_n` 初探

```cpp
// format.cpp

#include <format>
#include <iostream>
#include <iterator>
#include <string>

int main() {

    std::cout << '\n';

    std::cout << std::format("Hello, C++{}\n", "20") << '\n';

    std::string buffer;

    std::format_to(
        std::back_inserter(buffer),
        "Hello, C++{}\n",
        "20");

    std::cout << buffer << '\n';

    buffer.clear();

    std::format_to_n(
        std::back_inserter(buffer), 5,
        "Hello, C++{}\n",
        "20");

    std::cout << buffer << '\n';

    std::cout << '\n';

}
```

该程序在第 12 行直接显示格式化后的字符串。然而，第 16 行和第 25 行的调用使用字符串作为缓冲区。此外，`std::format_to_n` 只将五个字符推入缓冲区。

![](img/c60a87adb7f61e2e82071d081bbb389a_351_0.png)

格式化输出

相应地，下面是使用 `std::vformat` 和 `std::vformat_to` 的对应程序。

### `std::vformat` 和 `std::vformat_to` 初探

```cpp
// formatRuntime.cpp

#include <format>
#include <iostream>
#include <iterator>
#include <string>

int main() {

    std::cout << '\n';

    std::string formatString = "Hello, C++{}!\n";

    std::cout << std::vformat(formatString, std::make_format_args("20")) << '\n';

    std::string buffer;

    std::vformat_to(
        std::back_inserter(buffer),
        formatString,
        std::make_format_args("20"));

    std::cout << buffer << '\n';

}
```

第 12 行和第 18 行中的 `formatString` 是左值。

