

```cpp
export module squaring;

export namespace math        // Exports all nested declarations at once
{
  const double sqrt2 { 1.414213562373095 };    // the square root of 2
  auto square(const auto& x) { return x * x; }
  auto pow4(const auto& x) { return square(square(x)); }
}
```

无论如何，除了必须导入 squaring 模块之外，对于 Ex11_06 的 `main()` 程序来说，一切都没有改变。

## 组织更大的命名空间和模块

在组织更大的模块和/或命名空间时，你应当考虑以下一些策略：

-   你可以在多个模块中划分同一命名空间的实体。标准库对 `std` 命名空间所做的事情本质上就是如此。
-   你可以为部分或全部模块分配一个匹配的（嵌套）命名空间。例如，标准库的 `<ranges>` 模块就使用了 `std::ranges` 命名空间（详见第 20 章）。
-   你也可以将所有实体划分到有层次的子模块中。假设 `math` 命名空间包含的实体远多于 Ex11_06 中列出的那些。那么 `math.squaring` 将是 Ex11_06 和 Ex11_06b 模块的一个好名字。其他子模块可以命名为 `math.polynomials`、`math.geometry` 等等。利用之前讨论的技术，你可以让导入 `math` 时一次性导入所有 `math` 子模块。
-   你可以将层次化子模块与嵌套命名空间的并行层次结构结合起来（即 `math::squaring`、`math::polynomials` 等）。

无论你选择哪种方案，我们的建议是在你的代码库中尽量保持一致。毕竟，目标是在原本混乱的代码集合中建立起结构和秩序。

## 函数与命名空间

要使一个函数存在于命名空间中，只需让该函数的原型出现在一个命名空间块中即可。与全局命名空间中的函数一样，你可以在其他地方定义该函数——既可以在同一文件中，也可以（例如）在模块实现文件中。要定义这样一个其原型已经预先声明的函数，你有两种选择：要么再次将定义放在命名空间块中，要么使用函数的限定名称来引入其定义。

一个例子会使事情更加清晰。我们从一个用于又一个数学模块的模块接口文件开始。

```cpp
// math.cppm - Module interface file containing declarations and template definitions
export module math;
import <span>;

export namespace math
{
  auto square(const auto& x) { return x * x; }
}

namespace averages
{
    double arithmetic_mean(const std::span<double>& data);
    double geometric_mean(const std::span<double>& data);
    double rms(const std::span<double>& data);
    double median(const std::span<double>& data);
}
```

如前所述，将模块的接口与其实现分离，可以快速而方便地概览模块的内容。例如，这个特定的数学模块明确地专注于计算各种类型的平均值。

要导出（缩写的）`square<>()` 模板，其定义必须是模块接口的一部分，这一点之前也已解释过。你可以将其定义移到主接口文件的底部或接口分区文件中，但绝不能移到模块实现文件中。

另一方面，`math::averages` 命名空间中的函数定义可以移到模块实现文件中，如下所示。当然，你也可以简单地将它们放在模块接口文件的底部——这也没有任何问题。为简洁起见，我们在下面的概要中省略了函数体，但你可以在 Ex11_07 中找到完整的代码。

```cpp
// math.cpp - Module implementation file containing function definitions
module math;  // Remember: this implicitly imports the primary module interface...

// Option 1: define in nested namespace block (compact syntax)
namespace math::averages
{
    double arithmetic_mean(const std::span<double>& data) { /* body code... */ }
}
```

```cpp
// Option 2: define in nested namespace blocks
namespace math
{
    namespace averages
    {
        double geometric_mean(const std::span<double>& data) { /* body code... */ }
    }
}
```

```cpp
// Option 3: define using fully qualified function name
double math::averages::rms(const std::span<double>& data) { /* body code... */ }
```

```cpp
// Option 4: define using qualified name in outer namespace block
namespace math
{
    double averages::median(const std::span<double>& data) { /* body code... */ }
}
```

这个实现文件说明了在（嵌套）命名空间中声明的函数的不同定义方式。前两个函数定义只是简单地放在等效的嵌套命名空间块中。但是，由于所有函数都已在隐式导入的模块接口文件中各自对应的命名空间内声明过了，如果你不想的话，就不必再把它们的定义放在命名空间块中。你可以通过在定义中使用正确的命名空间名称来限定函数名，将定义与其声明关联起来。这就是 math.cpp 中选项 3 和选项 4 所展示的。

不言而喻，混合使用所有这些不同的选项并不是好的风格（尤其是在同一个文件中）。相反，你应该选择一种选项（最常见的是 math.cpp 中的选项 1 或选项 3），然后始终如一地在所有函数定义中使用这种风格。

