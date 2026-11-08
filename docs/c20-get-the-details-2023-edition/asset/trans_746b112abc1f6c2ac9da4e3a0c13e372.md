
如果你想了解所有复杂的细节，我强烈建议你观看 JF Bastien 在 CppCon 2019 上的演讲“Deprecating volatile”。以下是他演讲中的几个例子。此外，我修正了源代码中的几个拼写错误。以下代码片段中的编号对应前面列出的三个弃用项。

### volatile 的弃用用例

```cpp
// (1)
int neck, tail;
volatile int brachiosaur;
brachiosaur = neck;      // OK, a volatile store
tail = brachiosaur;      // OK, a volatile load

// deprecated: does this access brachiosaur once or twice
tail = brachiosaur = neck;

// deprecated: does this access brachiosaur once or twice
brachiosaur += neck;

// OK, a volatile load, an addition, a volatile store
brachiosaur = brachiosaur + neck;

***********************************************
// (2)
// deprecated: a volatile return type has no meaning
volatile struct amber jurassic();

// deprecated: volatile parameters aren't meaningful to the
//             caller, volatile only applies within the function
void trex(volatile short left_arm, volatile short right_arm);

// OK, the pointer isn't volatile, the data it points to is
void fly(volatile struct pterosaur* pteranodon);

***********************************************
(3)
struct linhenykus { volatile short forelimb; };
void park(linhenykus alvarezsauroid) {
    // deprecated: does the binding copy the forelimbs?
    auto [what_is_this] = alvarezsauroid; // structured binding
    // ...
}
```

![](img/c60a87adb7f61e2e82071d081bbb389a_231_0.png)

### volatile 与多线程语义

volatile 通常用于表示可以独立于常规程序流而改变的对象。例如，在嵌入式编程中表示外部设备（内存映射 I/O）的对象。由于这些对象可以独立于常规程序流而变化，并且它们的值直接写入主内存，因此不会在缓存中进行优化存储。换句话说，volatile 避免激进的优化，并且没有多线程语义。

## 4.9.2 带初始化器的基于范围的 for 循环

在 C++20 中，你可以直接使用带初始化器的基于范围的 for 循环。

带初始化器的基于范围的 for 循环

```cpp
// rangeBasedForLoopInitializer.cpp

#include <iostream>
#include <string>
#include <vector>

int main() {

    for (auto vec = std::vector{1, 2, 3}; auto v : vec) {
        std::cout << v << " ";
    }

    std::cout << "\n\n";

    for (auto initList = {1, 2, 3}; auto e : initList) {
        e *= e;
        std::cout << e << " ";
    }

    std::cout << "\n\n";

    using namespace std::string_literals;
    for (auto str = "Hello World"s; auto c : str) {
        std::cout << c << " ";
    }

    std::cout << '\n';
}
```

基于范围的 for 循环在第 9 行使用 `std::vector`，在第 15 行使用 `std::initializer_list`，在第 23 行使用 `std::string`。此外，在第 9 行和第 15 行，我应用了自 C++17 以来就有的类模板自动类型推导。我只需写 `std::vector`，而不是 `std::vector<int>`。

![](img/c60a87adb7f61e2e82071d081bbb389a_232_0.png)

带初始化器的基于范围的 for 循环的使用

## 4.9.3 虚 constexpr 函数

constexpr 函数有可能在编译时运行，但也可以在运行时执行。因此，在 C++20 中，你可以将 constexpr 函数声明为 virtual。两个方向都是可能的。虚 constexpr 函数可以覆盖非 constexpr 函数，而虚非 constexpr 函数可以覆盖虚 constexpr 函数。我想强调，override 意味着基类的相关函数是 virtual。

程序 virtualConstexpr.cpp 展示了两种组合：

```cpp
// virtualConstexpr.cpp

#include <iostream>

struct X1 {
    virtual int f() const = 0;
};

struct X2: public X1 {
    constexpr int f() const override { return 2; }
};

struct X3: public X2 {
    int f() const override { return 3; }
};

struct X4: public X3 {
    constexpr int f() const override { return 4; }
};

int main() {
    X1* x1 = new X4;
    std::cout << "x1->f(): " << x1->f() << '\n';

    X4 x4;
    X1& x2 = x4;
    std::cout << "x2.f(): " << x2.f() << '\n';
}
```

第 24 行通过指针使用虚分派（晚绑定），第 28 行通过引用使用虚分派。

```text
X1->f(): 4
X2.f(): 4
```

虚 constexpr 函数的使用

## 4.9.4 UTF-8 字符串的新字符类型：`char8_t`

