

```cpp
std::cout << std::format("The value of the expression {} < {} is {}\n",
                         first, second, first < second);
std::cout << std::format("The value of the expression {} == {} is {}\n",
                         first, second, first == second);
```

## 比较浮点数值

当然，你也可以比较浮点数值。让我们考虑一些稍微复杂一点的数值比较。首先，用以下语句定义变量：

```cpp
int i {-10};
int j {20};
double x {1.5};
double y {-0.25e-10};
```

现在考虑以下逻辑表达式：

```cpp
-1 < y        j < (10 - i)        0.0*x < (3 + y)
```

比较运算符的优先级都低于算术运算符，因此这些括号并非严格必需，但它们确实有助于让表达式更清晰。第一个比较求值为 true，因为 y 有一个非常小的负值（约 −0.000000000025），它大于 −1。第二个比较结果为 false，因为表达式 10 − i 的值为 20，与 j 相同。第三个表达式为 true，因为 3 + y 略小于 3。

浮点比较的一个特殊之处在于：非数（not-a-number）值既不小于、也不大于、也不等于任何其他数。它们甚至不等于另一个非数值。让 nan 变量定义如下（关于 numeric_limits 模板，见第 2 章）：

```cpp
const double nan{ std::numeric_limits<double>::quiet_NaN() };
```

那么以下所有表达式都会求值为 false：

```cpp
i < nan     nan > j     nan == nan
```

你可以使用关系运算符比较任何基本类型的值。当你学习类之后，就会看到如何让你定义的类型也支持比较运算符。现在你需要的只是一种利用比较结果来改变程序行为的方法。我们很快就会研究这一点。但首先：来自外太空的一次造访……

## 宇宙飞船运算符

在 C++20 中，语言新增了一个用于比较值的运算符：三向比较运算符，记作 `<=>`。这个新运算符更广为人知的非正式名称是“宇宙飞船运算符”。它之所以得到这个绰号，是因为字符序列 `<=>` 有点像一个飞碟！

在某种意义上，`<=>` 的行为就像是把 `<`、`==` 和 `>` 全部压缩成了一个。简而言之，`<=>` 在单个表达式中判定 a 是小于、等于还是大于 b。不过，通过一些代码来解释 `<=>` 的基本工作方式最容易。下面的示例读取一个整数，然后使用 `<=>` 将该数字与零进行比较：

```cpp
// Ex4_02.cpp
// Three-way comparison of integers
import <compare>;  // Required when using operator <=> (even for fundamental types)
import <format>;
import <iostream>;

int main()
{
    std::cout << "Please enter a number: ";

    int value;
    std::cin >> value;

    std::strong_ordering ordering{ value <=> 0 };

    std::cout << std::format("value < 0: {}\n", ordering == std::strong_ordering::less);
    std::cout << std::format("value > 0: {}\n", ordering == std::strong_ordering::greater);
    std::cout << std::format("value == 0: {}\n", ordering == std::strong_ordering::equal);
}
```

对于整数操作数，运算符 `<=>` 会求值为 `std::strong_ordering` 类型的值；该类型在大多数情况下表现得像枚举类型（见第 3 章），可能取值为 less、greater 和 equal（从技术上说还有第四个值，但稍后会详细说明）。然后，根据 `ordering` 的值，你可以确定 value 相对于数字 0 的排序关系。

此时，你可能会想：这个运算符有什么意义？你有此疑问很合理。如同所有外星接触一样，宇宙飞船运算符乍看之下有些奇怪且令人费解。毕竟，Ex4_02 的最后四行可以更简洁地写成下面这样（类似于 Ex4_01A）：

```cpp
std::cout << std::format("value < 0: {}\n", value < 0);
std::cout << std::format("value > 0: {}\n", value > 0);
std::cout << std::format("value == 0: {}\n", value == 0);
```

