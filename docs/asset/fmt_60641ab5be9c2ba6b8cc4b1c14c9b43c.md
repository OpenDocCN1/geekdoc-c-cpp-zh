
### 4.1.2.2 Koenig 查找（Koenig lookup）

如果 Koenig 查找被称为“Koenig 原则”，它完全可以作为一部新的鲁德姆（Ludlum）小说的标题。但它并不是。相反，它指的是一种 C++ 的技术细节。

Koenig 查找指的是这样一个事实：如果在不指定命名空间的情况下调用一个函数，则将使用其参数类型的命名空间来确定该函数的命名空间。如果定义参数的命名空间包含此类函数，则使用该函数。这一过程被称为“Koenig 查找”。

为了说明，请考虑下一个示例。函数 `FBB::fun(FBB::Value v)` 定义在 `FBB` 命名空间中。可以在不显式提到其命名空间的情况下调用它：

```cpp
#include <iostream>

namespace FBB
{
    enum Value // 定义 FBB::Value
    FIRST
}
```

## 4.1. 命名空间

```cpp
);

void fun(Value x)
{
    std::cout << "fun called for " << x << '\n';
}
```

```cpp
int main()
{
    fun(FBB::FIRST); // Koenig 查找：无命名空间
    // 对于指定的的 fun()
}

/*
    生成输出:
fun called for 0
*/
```

编译器在处理命名空间时相当智能。如果 `FBB` 命名空间中的 `Value` 被定义为 `using Value = int`，那么 `FBB::Value` 将被识别为 `int`，从而导致 Koenig 查找失败。

作为另一个例子，考虑下面的程序。这里涉及两个命名空间，每个命名空间都定义了自己的 `fun` 函数。这里没有歧义，因为参数定义了命名空间并且调用了 `FBB::fun`：

```cpp
#include <iostream>

namespace FBB
{
    enum Value // 定义 FBB::Value
    {
        FIRST
    };
}

void fun(Value x)
{
    std::cout << "FBB::fun() called for " << x << '\n';
}
```

```cpp
namespace ES
{
    void fun(FBB::Value x)
    {
        std::cout << "ES::fun() called for " << x << '\n';
    }
}
```

```cpp
int main()
{
    fun(FBB::FIRST); // 无歧义：参数决定了
    // 命名空间
}

/*
    生成输出:
FBB::fun() called for 0
*/
```

这里有一个存在歧义的示例：`fun` 有两个参数，分别来自每个命名空间。这种歧义必须由程序员解决：

## 4.1. 命名空间（NAMESPACES）

可以使用完全限定名。实体的完全限定名是在到达实体定义之前遇到的所有命名空间的列表。命名空间和实体通过作用域解析运算符连接在一起：

```cpp
int main()
{
  CppAnnotations::value = 0;
  CppAnnotations::Virtual::pointer = 0;
}
```

可以提供 `using namespace CppAnnotations` 指令。现在可以在任何前缀的情况下使用 `value`，但 `pointer` 必须带有 `Virtual::` 前缀：

```cpp
using namespace CppAnnotations;

int main()
{
  value = 0;
  Virtual::pointer = 0;
}
```

可以使用完整命名空间链的 `using namespace` 指令。现在 `value` 再次需要 `CppAnnotations` 前缀，但 `pointer` 不再需要前缀：

```cpp
using namespace CppAnnotations::Virtual;

int main()
{
  CppAnnotations::value = 0;
  pointer = 0;
}
```

当使用两个独立的命名空间指令时，不再需要任何命名空间前缀：

```cpp
using namespace CppAnnotations;
using namespace Virtual;

int main()
{
  value = 0;
  pointer = 0;
}
```

通过提供特定的 `using` 声明为特定变量实现相同的效果（即无命名空间前缀）：

```cpp
using CppAnnotations::value;
using CppAnnotations::Virtual::pointer;
```

```cpp
int main()
{
  value = 0;
  pointer = 0;
}
```

## 第 4 章 命名空间（NAMESPACES）

- 也可以结合使用 `using namespace` 指令和 `using` 声明。例如，可以在 `CppAnnotations::Virtual` 命名空间使用 `using namespace` 指令，对 `CppAnnotations::value` 变量使用 `using` 声明：

```cpp
using namespace CppAnnotations::Virtual;
using CppAnnotations::value;

int main() {
    value = 0;
    pointer = 0;
}
```

