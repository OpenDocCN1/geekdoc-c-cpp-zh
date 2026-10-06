
以及一个赋值运算符，通常使用 `new` 实例化在栈上。QDateTime、QImage、QString 以及容器类如 QList<T>、QVector<T>、QMap<K, T>。

其他“引用”类型（**reference** type）的类，包括 QObject 及其子类（QWidget、QTimer、QTcpSocket 等）。这些类具有虚函数且不能被复制。例如，QWidget 代表屏幕上一个特定的窗口或控件。如果内存中有 75 个 QWidget 实例，那么在屏幕上也会有 75 个窗口或控件。这些类通常使用 `new` 运算符进行实例化。

## 全局变量和函数

C++ 允许我们声明不属于任何类、且可以从任何其他函数访问的函数和变量。我们已经见过几个全局函数的示例，包括 `main()`，它是程序的入口点。全局变量较为少见，因为它们会损害模块化和线程重入性。但理解它们仍然很重要，因为你可能会在由经过重构的程序员和其他 C++ 用户编写的代码中遇到它们。

为了说明全局函数和变量的工作原理，我们将学习一个小程序，该程序使用一种简单粗暴的算法打印 128 个伪随机数列表。程序的源码分布在两个 .cpp 文件中。

第一个源文件是 random.cpp：

```cpp
int randomNumbers[128];

static int seed = 42;

static int nextNumber(){
  seed = 1009 + (seed * 2011);
  return seed;
}
void populateRandomArray(){
  for (int i = 0; i < 128; ++i)
    randomNumbers[i] = nextNumber();
}
```

该文件声明了两个全局变量（`randomNumbers` 和 `seed`）和两个全局函数（`nextNumber()` 和 `populateRandomArray()`）。其中两个声明包含 `static` 关键字；这些仅在当前编译单元（random.cpp）内可见，被称为静态链接（static linkage）。另外两个可以从程序中的任何编译单元访问；这些具有外部链接（external linkage）。

静态链接对于不应在其他编译单元使用的辅助函数和内部变量来说是理想的。它减少了标识符冲突的风险（在不同编译单元中具有相同名称全局变量或具有相同签名的全局函数），并防止恶意或其他使用不当的用户访问编译单元的内部实现。

现在来看第二个文件 main.cpp，它使用了在 random.cpp 中用外部链接声明的两个全局变量：

```cpp
#include <iostream>

extern int randomNumbers[128];

void populateRandomArray();

int main() {
    populateRandomArray();
    for (int i = 0; i < 128; ++i)
        std::cout << randomNumbers[i] << std::endl;
    return 0;
}
```

我们在调用外部变量和函数之前声明它们。`randomNumbers` 的外部变量声明（在当前编译单元中创建一个外部变量）以 `extern` 关键字开头。如果没有 `extern`，编译器会认为它必须处理一个变量定义，链接器会报错，因为同一个变量在两个编译单元（random.cpp 和 main.cpp）中都被定义了。变量可以声明任意次，但只能定义一次。定义导致编译器为变量预留空间。

`populateRandomArray()` 函数是使用函数原型声明的。对于函数，`extern` 关键字是可选的。

通常，我们会把外部变量和函数的声明放在头文件中，并将其包含在所有需要它们的文件中：

```cpp
#ifndef RANDOM_H
#define RANDOM_H
extern int randomNumbers[128];

void populateRandomArray();
```

我们已经看到如何使用 `static` 来声明不附加到类特定实例的变量和函数，现在我们又看到了如何使用它来声明具有静态链接的函数和变量。`static` 关键字还有一个用法值得顺带提一下。在 C++ 中，我们将局部变量声明为 `static`。此类变量在函数第一次被调用时初始化，并在函数多次调用之间保持其值。例如：

```cpp
void nextPrime()
{
    static int n = 1;

    do {
        ++n;
    } while (!isPrime(n));

    return n;
}
```

静态局部变量与全局变量类似，不同之处在于仅在定义它们的函数内部可见。

## 命名空间（Namespaces）

命名空间是减少 C++ 程序中名称冲突风险的机制。在使用了多个第三方库的大型程序中，名称冲突经常发生。在自己的程序中，你可以选择是否要使用命名空间。

