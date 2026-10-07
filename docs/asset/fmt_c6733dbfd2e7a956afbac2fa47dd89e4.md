
```cpp
template<Number... T>
sum2(T... v)
{
    return (0 + ... + v); // 将 v 的所有元素加到 0
}
```

现在，第一个被加的元素是“最左侧的”（索引最低的）：`(((0+v0)+v1)+v2)+v3)+v4)`。也就是说，从 0 所在的左侧开始。

折叠（Fold）是一种非常强大的抽象，显然与标准库中的 `accumulate()` 相关，在不同的语言和社区中有许多不同的名称。在 C++ 中，折叠表达式被限于简化变参数模板的实现。折叠并不非执行数值计算。考虑一个著名的例子：

```cpp
template<Printable... T>
void print(T&&... args)
{
    (std::cout << ... << args) << '\n'; // 打印所有参数
}
```

为什么是 2017 年？因为 `fold(v)` 在 2017 年被添加到 C++（C++17）。

## 8.4.2 参数转发

在接口中原样传递参数是变参数模板的重要用途。考虑一种网络输入通道的概念，移动值的方法是一个参数。不同的机制具有不同的构造参数集：

```cpp
template<concepts:InputTransport>
class InputChannel {
public:
    // ...
    InputChannel(Transport::Args&..., transportArgs)
        : _transport(std::forward<TransportArgs>(transportArgs));
    // ...
    Transport_transport;
}
```

标准库函数 `forward()`（§16.6）用于将参数从 `InputChannel` 构造函数原样移动到 `Transport` 构造函数。

这里的意义在于，`InputChannel` 的编写者可以在不知道构造特定 `Transport` 需要什么参数的情况下，构造任何类型的 `Transport`。`InputChannel` 的实现者只需要使用所有 `Transport` 的通用接口。

转发在需要通用性和低运行时开销且通用接口的底层库中非常常见。

## 8.5 模板编译模型

在使用处，模板的参数会对其概念进行检查。在这里发现的错误将立即报告。在此处无法检查的内容（例如无约束模板参数的参数）将推迟到为一组模板参数生成代码时进行：“实例化时”。

实例化类型检查的一个遗憾是，类型错误可能会在非常晚的时候才被发现（§8.2.4.1）。此外，检查通常会导致极其糟糕的错误信息，因为编译器没有为程序员提供类型信息提示。

# 库概述

既然无知可以瞬间获得，何必浪费时间去学习呢？

– 霍布斯

- 引言
- 标准库组件
- 标准库结构
- 命名空间：ranges 命名空间；模块；头文件
- 建议

## 9.1 引言

没有任何一个重要的程序是仅用原生编程语言编写的。首先，需要开发一套库。它们构成了进一步工作的基础。用原生语言编写大多数程序是枯燥的，而通过使用良好的库，任何任务都可以变得简单。

接第 1 至 8 章，第 9 至 18 章将快速介绍标准库的关键设施。我简要介绍实用的标准库类型，例如 `string`、`ostream`、`variant`、`vector`、`map`、`path`、`thread`、`regex`、`system_clock`、`time_zone` 和 `complex`，以及它们最常用的方法。

与前章节一样，鼓励你不要对细节的理解理解而分心或灰心。本章的目的是传达对最有用库设施的基本理解。

标准库的规范是 ISO C++ 标准的两千多页。探索它，并优先于使用自制的替代方案。它的设计上投入了大量心血，在实现上投入了更多，而在维护和扩展上将将投入大量精力。

书中描述的标准库设施是每个完整 C++ 实现的。。除了标准库组件外，大多数实现还提供了“图形用户界面”系统（GUI）、Web 接口、数据库接口等。同样，大多数应用程序开发环境为企业或工业级“标准”开发和/或执行环境提供了“基础库”。此外，还有数以万计支持专门应用领域的库。在这里，我不描述标准库之外的库、系统或环境。其目的是提供一个根据标准 [C++,2020] 定义的 C++ 的自包含式描述，并保持示例简单。自然地，鼓励程序员去探索大多数系统上提供的更广泛的设施。

## 9.2 标准库组件

标准库提供的设施可以分类如下：