跟随 `using namespace` 指令，该命名空间的所有实体都可以在任何前缀的情况下使用。如果使用单个 `using namespace` 指令引用嵌套命名空间，则该嵌套命名空间的所有实体都可以在无需进一步前缀的情况下使用。然而，定义在最浅层命名空间中的实体仍然需要该浅层命名空间的名称。只有在提供了特定的命名空间指令或 `using` 声明后，才能省略命名空间限定。

当认为完全限定名比如下名称

```cpp
CppAnnotations::Virtual::pointer
```

长时，可以使用命名空间别名：

```cpp
namespace CV = CppAnnotations::Virtual;
```

这将 `CV` 定义为完全名的别名。现在可以使用以下方式访问变量 `pointer`：

```cpp
CV::pointer = 0;
```

命名空间别名也可以用于 `using namespace` 指令或 `using` 声明：

```cpp
namespace CV = CppAnnotations::Virtual;
using namespace CV;
```

### 嵌套命名空间定义

从 C++17 标准开始，在嵌套命名空间时，可以使用作用域解析运算符直接引用嵌套命名空间。例如：

```cpp
namespace Outer::Middle::Inner {
    // 在这里定义/声明的实体位于 Inner
    // 命名空间中，该命名空间在 Middle 命名空间中定义，
    // 而 Middle 又在 Outer 命名空间中定义。
}
```

### 4.1.4.1 在命名空间之外定义实体

并不是严格要求在命名空间区域内定义命名空间的成员。但在命名空间之外定义实体之前，它必须已在其命名空间内部声明过。

## 4.1 命名空间（NAMESPACES）

要在命名空间之外定义实体，必须通过为成员加上命名空间名前缀来完全限定。定义可以在全局级别提供，也可以在嵌套命名空间的情况下在中间层提供。这允许我们在命名空间 `A` 的区域内定义属于命名空间 `A::B` 的实体。

假设类型 `INT8[8]` 定义在 `CppAnnotations::Virtual` 命名空间中。此外，我们还打算在 `CppAnnotations::Virtual::INT8` 命名空间内部定义函数 `squares`。

在 `CppAnnotations::Virtual` 命名空间中定义了前提后，函数可以定义如下（第 9 章涵盖了内存分配运算符 `new[]`）：

```cpp
namespace CppAnnotations
{
    namespace Virtual
    {
        void *pointer;
        using INT8 = int[8];

        INT8 *squares()
        {
            INT8 *ip = new INT8[1];
            for (size_t idx = 0; idx != sizeof(INT8) / sizeof(int); ++idx)
                (*ip)[idx] = (idx + 1) * (idx + 1);
            return ip;
        }
    }
}
```

函数 `squares` 定义了一个包含一个 `INT8` 向量的数组，并在通过前八个自然数的平方初始化向量后返回其地址。

现在可以在 `CppAnnotations::Virtual` 命名空间之外定义函数 `squares`：

```cpp
namespace CppAnnotations
{
    namespace Virtual
    {
        void *pointer;
        using INT8 = int[8];
        INT8 *squares();
    }
}

CppAnnotations::Virtual::INT8 CppAnnotations::Virtual::squares()
{
    INT8 *ip = new INT8[1];
    for (size_t idx = 0; idx != sizeof(INT8) / sizeof(int); ++idx)
        (*ip)[idx] = (idx + 1) * (idx + 1);
    return ip;
}
```

在上述代码片段中请注意：

- `squares` 声明在 `CppAnnotations::Virtual` 命名空间内部。
- 命名空间之外的定义要求我们使用函数及其返回类型的完全限定名。
- 在 `squares` 函数体内，我们处于 `CppAnnotations::Virtual` 命名空间内，因此在函数内部完全限定名（例如 `INT8`）不再需要。

## 第 4 章 命名空间

`ratio<1, 1000>` - 表示 1/1000。

`ratio` 类定义了两个可访问的静态数据成员：`num` 表示其分子，`den` 表示其分母。`ratio` 定义本身仅仅定义了一个特定的数值。例如，当执行程序时：

```cpp
#include <ratio>
#include <iostream>
using namespace std;

int main() {
    cout << ratio<5, 1000>::num << ' ' << ratio<5, 1000>::den << '\n';
    cout << milli::num << ' ' << milli::den << '\n';
}
```

会显示文本 1,200，因为这是 `ratio<5, 1000>` 所表示的“数值”，它会尽可能对分数进行约分。

存在许多预定义的 `ratio` 类型。它们与 `ratio` 本身一样，定义在 `std` 命名空间中，可以用来代替更麻烦的 `ratio<x>` 或 `ratio<x, y>` 规格：