## using 指令与 using 声明

从第 3 章你已经知道，通过使用 using 指令，你可以引用命名空间中的任何名称，而无需使用命名空间名称来限定它：

```cpp
using namespace std;
```

然而，这可能会破坏使用命名空间的初衷，并因为意外使用 `std` 命名空间中的名称而增加出错的可能性。因此，更好的做法通常是使用限定名称，或者为所引用的另一个命名空间中的名称添加 using 声明。正如你从第 3 章也了解到的，using 声明允许你使用某个特定的名称而无需其命名空间限定。下面是一些示例：

```cpp
using std::vector;
using std::max;
```

这些声明将名称 `vector` 和 `max` 从命名空间 `std` 引入当前作用域或命名空间。一条 using 声明可以引入许多不同的实体。例如，针对 `std::max` 的 using 声明可以通过一条 using 声明引入不同 `std::max()` 模板的所有可能实例化和重载。

我们在一些示例中偶尔已经在全局作用域中放置了一些 using 声明和指令。但你也可以将它们放置在命名空间内、函数内，甚至语句块内。当放置在命名空间中时，它使来自一个命名空间的名称在另一个命名空间中可用。下面是 Ex11_06b 的一个变体，它使用了这种技术：

```cpp
// squaring.cppm
module; // Start of the global module fragment (for #include directives)
#include <cmath> // For std::sqrt()
export module squaring;
import <numbers>; // For std::numbers::sqrt2

export namespace math
{
    using std::numbers::sqrt2;
    using std::sqrt; // Never 'using std::sqrt();' or 'using std::sqrt(double);'!
    auto square(const auto& x) { return x * x; }
    auto pow4(const auto& x) { return square(square(x)); }
}
```

通过添加 `using std::numbers::sqrt2;` 声明，你保证了在导入 squaring 后，既可以将 `sqrt2` 常量限定为 `std::numbers::sqrt2`，也可以限定为 `math::sqrt2`。请注意，如果整个 `math` 命名空间尚未被导出，你就需要使用 `export using std::numbers::sqrt2;` 来使这个别名在 squaring 模块外部可见。

导出的 `math` 命名空间中的第二个 using 声明同样也将 `sqrt()` 函数的所有重载引入到该命名空间中。你不能挑选函数中的某些重载导入命名空间；你只能导入一个特定的名称（另请参见代码中的注释）。例如，`std::sqrt()` 具有针对 `double`、`float`、`long double` 以及各种整数参数的重载；由于我们的单条 using 声明，所有这些重载现在都可以作为 `math::sqrt()` 来寻址。

如果你想将 `<numbers>` 模块的所有常量（和变量模板）引入 `math` 命名空间——而不是像我们最初那样只引入 `sqrt2` 常量——你可以通过添加（并导出）以下 using 指令来做到这一点。

```cpp
namespace math
{
    export using namespace std::numbers;
}
```

在非命名空间的任何作用域中添加 using 指令或声明时，适用类似的别名规则，但仅限于该作用域内。例如，以下函数模板用于计算给定直角三角形另外两条边长度的斜边长度（使用著名的毕达哥拉斯定理）。由于这个类型定义在全局命名空间中，其函数体默认必须用 `math::` 限定 `sqrt` 和 `square` 名称。

```cpp
auto hypot(const auto& x, const auto& y)
{
    using namespace math;
    // Or:
    //     using math::square;
    //     using math::sqrt; // Same as, of course: using std::sqrt;
    return sqrt(square(x) + square(y));
}
```

该声明或指令在包含它的块结束之前一直有效。

> **注意**  切勿在实际编程中使用这种朴素的 `hypot()` 实现。始终使用 `<cmath>` 中的 `std::hypot()` 函数。原因在于，我们这种朴素的解法常常会失败或不准确（它同时存在下溢和上溢问题）。因为创建高效且数值稳定的数学原语出奇地困难（仅关于 `hypot()` 的算法就写了许多科学论文），所以你应该始终优先寻找预定义的原语。

> **提示**  我们这里关于 using 指令和声明的内容同样适用于类型别名和 using 枚举声明（两者都在第 3 章中介绍过）。它们都可以从模块中导出和/或引入命名空间，或者在函数甚至语句作用域中更局部地应用。你在本章前面的 `from_roman()` 辅助函数中的 switch 语句中看到了局部 using 枚举声明的示例。
> 
> 就个人而言，我们倾向于尽量少地应用 using 指令和声明，并且总是尽可能在局部使用。这样我们不仅避免了意外的名称冲突，还向代码读者阐明了每个实体名称来自哪个命名空间。