- 运行时语言支持（例如用于内存分配、异常和运行时类型信息）。
- C 标准库（进行了极微小的修改，以减少对类型系统的违背）。
- 支持国际字符集、本地化和子字符串只读视图的字符串（§10.2）。
- 对正则表达式匹配的支持（§10.4）。
- I/O 流，一个用于输入输出的可扩展框架，用户可以在其中添加自己的类型、缓冲策略、区域和字符集（第 11 章）。它还提供了灵活输出格式化的设施（§11.6,2）。
- 以可移植方式操作文件的库（§11.9）。
- 容器框架（如 `vector` 和 `map`；第 12 章）和算法（如 `find()`、`sort()` 和 `merge()`；第 13 章）。按照惯，STL [Sepanov,1994] 是可扩展的，用户可以添加自己的容器和算法。Ranges（§14.1），包括 views (§14.2)、generators (§14.3) 和 pipes (§14.4)。
- 基础计算的概念，例如数学函数、复数、带有算术运算操作的向量、数学常数和随机数生成器（§15.2 和第 16 章）。
- 对并发编程的支持，包括线程和锁（第 18 章）。并发支持是基础性的，以便用户可以通过同步和异步构造添加对并发模型的支持（§18.6）。
- 某些算法的并行版本和某些数值算法，例如 `sort(13.6)` 和 `reduce(17.3,1)`。
- 支持元编程的工具（例如类型函数；§16.4）、STL 风格泛型编程（例如 `pair`；§15.3,3）和通用编程（例如 `variant` 和 `optional`；§15.4,1,15.4,2）。
- 用于管理的“智能指针”（例如 `unique_ptr` 和 `shared_ptr`；§15.2,1）。
- 特殊用途容器，如 `array` (§15.3,1)、`bitset` (§15.3,2) 和 `tuple` (§15.3,3)。
- 对绝对时间和持续时间的支持，例如 `time_point` 和 `system_clock`（§16.2,1）。
- 对日历的支持，例如 `month` 和 `time_zone`（§16.2,2,§16.2,3）。
- 常用单位的后缀，例如毫秒的 `ms` 和索引的 `i`（§16.6）。
- 操作元素序列的方法，例如 `views` (§14.2)、`string_views` (§10.3) 和 `spans` (§15.2,2)。

将类包含在库中的标准是：

- 它对几乎每个 C++ 程序员（无论是新手还是专家）都有帮助。
- 它可以以通用形式提供，且与相同设施的简单版本相比不会增加显著开销。
- 简单的用法应该易于学习（相对于其任务固有的复杂性）。

本质上，C++ 标准库提供了最常见的基础数据结构以及用于这些结构的基础算法。

## 9.3 标准库结构

标准库的设施位于 `std` 命名空间中，并通过 `std` 命名空间提供给用户。

### 9.3.1 命名空间

每个标准库设施都提供在某个头文件中。要使用它，我们必须用 `std` 对进行限定。例如：

```cpp
#include<string>
using namespace std
```

这使得 `string` 可用。为了简洁起见，我很少使用 `std::` 前缀。但在这种情况，我会使用 `std::`。例如：

```cpp
#include<string>
std::string s
```

标准库提供了几个命名空间。要使用它们，我们必须将它们引入要使用的命名空间中。例如：

```cpp
#include<string>
// 没有提到 complex_literals
auto z1 = 2+3i; // 错误：没有后缀 'i'
```

```cpp
using namespace std::complex_literals
auto z2 = 2+3i; // 正常：z2 是 complex<double>
```

对于什么是子命名空间还没有统一的哲学。然而，后缀无法明确限定，因此我们可以在范围内范围内引入一组后缀。因此，旨在与其他库（可能定义自己的后缀）工作的库的后缀被放在子命名空间中

### 9.3.2 ranges 命名空间

标准库提供了算法，如 `sort()` 和 `copy()`，有两个版本：

- 接收一对迭代器的传统版本；例如 `sort(begin(v),v.end())`。
- 接收单个范围的版本：例如 `sort(v)`

理想情况下，这两个版本应该可以完美重载而无需任何特殊努力。然而，它们并没有。例如：

```cpp
using namespace std;
using namespace std::int& v
```

```cpp
void g(vector<int>& v)
{
  sort(begin(v),v.end()); // 错误：歧义
  sort(v);                   // 错误：歧义
}
```

为了在使用传统的无约束模板时防止歧义，标准要求我们明确将标准库算法的范围版本引入作用：

```cpp
using namespace std;
void g(vector<int>& v)
```

```cpp
{
  sort(begin(v),v.end()); // OK
  sort(v);                 // 错误：没有匹配的函数（在 std 中）
  ranges::sort(v);         // OK
  using ranges::sort;      // 从这里开始 sort(v) OK
  sort(v);                 // OK
}
```

### 9.3.3 模块

目前还没有标准库模块。C++23 可能会弥补这一缺失（由于委员会时间不足导致）。目前，我使用可能成为标准的模块 `std`，提供了命名空间 `std` 中的所有功能。参见附录 A。

### 9.3.4 头文件

以下是一些标准库头文件，它们都在 `std` 命名空间中提供声明：

| 选定的标准库头文件 | | |

| :--- | :--- | :--- |

| <algorithm> | copy(), find(), sort() | 第 13 章 |

| <array> | array | $15.3 |

| <chrono> | duration, time_point, month, time_zone | $16.2 |

| <cmath> | sqrt(), pow() | $17.2 |

| <complex> | complex, sqrt(), pow() | $17.4 |

| <concepts> | floating_point, copyable, predicate, invocable | $14.5 |

| <filesystem> | path | $11.9 |

| <format> | format() | $11.6 |

| <fstream> | fstream, ifstream, ofstream | $11.7 |

| <functional> | function, greater, equal, range_value_t | 第 16 章 |

| <future> | future, promise | $18.5 |

