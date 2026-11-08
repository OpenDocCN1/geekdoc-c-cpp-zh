
> **注意** 与头文件（参见附录 A）不同，用于 `import` 模块的名称并不基于包含模块接口的文件名。相反，它基于在 `export module` 声明中声明的名称。虽然有些编译器要求文件名与模块名称匹配，但其他编译器也允许模块接口文件使用任意名称。因此，尽管在本书中我们总是将模块接口文件命名为 `module_name.cppm`，但请记住，从技术上讲，这个文件的名称并不决定你在 `import` 声明中应使用的名称。

一旦导入了模块，你就可以使用它导出的所有实体。例如，`Ex11_01` 的 `main()` 函数使用了我们强大无比的 `math` 模块导出的所有实体：`square<>()` 函数模板的一个实例化、`lambda` 常量、`getOddity()` 函数以及 `Oddity` 枚举类型。

不过，关键在于你只能使用这些导出的实体。举例来说，你可以尝试取消注释 `Ex11_01.cpp` 中调用 `isOdd()` 的 `if` 语句。然后编译器会提示它不知道任何名为 `isOdd()` 的函数。这并不奇怪：并不是因为 `isOdd()` 在模块接口文件中声明，它就会自动成为模块接口的一部分。要让 `isOdd()` 从 `math` 模块外部可见，你还必须在其定义前添加 `export`。

除此之外，`Ex11_01.cpp` 的 `main()` 程序几乎没有什么新内容，也许除了 `switch` 语句中的 `using enum` 声明。我们在第 3 章向你展示了如何使用 `using enum` 声明，但这是我们第一次在 `switch` 语句（第 4 章介绍）中使用它。得益于这个 `using` 声明，你可以在枚举项名称 `Even` 和 `Odd` 前省略 `Oddity::`——但仅在该 `switch` 语句的作用域内。在本章后面，你会看到，同样可以把其他 `using` 声明和 `using` 指令放在语句、函数或命名空间的作用域中。

### 导出块

在 `Ex11_01` 中，我们使用四个单独的 `export` 声明，逐个导出了四个不同的实体。你也可以通过将它们分组到一个*导出块*中，一次性导出多个实体。导出块由 `export` 关键字后跟花括号之间的一系列声明组成。下面是 `Ex11_01` 中 `math` 模块的另一种定义，它使用导出块而不是四个导出声明的序列（该模块文件可从 `Ex11_01A` 获取）。

```cpp
// math.cppm - Exporting multiple entities at once
export module math;

bool isOdd(int x) { return x % 2 != 0; }  // Module-local function (not exported)

export
{
    auto square(const auto& x) { return x * x; }

    const double lambda{ 1.303577269034296391257 }; // Conway's constant

    enum class Oddity { Even, Odd };
    auto getOddity(int x) { return isOdd(x) ? Oddity::Odd : Oddity::Even; }
}
```

### 将接口与实现分离

到目前为止，所有实体都始终直接定义在模块接口文件中。对于像我们强大的 math 模块中的那些小函数和类型来说，这样做完全没问题。当然，math 的接口文件也许已经因为模块局部的 isOdd() 函数而显得有些杂乱，但还不至于太分散注意力。然而，在现实中，函数定义可能每个长达数十行，而且你可能需要更多局部函数和类型来实现导出的接口。如果不小心，所有这些实现细节都可能掩盖模块的接口，使人更难快速了解某个特定模块提供了什么。在这种情况下，你应该考虑将模块的接口（例如只包含导出函数的原型）与其实现（即这些导出函数连同任何模块局部实体一起定义的地方）分离。

将模块接口与实现分离的第一种选择，是在模块接口文件本身内部进行分离。如下所示：