| yocto | 10⁻²⁴ | zepto | 10⁻²¹ |
|---|---|---|---|
| atto | 10⁻¹⁸ | femto | 10⁻⁵ | pico | 10⁻¹² |
| nano | 10⁻⁹ | micro | 10⁻⁶ | milli | 10⁻³ |
| cent | 10⁻² | deci | 10⁻¹ | | |
| | | hect | 10⁻² | kilo | 10³ |
| mega | 10⁶ | giga | 10⁹ | tera | 10¹² |
| peta | 10¹⁵ | exa | 10¹⁸ | | |
| zetta | 10²¹¹ | yotta | 10²⁴ | | |

（注意：`yocto`、`zepto`、`zetta` 和 `yotta` 类型的定义使用了超过 64 位的整数常量。虽然这些常量在 C++ 中被定义，但在 64 位或更小的架构上不可用。）

时间比例可以很好地解释为秒的分数或倍数，其中 `ratio<1,1000>` 表示一秒的分辨率。

这里是一个展示这些缩写如何使用的示例：

```cpp
cout << milli::num << ' ' << milli::den << '\n';
cout << milli::num << ' ' << milli::den << '\n';
```

## 4.2 `STD::CHRONO` 命名空间（处理时间）

时间量通过 `std::chrono::duration` 类的对象来指定。

在使用 `duration` 类之前，必须包含 `<chrono>` 头文件。

与 `ratio` 类似，`duration` 类需要两个模板参数：一个数值类型（通常是 `int64_t`）定义持续时间的数值类型，以及一个时间分辨率（通常通过 `std::ratio` 类型指定，使用 chrono 的缩写之一）。

使用预定义的 `std::deca` ratio（代表 10 秒单位），将 30 分钟的时间间隔定义为：

```cpp
duration<int64_t, std::deca> halfHr(180);
```

在这里，`halfHr` 代表 180 deca 的时间间隔，即 1800 秒。与 `halfHr` 类似的定义类型有：

| nanoseconds | `duration<int64_t, nano>` |
| microseconds | `duration<int64_t, micro>` |
| milliseconds | `duration<int64_t, milli>` |
| seconds | `duration<int64_t>` |
| minutes | `duration<int64_t, ratio<60>>` |
| hours | `duration<int64_t, ratio<3600>>` |

使用这些类型，现在可以将 30 分钟的时间量简单地定义为 `halfHour(30)`。

使用这些类型，30 分钟的时间量现在可以简单地定义为 `halfHour(30)`。

`duration` 提供了以下成员函数类型：

- `rep`：持续时间数值的数值类型。
- `period`：表示时间分辨率的 `ratio` 类型。
- `count()`：返回持续时间数值的计数。
- `time_since_epoch()`：返回自纪元以来的时间。
- `ratio()`：返回 `period` 的 `ratio` 类型。
- `operator()`：返回 `duration` 的数值。
- `operator double()`：返回 `duration` 的浮点数数值。
- `operator long long()`：返回 `duration` 的长整数数值。
- `operator int()`：返回 `duration` 的整数数值。
- `operator signed()`：返回 `duration` 的有符号整数数值。
- `operator unsigned()`：返回 `duration` 的无符号整数数值。
- `operator float()`：返回 `duration` 的单精度浮点数值。
- `operator double()`：返回 `duration` 的双精度数值。
- `operator long double()`：返回 `duration` 的扩展精度浮点数值。
- `operator==`：比较两个 `duration` 是否相等。
- `operator!=`：比较两个 `duration` 是否不等。
- `operator<`：比较两个 `duration` 的大小。
- `operator>`：比较两个 `duration` 的大小。
- `operator<=`：比较两个 `duration` 的大小。
- `operator>=`：比较两个 `duration` 的大小。
- `operator+`：相加两个 `duration`。
- `operator-`：相减两个 `duration`。
- `operator*`：将 `duration` 乘以一个数值。
- `operator/`：将 `duration` 除以一个数值。
- `operator+=`：累加一个 `duration`。
- `operator-=`：减去一个 `duration`。
- `operator*=`：将 `duration` 乘以一个数值。
- `operator/=`：将 `duration` 除以一个数值。
- `operator<<`：将 `duration` 输出到输出流。
- `operator>>`：从输入流读取 `duration`。

两个 `duration` 类型之间可以比较，只要它们的 `period` 相同。如果 `period` 不同，则需要通过 `duration_cast` 进行转换。

`duration_cast` 用于将一个 `period` 的 `duration` 转换为另一个 `period` 的 `duration`。这在转换可能会丢失精度时是必须的：

```cpp