除了 C++11 中的字符类型 `char16_t` 和 `char32_t` 之外，C++20 还新增了字符类型 `char8_t`。类型 `char8_t` 足够大，可以表示任何 UTF-8 代码单元（8 位）。它与 unsigned char 具有相同的大小、符号性和对齐方式，但属于不同类型。

![](img/c60a87adb7f61e2e82071d081bbb389a_233_0.png)

### char 与 char8_t

char 有一个字节。与 char8_t 不同，一个字节的位数（因而 char 的位数）并未定义。几乎所有实现都使用 8 位作为一个字节。`std::string` 是 `std::basic_string` 字符类型的别名。

### `std::string` 与 `std::string` 字面量

```cpp
std::string std::basic_string<char>
"Hello World"s
```

因此，C++20 为字符类型 `char8_t` 新增了一个 typedef（第 1 行），并新增了 UTF-8 字符串字面量（第 2 行）。

### 新的 `char8_t` 字符类型与 UTF-8 字符串字面量

```cpp
std::u8string std::basic_string<char8_t>
u8"Hello World"
```

程序 char8Str.cpp 展示了新字符类型 char8_t 的简单用法。

### 新字符类型 char8_t 的直观用法

```cpp
// char8Str.cpp

#include <iostream>
#include <string>

int main() {

    const char8_t* char8Str = u8"Hello world";
    std::basic_string<char8_t> char8String = u8"helloWorld";
    std::u8string char8String2 = u8"helloWorld";

    char8String2 += u8".";

    std::cout << "char8String.size(): " << char8String.size() << '\n';
    std::cout << "char8String2.size(): " << char8String2.size() << '\n';

    char8String2.replace(0, 5, u8"Hello");

    std::cout << "char8String2.size(): " << char8String2.size() << '\n';
}
```

废话不多说，以下是程序的输出：

```
char8String.size(): 10
char8String2.size(): 11
char8String2.size(): 12
```

新字符类型 char8_t 的使用

C++20 没有针对 char8_t 字符串的输出运算符。因此，一种方便的方法是对 char8_t 字符串应用 `reinterpret_cast<const char*>(...)`。

### char8_t 字符串的输出

```cpp
// char8StrOutput.cpp

#include <iostream>
#include <string>

int main() {

    std::cout << '\n';

    const char8_t* char8Str = u8"Dollar: \u20AC";
    std::basic_string<char8_t> char8String = u8"Euro: \u0024";
    std::u8string char8String2 = u8"Pound: \u00A3";

    std::cout << reinterpret_cast<const char*>(char8Str) << '\n';
    std::cout << reinterpret_cast<const char*>(char8String.c_str()) << '\n';
    std::cout << reinterpret_cast<const char*>(char8String2.c_str()) << '\n';

    std::cout << '\n';
}
```

该程序显示美元（第 14 行）、欧元（第 15 行）和英镑（第 16 行）符号。

![](img/c60a87adb7f61e2e82071d081bbb389a_235_0.png)

char8_t 字符串的输出

## 4.9.5 在局部作用域中使用 using enum

using enum 声明将指定枚举的枚举项引入局部作用域。

### 在局部作用域中引入枚举项

```cpp
// enumUsing.cpp

#include <iostream>
#include <string_view>

enum class Color {
    red,
    green,
    blue
};

std::string_view toString(Color col) {
    switch (col) {
        using enum Color;
        case red: return "red";
        case green: return "green";
        case blue: return "blue";
    }
    return "unknown";
}

int main() {

    std::cout << '\n';

    std::cout << "toString(Color::red): " << toString(Color::red) << '\n';

    using Color::green;

    std::cout << "toString(green): " << toString(green) << '\n';

    using enum Color;

    std::cout << "toString(blue): " << toString(blue) << '\n';

    std::cout << '\n';

}
```

using enum 声明（第 14 行和第 32 行）将作用域枚举 Color 的枚举项引入局部作用域。从那时起，枚举项就可以不加作用域限定使用（第 15-17 行和第 34 行）。此外，你还可以为特定枚举值应用 using 声明（第 28 行）。

![](img/c60a87adb7f61e2e82071d081bbb389a_236_0.png)

## 4.9.6 位域的默认成员初始化器

首先，什么是位域？以下是维基百科⁸⁰ 的定义：“位域是计算机编程中使用的一种数据结构。它由若干相邻的计算机内存位置组成，这些位置被分配用于保存一个位序列，其存储方式使得其中的任何单个位或一组位……

⁸⁰https://en.wikipedia.org/wiki/Bit_field