| <ios> | hex, dec, scientific, fixed, defaultdict | $11.6 |

| <iostream> | istream, ostream, cin, cout | 第 11 章 |

| <map> | map, multimap | $12.6 |

| <memory> | unique_ptr, shared_ptr, allocator | $15.2.1 |

| <random> | default_random_engine, normal_distribution | $17.5 |

| <ranges> | sized_range, substring, take(), split(), iterator_t | $14.1 |

| <regex> | regex, smatch | $10.4 |

| <string> | string, basic_string | $10.2 |

| <string_view> | string_view | $10.3 |

| <set> | multiset | $12.8 |

| <sstream> | istream, ostring | $11.7.3 |

| <stdexcept> | length_error, out_of_range, runtime_error | $4.2 |

| <tuple> | tuple, get<>, tuple_size<> | $15.3.4 |

| <thread> | thread | $18.2 |

| <unordered_map> | unordered_map, unordered_multimap | $12.6 |

| <utility> | move(), swap(), ptr | 第 16 章 |

| <variant> | variant | $15.4.1 |

| <vector> | vector | $12.2 |

此列表并不完整。

提供了来自 C 库的头文件，例如 `<stdlib.h>`。对于每个头文件，还有一个版本，其名称以 `c` 为前缀并去除了 `_h`。这个版本（如 `<cstdlib>`）将其声明放置在全局命名空间中。

头文件反映了标准库的发展历史。因此，它们并不总是像我们希望的那样逻辑清晰且易于记忆。这就是为什么要使用模块（如 `std`，§9.3.3）的原因之一。

## 9.4 建议

- [1] 不要重造轮子；使用库；§9.1; [CG: SL.1]
- [2] 当你有选择余时，优先选择标准库而非其他库；§9.1; [CG: SL.2]
- [3] 不要认为标准库适用于所有情况；§9.1。
- [4] 如果你不使用模块，记得 `#include` 相应的头文件；§9.3.1。
- [5] 记住标准库功能定义在命名空间 `std` 中；§9.3.1; [CG: SL.3]
- [6] 使用 ranges 时，记住要显式地限定算法名称；§9.3.2。
- [7] 优先导入模块而非 `#include` 头文件 (§9.3.3)。

## 字符串与正则表达式

> 优先选择标准，而非奇特。
> – Strunk & White

- 导言
- 字符串
  - string 实现
  - 字符串视图
- 正则表达式
  - 搜索：正则表达式符号；迭代器
- 建议

文本处理是大多数程序的重要部分。C++ 标准库提供了一种字符串类型，让大多数用户避免通过指针进行 C 风格的字符数组操作。`string_view` 类型允许我们以任何存储方式操作字符序列（例如，在 `std::string` 或 `char[]` 中）。此外，还提供了正则表达式匹配以帮助在文中查找模式。正则表达式的形式与大多数现代语言中的形式相似。字符串正则对象可以使用多种字符类型（例如 Unicode）。

## 10.2 字符串

标准库提供了一种字符串类型来补充字符串字面量 (§1.2.1)；string 是一种普通类型（§8.2, §14.5），用于拥有和操作各种字符类型的序列。string 类型提供了各种许多实用的字符串操作，例如拼接。示例如：

```cpp
string incantation;

void respond(const string& answer)
{
    if (answer == incantation) {
        // ... 执行魔法 ...
    }
    else if (answer == "yes") {
        // ...
    }
}
```

标准库提供了一种字符串类型来补充字符串字面量 (§1.2.1)；string 是一种普通类型 (§8.2, §14.5)，用于拥有和操作各种字符类型的序列。string 类型提供了各种实用的字符串操作，例如拼接。示例如：

```cpp
string s1;
string s2;
// ...
```

字符串字面量定义为 `const char*`。要获取 std::string 字面量，请使用 s 后缀。

```cpp
auto cat = "Cat"; // std::string
auto dog = "Dog"; // C 风格：const char
```

要使用该后缀，你需要使用命名空间 `std::literals::string_literals` (§6.6)。

### 10.2.1 string 实现

实现字符串类是一个流行且实用的练习。然而，对于通用用途，我们精心设计的尝试很少能在能力或性能上匹配标准 string。如今，string 通常使用短字符串优化（SSO）。也就是说，短字符串值保留在内部，只有较长的字符串会被放在堆上。考虑：

```cpp
string s1 = "Annemarie"; // 短字符串
string s2 = "Annemarie Stroustrup"; // 长字符串
```

当字符串的值从短字符串变为长字符串（反之亦然）时，其表示形式会进行相应的调整。“短”字符串可以有多少个字符？这由实现定义，但“大约 14 个字符”不是一个糟糕的猜测。

# 128 字符串与正则表达式 第 10 章

字符串的实际性能在很大程度上取决于运行时环境。特别是在多线程实现中，内存分配可能相对昂贵。此外，当使用大量不同长度的字符串时，可能会导致内存碎片。这些都是短字符串优化（short-string optimization）变得普及的主要原因。
