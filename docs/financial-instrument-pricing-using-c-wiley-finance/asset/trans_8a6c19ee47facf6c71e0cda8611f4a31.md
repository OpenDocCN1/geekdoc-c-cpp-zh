

# 8.6 C++ 中其他有用的数学函数

本节汇总了一些 C++ 中常用的数学函数，方便参考查阅。我们重点介绍与浮点类型、数值算法和函数相关的函数。这些函数的类别以及每组中主要函数（与浮点变量相关）的描述如下：

- 基本运算：绝对值、最小值和最大值、除法后的余数。
- 指数函数：e^x、2^x、e^x − 1、log x、log10 x、log2 x、log(1 + x)（有些作者用 ln 代替 log）。
- 幂函数：x^y、√x、∛x、√(x² + y²)。
- 三角函数：sin、cos、tan 及其反函数。
- 双曲函数：sinh、cosh、tanh 及其反函数。
- 误差函数和伽马函数：误差函数与互补误差函数、伽马函数以及伽马函数的自然对数。
- 最近整数浮点运算。
- 分类与比较。
- 类型：与浮点除法中商和余数的舍入方向实现无关；哪些基本浮点类型至少与 float 和 double 宽度相同？

上述大多数函数都易于使用，因此除了误差函数、比较函数和少数基本函数外，我们无需举例说明。为方便起见，我们使用 double 作为类型。下面举例说明如何使用这些代码：

```
void Remainder(double x, double y)
{
    std::cout << "Remainder\n";
    // Compute floating-point remainder of x/y
    std::cout << "fmod: " << std::fmod(x, y) << '\n';

    // Compose a float with magnitude of x and sign of y
    std::cout << "copysign: " << std::copysign(x, y) << '\n';

    std::cout << "remainder: " << std::remainder(x, y) << '\n';

    // remquo = remainder+sign of x/y +at least 3 oflast bits of x/y
    int* quadrant = nullptr;
    std::cout << "remquo: " << std::remquo(x, y, quadrant) << '\n';
}
```

```
void BasicOperations(double x, double y, double z)
{
    std::cout << "Basic Operations\n";
    // Fused multiply-add (mostly hardware)
    // Compute (x*y) + z to infinite precision and rounded once
    std::cout << "fma: " << std::fma(x, y, z) << '\n';
    std::cout << "fmax: " << std::fmax(x, y) << '\n';
    std::cout << "fmin: " << std::fmin(x, y) << '\n';
    std::cout << "fdim == max(0, x-y): " << std::fdim(x, y) << '\n';

    // NaN stuff
    auto f = NAN;
    std::cout << std::boolalpha << "is NaN?: " << std::isnan(f);
    std::cout << "fmax: " << std::fmax(f, y) << '\n'; // y
    std::cout << "fmin: " << std::fmin(f, y) << '\n'; // y
}
```

```
void Comparison(double x, double y)
{ // Comparing floating point numbers
// If at least one of the arguments is NaN then result is NaN

std::cout << "Comparison\n";
std::cout << std::boolalpha << "is greater?: "
<< std::isgreater(x,y) << '\n';
std::cout << std::boolalpha << "is greaterequal?: "
<< std::isgreaterequal(x, y) << '\n';

std::cout << std::boolalpha << "is less?: " << std::isless(x, y);
std::cout << std::boolalpha << "is lessequal?: "
<< std::islessequal(x, y) << '\n';

// True if x < y || x > y
std::cout << std::boolalpha << "is lessgreater?: "
<< std::islessgreater(x, y) << '\n';
std::cout << std::boolalpha << "is lessgreater?: "
<< std::islessgreater(x, x) << '\n';

double eps = std::numeric_limits<double>::epsilon();
std::cout << std::boolalpha << "is lessgreater?: "
<< std::islessgreater(x, x + eps) << '\n';
std::cout << std::boolalpha << "is lessgreater?: "
<< std::islessgreater(x, x + 10*eps) << '\n';

// NaN
auto f = NAN;
std::cout << std::boolalpha << "is lessgreater NaN?: "
<< std::islessgreater(x, f) << '\n';

// Can we compare NaNs with normal numbers?
std::cout << std::boolalpha << "is unordered?: "
<< std::isunordered(x, f) << '\n';
std::cout << std::boolalpha << "is unordered?: "
<< std::isunordered(x, y) << '\n';
}
```

```
void ErrorGammaFunctions(double x)
{ // Error and gamma functions

    std::cout << "Error and Gamma functions\n";
    std::cout << "erf: " << std::erf(x) << '\n';
    std::cout << "erfc: " << std::erfc(x) << '\n';

    std::cout << "tgamma: " << std::tgamma(x) << '\n';
    std::cout << "lgamma: " << std::lgamma(x) << '\n';
}
```

测试程序如下：

