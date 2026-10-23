

```cpp
std::string s("1.3");
//std::cout << ArithmeticCompute(s) << '\n';    // Error

//std::cout << NonArithmeticCompute(d) << '\n'; // Error

std::cout << NonArithmeticCompute(s) << '\n';   // OK
```

最后的一个例子：许多数值过程需要同时支持浮点数和复数。假设我们开发了一种算法，并且希望将数据类型限制为 double 和 std::complex<double>。那么下面的代码就满足了这一要求：

```cpp
template <typename T> typename boost::enable_if_c
  <std::is_same<T, double>::value
   || std::is_same<T, std::complex<double>>::value, T>::type
Exponential(T t)
{ // Only for double or complex<double>

    return std::exp(t);
}
```

使用示例为：

```cpp
// Exponential for double or complex<double>
double x = 3.2;
std::complex<double> c(1.0, 2.0);
float f = 3.0F;
std::cout << Exponential<double>(x) << '\n';                         // OK
std::cout << Exponential<std::complex<double>>(c) << '\n';          // OK
//std::cout << Exponential<float>(f) << '\n';                        // Error
```

这里我们也看到 float 是不允许的，如果尝试使用它将会导致编译器错误。更一般地，函数 Exponential 仅接受 double 和复数。

作为最后的评论，我们注意到 C++ 中的许多语言特性最初都以一个或多个 Boost 库的形式出现。一般来说，Boost 在撰写之时往往比 C++ 提供了更广泛的功能、示例和文档。因此我们建议及时关注 Boost 的发展及其在线文档。

## 4.8 `std::decay()` TRAIT

这是在 C++ 中另一种奇特的语法。它最好被理解为一个将给定类型转换为更简单类型的函数。总体而言，它从类型中移除 *多余的* 或其他次要信息。转换后的类型（称为 *decay 类型*）别名为 `std::decay<T>::type`。该转换类似于在按值将参数传递给函数时发生的隐式转换。

规则如下：

- 如果 T 是函数类型，则应用函数到指针的转换，decay 类型与 `add_pointer<T>::type` 相同。
- 如果 T 是数组类型，则应用数组到指针的转换，decay 类型与 `add_pointer<remove_extent<remove_reference<T>::type>::type>::type` 相同。用通俗的语言来说，我们从类型中移除引用和数组索引，并作为一系列操作向类型添加指针。
- 否则，应用常规的 *左值到右值* 转换，decay 类型与 `remove_cv<remove_reference<T>::type>::type` 相同。顺便说一下，我们将在第 6 章更详细地讨论这些“remove”函数。

我们指出，`std::decay()` 使用另一种类型作为模型来获得一种类型，但它不会在这些类型之间转换值或对象。它是一个 *高阶函数*，因为它对函数进行操作并且也返回函数。它可以被视为 C++ 中 *去漆剂* 的等价物（作者观点）。

我们举一个例子。我们首先定义一些类型别名：

```cpp
using A = std::decay<int>::type;                 // int
using B = std::decay<int&>::type;                // int
using C = std::decay<int&&>::type;               // int
using D = std::decay<const int&>::type;          // int
using E = std::decay<int[2]>::type;              // int*
using F = std::decay<int (int)>::type;           // int(*)(int)

using G = std::decay<volatile int>::type;        // int
using H = std::decay<const volatile int&>::type; // int
```

其次，我们将得到的 decay 类型与类型 `int` 进行比较。你应该运行代码并将输出与你的预期进行比较，并尝试使用用户定义的类型。

## 4.9 一个小型应用：量与单位

我们以一个小型应用来结束本章，用于建模量纲、单位和量。例如，我们希望将值 100 定义为长度（可能是英里）或温度（例如摄氏度）。我们如何实现这一点？为此，我们采用 Abrahams 和 Gurtovoy（2005）中的一个例子。在此之前我们引用一个失败的项目，因为一家承包商使用 SI 单位而另一家承包商使用非 SI 单位：

> 火星气候轨道器是一颗质量为 338 千克（745 磅）的机器人空间探测器，由 NASA 于 1998 年 12 月 11 日发射，用于研究火星气候、火星大气和地表变化，并作为 1998 年火星探测器计划中火星极地着陆器的通信中继。然而，在 1999 年 9 月 23 日，与航天器的通信在航天器进入轨道插入时丢失，原因是地面计算机软件产生的输出使用非 SI 单位磅力-秒（lbf·s）而不是合同中 NASA 与洛克希德之间规定的 SI 单位牛顿-秒（N·s）。航天器以一条轨迹接近火星，使其过近地接近行星，导致其穿过上层大气并解体。