通常，我们会在头文件中所有的声明周围包裹一个命名空间，以确保在该头文件中声明的标识符不会泄漏到全局命名空间。例如：

```cpp
#ifndef SOFTWAREINC_RANDOM_H
#define SOFTWAREINC_RANDOM_H

namespace SoftwareInc
{
    extern int randomNumbers[128];

    void populateRandomArray();
}

#endif
```

（注意，我们还重命名了用于防止重复包含的处理器宏，以减少与同名但位于不同目录的头文件发生名称冲突的风险。）

命名空间的语法与类类似，但它以分号结尾。这里是新的 random.cpp 文件：

```cpp
#include "random.h"
```

```cpp
int SoftwareInc::randomNumbers[128];
static int seed = 42;
static int nextRandomNumber() {
    seed = 1009 + (seed * 2011);
    return seed;
}
```

```cpp
void SoftwareInc::populateRandomArray() {
    for (int i = 0; i < 128; ++i)
        randomNumbers[i] = nextRandomNumber();
}
```

与类不同，命名空间可以任何时候“重新打开”。例如：

```cpp
namespace Alpha {
    void alpha1();
    void alpha2();
}
```

```cpp
namespace Beta {
    void beta1();
}
```

```cpp
namespace Alpha {
    void alpha3();
}
```

这使得在一个命名空间中定义数百个位于许多个头文件中的类成为可能。利用这种技巧，标准 C++ 库将其所有的标识符放在 `std` 命名空间中。在 Qt 中，命名空间用于全局类的标识符，如 `Qt::AlignBottom` `Qt::yellow`。由于历史原因，Qt 类不属于任何命名空间，但以字母 'Q' 为前。

要从命名空间外部引用命名空间中声明的标识符，我们需要加上命名空间的名字（以及 `::`）。或者，我们可以使用以下机制之一，旨在减少我们的击键次数：

- **我们可以定义命名空间别名**

```cpp
namespace PuebloDeLosAngeles
{
    void beverHills();
    void santaMonica();
}

namespace LA = PuebloDeLosAngeles;
```

在别名定义后，可以使用别名代替原始名称。

- **我们可以从命名空间导入单个标识符：**

```cpp
int main()
{
    using PuebloDeLosAngeles::beverHills;
    ...
}
```

`using` 声明允许我们访问命名空间中的给定标识符，而无需加上命名名前缀。

- **我们可以通过一个指令导入整个命名空间：**

```cpp
int main()
{
    using namespace PuebloDeLosAngeles;
    ...
}
```

使用这种方法，更有可能发生名称冲突。如果编译器对模糊名称报错（例如在两个命名空间中定义了相同的类），我们可以始终通过命名空间的名字来限定它。

## C++ 处理器

C++ 处理器是一个程序，它将包含 # 指令（如 `#include`、`#ifdef` 和 `#endif`）的 .cpp 文件转换为不包含指令的文件。处理器对源文件执行文本操作，例如条件编译、文件包含和宏展开。通常，处理器由编译器自动调用，但大多数系统仍提供单独调用它的方法（通常通过 -E 编译器选项）。

- #include 包含尖括号 `<>` 或双引号 `""` 指定的文件内容，取决于头文件是安装在标准位置还是当前项目的一部分。文件名可能包含 `...` 和 `/`（Windows 编译器会正确解释为目录分隔符）。例如：
`#include "../shared/globaldefs.h"`
- #define 定义宏。#define 指令之后出现的宏将被替换为宏的定义。例如，指令
`#define PI 3.14159265359`

告诉处理器将当前编译单元中所有标记 PI 替换为标记 3.14159265359。为了与变量和类名冲突，通常给宏全大写的名称。可以定义带参数的宏：
`#define SQUARE(x) ((x) * (x))`

在宏主体中，将所有出现参数的地方括起来是良好的风格，以及整个主体，以避免运算符优先级的问题。毕竟，我们希望 `7 * SQUARE(2 + 3)` 展开为 `7 ((2 + 3), (2 + 3))`，而不是 `7 + 2 + 3 + 2 + 3`。

C++ 通常允许我们在命令行上定义宏，使用

(img/5a524abdf0b0d58fa99d30abb4463611_1063_0.png)