输入量少得多，效率却同样高（好像性能对整数比较真的重要似的）。确实：单独比较基本类型的变量时，`<=>` 运算符几乎没有什么意义。然而，比较更复杂类型的变量可能代价高昂。此时，只比较一次（如 Ex4_02）而不是两到三次（如 Ex4_01）就会有所回报。我们将在第 7 章看到使用 string 对象的此类示例。在第 13 章，我们将向你展示：得益于 `<=>` 运算符，为自己的对象类型添加比较支持会变得轻而易举。但所有这些最终都建立在基本类型的 `<=>` 比较之上。而在达到那一步之前，我们需要在接下来的两个小节中再介绍一些基础知识。

## 比较类别

`<=>` 运算符并不总是求值为 `std::strong_ordering` 类型的值。它求值得到的类型取决于其操作数的类型。例如，对于浮点数 `f1` 和 `f2`，`f1 <=> f2` 的类型会是 `std::partial_ordering`。原因在于，从数学上说，浮点数不是强序的（或者在数学中更常称为全序）；它们只是偏序的。也就是说：并非所有浮点数对都可比较。具体来说，如上一节所示，非数值相对于任何其他数都没有顺序。因此，如果 `f1` 和/或 `f2` 是非数，`f1 <=> f2` 会求值为 `std::partial_ordering::unordered`。

表 4-2 展示了可用于三向比较的三种类型。比较大多数基本类型或标准库类型的两个值时，会得到 `strong_ordering`。当这些值是浮点值或包含浮点值时，结果会变为 `partial_ordering`。比较标准类型绝不会得到 `weak_ordering`，但和所有比较类别类型一样，你可以将它用于用户定义的 `<=>` 运算符（见第 13 章）。弱序的一个例子是：按点到原点的距离对欧几里得空间中的点进行排序。

**表 4-2.** 由 `<compare>` 定义的比较类别类型

| | 小于 | 大于 | 相等 | 等价 | 无序 | 用途 |
|---|---|---|---|---|---|---|
| `strong_ordering` | ✓ | ✓ | ✓ | ✓ | | 整数和指针 |
| `partial_ordering` | ✓ | ✓ | | ✓ | ✓ | 浮点数 |
| `weak_ordering` | ✓ | ✓ | | ✓ | | 仅限用户定义运算符 |

这三种比较类别类型由 `<compare>` 模块定义。每当你使用 `<=>` 运算符时，即使操作数是基本类型，也必须导入 `<compare>` 模块，否则会得到编译器错误（你可以用 Ex4_02 试一试）。

请注意，只有 `strong_ordering` 使用术语“相等”，而 `partial_ordering` 和 `weak_ordering` 使用“等价”。形式上说，相等意味着可替换性，而等价则不然。反过来，可替换性大致意味着：如果 `a == b` 为真，那么对于任意函数 `f`，`f(a) == f(b)` 也必须为真。例如，对于浮点值，尽管 `-0.0 == +0.0`，但 `signbit(-0.0) != signbit(+0.0)`（`signbit()` 是一个 `<cmath>` 函数，它返回——你猜对了——浮点数的符号位）。换句话说：`-0.0` 和 `+0.0` 非常接近相等，但并不完全相等；然而，从一切实际意义上看，它们完全等价。

**注意** `std::strong_ordering::equivalent` 等于 `std::strong_ordering::equal`。我们建议你主要使用后者，因为它能更好地表达强序的语义。

`strong_ordering` 值会隐式转换为 `weak_ordering` 或 `partial_ordering`，而 `weak_ordering` 值会隐式转换为 `partial_ordering`。这些转换会产生显而易见的结果。然而，`partial_ordering` 值不能转换为另外两种类型中的任何一种。这也完全合理：否则，你打算如何处理无序值呢？

**注意** 表 4-2 中的比较类别类型只是表现得像枚举类型，但它们实际上是类类型。其后果包括：不能对它们使用 enum 语句，而且在本章后面看到的 `switch` 语句中也不能使用它们。