```
int main()
{
    double x = 5.1; double y = 3.0; double z = 5.3;

    Remainder(x, y);
    BasicOperations(x, y, z);
    Comparison(x, y);
    ErrorGammaFunctions(x);

    return 0;
}
```

该程序的输出为：

```
Remainder

fmod: 2.1
copysign: 5.1
remainder: -0.9
remquo: -0.9

Basic Operations
fma: 20.6
fmax: 5.1
fmin: 3
fdim == max(0, x-y): 2.1
is NaN?: true
fmax: 3
fmin: 3

Comparison
is greater?: true
is greaterequal?: true
is less?: false
is lessequal?: false
is lessgreater?: true
is lessgreater?: false
is lessgreater?: false
is lessgreater?: true
is lessgreater NaN?: false
is unordered?: true
is unordered?: false

Error and Gamma functions
erf: 1
erfc: 5.49382e-13
tgamma: 27.9318
lgamma: 3.32976
```

你可能会在应用程序中发现这些函数很有用，尤其是当你希望提高后者的健壮性时。

## 8.7 创建 C++ 库

本节讨论将编译后的源代码封装为库的若干方法。

### 8.7.1 创建静态 C++ 库

在某个阶段，开发人员可能希望将代码打包为单元或*库*，这些库编写一次并在许多应用程序中重复使用。出于安全原因，开发人员可能不希望分发源代码，而且开发人员的客户可以将静态库链接为其应用程序的一部分，而无需包含非常多的源文件。

本节讨论如何在 Microsoft 的 Visual Studio 中创建*静态库*（关于其他编译器如何实现此操作超出当前范围）。主要步骤是：(1) 创建静态库项目；(2) 向静态库添加类；(3) 构建项目以生成 .lib 文件；(4) 创建控制台可执行项目，引用静态库并在 main 方法中使用其功能。有关更具体的细节，请参阅 Microsoft 在线文档。

我们以一个简单示例来展示创建静态库的机制。我们使用一个包含默认构造函数和多个静态成员函数的类：

```
// StaticLib.hpp

namespace StaticFuncs
{
    class MyStaticFuncs
    {
    public:

        MyStaticFuncs() { }

        // Returns a + b
        static double Add(double a, double b);

        // Returns a - b
        static double Subtract(double a, double b);

        // Returns a * b
        static double Multiply(double a, double b);

        // Returns a / b
        static double Divide(double a, double b);
    };
}
```

```
// StaticLib.cpp
#include "StaticLib.hpp"

#include <stdexcept>

namespace StaticFuncs
{

double MyStaticFuncs::Add(double a, double b)
{
    return a + b;
}

double MyStaticFuncs::Subtract(double a, double b)
{
    return a - b;
}

double MyStaticFuncs::Multiply(double a, double b)
{
    return a * b;
}

double MyStaticFuncs::Divide(double a, double b)
{
    return a / b;
}
}
```

我们将包含此代码的 .cpp 文件添加并构建项目。将生成名为 StaticLib.lib 的文件，并在可执行控制台项目中将其添加为引用。测试代码如下：

```
// TestStaticLib.cpp

#include <iostream>
#include "StaticLib.hpp"

int main()
{
    // Test
    StaticFuncs::MyStaticFuncs f;

    double a = 7.4;
    int b = 99;

    std::cout << "a + b = "
        << StaticFuncs::MyStaticFuncs::Add(a, b) << std::endl;
    std::cout << "a - b = "
        << StaticFuncs::MyStaticFuncs::Subtract(a, b) << std::endl;
    std::cout << "a * b = "
        << StaticFuncs::MyStaticFuncs::Multiply(a, b) << std::endl;
    std::cout << "a / b = "
        << StaticFuncs::MyStaticFuncs::Divide(a, b) << std::endl;

    return 0;
}
```

总之，客户会收到文件 StaticLib.lib 和 StaticLib.hpp，但不会收到 StaticLib.cpp。我们必须告诉编译器库文件的位置，并告知它需要查找的目录。

更一般地说，将可重用的代码封装到库中是有益的。我们可以将相关代码分组到易于使用的函数中，以减少认知负担。此外，我们可以引入检查和异常处理机制，使代码更加健壮。我们举一个使用 C++11 代码且与计算金融应用密切相关的示例。在此情况下，我们将与单变量正态分布函数相关的功能封装起来。我们将在后续章节中更详细地讨论这些代码：

```
// Normal.hpp
//
// Useful normal distribution functionality in one place
//
// (C) Datasim Education BV 2018
//

#include <cstdlib>
#include <random>

namespace Distributions
{
    double PdfNormal(double x); // n(x)

    double CdfNormal(double x); // N(x)

    class NormalDistribution
    { // Test case
    private:
        std::default_random_engine eng;
        std::normal_distribution<double> nor;
```