我们对 *量纲分析* 主题做一个简要介绍。该理论关注通过识别其基本 *量纲*（例如长度、质量和时间）和 *度量单位*（例如英里与公里、磅与千克）来分析不同物理量之间的关系。我们还希望在进行计算和比较时在量纲单位之间转换并跟踪量纲。

*基本量纲* 是我们希望测量的某个实体，例如质量、长度和时间。基本量纲本质上是标签，它们本身并不提供量纲分析功能。在 C++ 中，我们可以使用 *Boost.MPL* 的功能来建模基本和复合量纲：

```cpp
#include <boost/mpl/vector_c.hpp>

// Base dimensions
using mass =
    boost::mpl::vector_c<int, 1, 0, 0, 0, 0, 0, 0>;      // M
using length =
    boost::mpl::vector_c<int, 0, 1, 0, 0, 0, 0, 0>;      // L
using time =
    boost::mpl::vector_c<int, 0, 0, 1, 0, 0, 0, 0>;      // T
using charge =
    boost::mpl::vector_c<int, 0, 0, 0, 1, 0, 0, 0>;
using temperature =
    boost::mpl::vector_c<int, 0, 0, 0, 0, 1, 0, 0>;
using intensity =
    boost::mpl::vector_c<int, 0, 0, 0, 0, 0, 1, 0>;
using angle =
    boost::mpl::vector_c<int, 0, 0, 0, 0, 0, 0, 1>;

// (Composite) dimensions
using force =
    boost::mpl::vector_c<int, 1, 1, -2, 0, 0, 0, 0>;     // ML/T^2
using velocity =
    boost::mpl::vector_c<int, 0, 1, -1, 0, 0, 0, 0>;     // L/T
using acceleration =
    boost::mpl::vector_c<int, 0, 1, -2, 0, 0, 0, 0>;     // L/T^2
using dynamicViscosity =
    boost::mpl::vector_c<int, 1, -1, -1, 0, 0, 0, 0>;    // M/(LT)
```

这些类型是纯元数据。为了能够执行计算，我们创建一个类来建模 *量*。要相加或相减的参数的量纲必须始终匹配，否则我们将得到编译器错误：

```cpp
// TMP Abrahams and Gurtovoy page 40
template <class T, class Dimensions>
    struct Quantity
```

与某个偏积分微分方程（PIDE）相关的 VG 过程的 VG 过程。谱值为：

λₙ = 1/ϑ × Λₙ(σ²ϑ / L²), n = 1, 2, ...

其中参数及其量纲由以下给出：

- (ϑ, σ) = VG 过程的参数
- [ϑ] = [T], [σ²] = [X²/T]
- [X] = 空间坐标的量纲
- L = PIDE 问题的上边界
- [L] = [X]
- λₙ = PIDE 谱问题的特征值，[λₙ] = [1/T]
- Λₙ = 缩放函数

再次总结，我们看到缩放函数是无量纲的。

## 4.10 结论与总结

我们对 C++ 中一系列新的和高级主题进行了详细阐述，这些主题属于模板元编程和泛型编程等各种名称。如果我们希望编写灵活且健壮的代码，对这些技术的理解至关重要。

我们将在本书的后面章节讨论如何将泛型编程技术应用于数值分析和计算金融。

## 4.11 练习与项目

- 1. （隐式转换‘101’）
  - 复习并运行实现第 4.2.1 节中情况 A1、A2、A3 和 A4 的代码。
  - 回答以下问题：
    - a) 确定此代码生成的编译器错误和/或警告。确定这些错误的严重性。
    - b) 确定如何修改代码以在应移除这些编译器错误和/或警告的情况下进行修改。
    - c) 解释此代码的输出：

      ```cpp
      std::cout << AddIntegers(4, 10, 'A', true, false) << '\n';  // 76
      ```

- 2. （可变参数函数）
  - 本练习的目标是使用第 4.2.2 节中的功能计算可变参数函数的参数的标准差。我们提出两个阶段；首先创建一个名为 args1 的 va_list 并用它来计算均值，然后使用 va_copy 复制 args1 以计算输入参数的标准差。