```cpp
// math.cppm - Exporting multiple entities at once
export module math;

export   // The module's interface
{
    auto square(const auto& x);

    const double lambda = 1.303577269034296391257;  // Conway's constant

    enum class Oddity { Even, Odd };
    auto getOddity(int x);
}

// The implementation of the module's functions (+ local helpers)
auto square(const auto& x) { return x * x; }

bool isOdd(int x) { return x % 2 != 0; }
auto getOddity(int x) { return isOdd(x) ? Oddity::Odd : Oddity::Even; }
```

你始终可以像这样把函数定义移到模块接口文件的底部。你甚至可以把枚举类型 Oddity 的定义下移，先用 `enum class Oddity;` 声明它。不过，我们把 Oddity 的定义留在了导出块中，因为它是——而且需要是——模块接口的一部分（使用者需要知道枚举项才能使用该模块）。常量必须立即初始化，因此 lambda 的定义不能移动。

不过，请注意，你从之前的示例中已经知道了其中大部分内容：我们经常也把所有函数原型放在源文件顶部（以便清晰概览可用函数），并把所有函数定义放在底部（通常放在使用它们的 main() 函数之后）。

此时唯一真正值得注意的新一点是，你不必在底部的定义前重复 `export` 关键字。你可以重复，但不是必须。也就是说，你可以在 math.cppm 底部 square<>() 和 getOddity() 的定义前重复 export，但这样做完全是可选的。

然而，不允许在某个实体的声明前添加 export，而该实体最初声明时没有 export。例如，下面这组声明因此会导致编译错误。

```cpp
bool isOdd(int x);
// ...
export bool isOdd(int x); /* Error: isOdd() was previously declared as not exported! */
```

```cpp
static const std::string cds[]{ "", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM" };
static const std::string xls[]{ "", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC" };
static const std::string ivs[]{ "", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX" };
return ms[i / 1000] + cds[(i % 1000) / 100] + xls[(i % 100) / 10] + ivs[i % 10];
}
```

与所有模块文件一样，模块实现文件包含模块声明。然而，与模块接口文件不同，模块实现文件的模块声明不以 export 关键字开头。自然，这意味着模块实现文件不能导出任何实体。事实上，你甚至不能在这里 to_roman() 的定义前重复 export 关键字；你只能在模块接口文件中添加或重复 export。

to_roman() 函数本身的实现包含一些巧妙而紧凑的编码，用于将无符号整数转换为标准罗马数字。不过，既然你已在本节前半部分掌握了 C++ 表达式和函数，我们相信你能弄清楚它是如何工作的。由于本节的重点是模块，因此我们将解读这个函数体留作你的可选练习。

为完整起见，下面是我们 roman 模块的第二个模块实现文件；如你所知，它庞大到不可能放进单个实现文件。

```cpp
// from_roman.cpp - Implementation of the from_roman() function
module roman;

unsigned int from_roman(char c)
{
    switch (c)
    {
    case 'I': return 1;    case 'V': return 5;    case 'X': return 10;
    case 'L': return 50;   case 'C': return 100;  case 'D': return 500;
    case 'M': return 1000; default: return 0;
    }
}

unsigned int from_roman(std::string_view roman)
{
    unsigned int result{};
    for (size_t i{}, n{ roman.length() }; i < n; ++i)
    {
        const auto j{ from_roman(roman[i]) };   // Integer value of the i'th roman digit
        // Look at the next digit (if there is one) to know whether to add or subtract j
        if (i + 1 == n || j > from_roman(roman[i + 1])) result += j; else result -= j;
    }
    return result;
}
```

第二个实现文件与前一个类似，不同之处在于它定义了一个局部辅助函数，用于将单个罗马数字位转换为整数。from_roman() 的这个重载仅在当前源文件内可见。

由于 switch、for 和 if 语句都是熟悉的内容，我们同样完全相信你能弄清楚这些 from_roman() 函数如何工作（如果你感兴趣的话）。我们添加了一些注释来帮你入门（在你自己的代码中，只要逻辑不那么显而易见，添加这类注释也从来不是坏主意）。

