

```cpp
double& operator[](int i);
int size();
```

private:

```cpp
double* elem; // elem 指向一个大小为 sz 的元素数组
int sz;
```

这里的关键点是函数体（即函数定义）可以位于“别处”。对于这个示例，我们可能希望 Vector 的表示也位于“别处”，我们稍后会处理这一点（抽象类型）；§5.3。`sqrt(t)` 的定义看起来如下：

点击此处查看代码图片

```cpp
double sqrt(double d)    // sqrt(t) 的定义
{
    // ... 数学教科书中的算法 ...
}
```

对于 Vector，我们需要定义所有的成员函数：

点击此处查看代码图片

```cpp
Vector::Vector(int s)        // 构造函数的定义
    elem(new double[s]), sz(s)
{
    // 成员
}
```

```cpp
double& Vector::operator[](int i)    // 下标运算符的定义
{
    return elem[i];
}
```

```cpp
int Vector::size()            // size() 的定义
{
    return sz;
}
```

我们必须定义 Vector 的函数，但不需要定义 sqrt(t)，因为它是标准库的一部分。
然而，这并没有本质区别：库仅仅是“我们恰好使用的某些代码”，并且是用与我们相同的语言编写的。
一个实体（如函数）可以有多个声明，但只能有一个定义。

# 3.2 独立编译

C++ 支持“独立编译”的概念，用户代码只看到所用类型和函数的声明。这可以通过两种方式实现：

- *头文件 (§3.2.1)*：将声明放在单独的文件中（称为头文件），并在需要声明的地方通过文本形式 #include 头文件。
- *模块 (§3.2.2)*：定义模块文件，单独对它们进行编译，并并在需要的地方导入（import）它们。只有被显式导出的声明才能被导入模块的代码可见。

这两种方法任其一都可以用于将程序组织成一组半独立的代码片段。这种分离可以用来缩短编译时间，并强制执行程序中逻辑上不同部分之间的分离（从而减少错误概率）。库通常是一系列独立编译的代码片段（例如函数）的集合。
用于组织代码的头文件技术追溯到 C 语言的早期，目前仍然是最常用的方法。模块的使用在 C++20 中引入，在代码整洁和编译时间方面提供了巨大的优势。

# 3.2.1 头文件

传统上，我们将指定某个我们认为是模块的代码块接口的声明放在一个文件中，文件名指示其预期用途。例如：

点击此处查看代码图片

// Vector.h:

```cpp
class Vector {
public:
    Vector(int s);
    double& operator[](int i);
    int size();
private:
    double* elem;
    int sz;
};
```

该声明将被放置在 Vector.h 文件中。用户 #include 该文件（称为头文件）以访问接口。例如：

点击此处查看代码图片

// user.cpp:

```cpp
#include "Vector.h" // 获取 Vector 的接口
#include <cmath> // 获取标准库数学函数接口，包括 sqrt()
double sqrt_sum(const Vector& v) {
    double sum = 0;
    for (int i = 0; i < v.size(); ++i)
        sum += sqrt(v[i]); // 根之和
    return sum;
}
```

为了帮助编译器确保一致性，提供 Vector 实现的 .cpp 文件也包含了提供其接口的 .h 文件：

点击此处查看代码图片

// Vector.cpp:

```cpp
#include "Vector.h" // 获取 Vector 的接口
Vector::Vector(int s)
    : elem(new double[s]), sz(s) {} // 初始化成员

double& Vector::operator[](int i)
{
    return elem[i];
}

int Vector::size()
{
    return sz;
}
```

user.cpp 和 Vector.cpp 中的代码共享 Vector.h 中提供的 Vector 接口，但这两个文件在其他方面是独立的，并且可以独立编译。从图示上看，程序片段表示如下：

# Vector.h:
![](img/0bd2e5eba2737c5daca16fad_0.png)

# user.cpp:
```cpp
#include "Vector.h" // 使用 Vector
```

# Vector.cpp:
```cpp
#include "Vector.h" // 定义 Vector
```

程序组织的最佳方法是将其视为一组具有定义依赖关系的模块。头文件通过文件表示了这种模块化，并通过独立编译利用了模块化。一个单独编译的文件（包括头文件）被称为编译单元。一个程序可以由数千个编译单元组成。

使用头文件和 #include 是一种模拟模块化的非常旧的方法，具有显著的缺点：

- 编译时间：你在数千个编译单元中 #include header.h，header.h 的文本将被编译器处理。
- 顺序依赖：如果你在 #include header2.h 之前包含 header1.h，header1.h 中的声明和宏可能会影响 header2.h 中代码的含义。如果你在 #include header1.h 之前包含 header2.h，那么可能是 header2.h 影响 header1.h 中的代码。
- 不一致性：在一个文件中定义实体（如类型或函数），而在另一个文件中以不同的方式定义它，可能会导致崩溃或微妙的错误。当你——无论无意还是故意——在两个文件中分别声明一个实体，而不是将其放在头文件中时，就会发生这种情况。
- 传递性：所有需要访问头文件中声明的代码都必须存在于该头文件中。这导致头文件的使用者——无论无意还是故意——变得依赖于实现细节。

显然，这不是理想的，这种技术自 20 世纪 70 年代初引入 C 语言以来，一直是成本和错误的主要来源。然而，头文件的使用已经持续多年，且到目前为止它仍然远胜其他常见的方法。

# 3.2.2 模块

在 C++20 中，我们有一种原生支持的方式来表达模块化（19.4）。考虑使用模块表达 §3.2 的 Vector 示例：

点击此处查看代码图片

```cpp
export module Vector // 定义名为 "Vector" 的模块

export class Vector {
public:
    Vector(int s);
    double& operator[](int i);
    int size();
private:
    double* elem; // elem 指向一个大小为 sz 的元素数组
    int sz;
};
```

```cpp
Vector::Vector(int s)        // 构造函数的定义
    : elem(new double[s]), sz(s)
{} // 初始化成员

double& Vector::operator[](int i)
{
    return elem[i];
}

int Vector::size()
{
    return sz;
}

export bool operator==(const Vector& v1, const Vector& v2) {
    if (v1.size() != v2.size())
        return false;
    for (int i = 0; i < v1.size(); ++i) {
        if (v1.elem[i] != v2.elem[i])
            return false;
    }
    return true;
}
```

这代码定义了一个名为 Vector 的模块，它导出了类 Vector、它的成员函数以及非成员函数 ==。

我们使用这种模块的方法是在需要的地方导入它。例如：

点击此处查看代码图片

// user.cpp:

```cpp
import Vector;      // 获取 Vector 的接口
#include <cmath>     // 获取标准库数学函数接口，包括 sqrt()

double sqrt_sum(Vector& v) {
    double sum = 0;
    for (int i = 0; i < v.size(); ++i)
        sum += sqrt(v[i]); // 根之和
    return sum;
}
```

头文件和模块的区别在于它们只编译一次（而不是在每个编译单元中重复编译）：

- 模块只编译一次（而不是在每个编译单元中重复编译）。
- 两个模块可以按任何顺序导入而不改变其含义。
- 如果你导入或包含某些内容到模块，导入模块的用户不会隐式地获得所有内容：导入不是传递的。

这对可维护性和编译时间的影响可能是惊人的。例如，我测量出使用 import std; 编译“Hello, World!”程序的速度比使用 #include<iostream> 的版本快 10 倍。尽管 module std 包含了整个标准库，信息比 <iostream> 头文件多出 10 倍，但这仍然实现了。原因是模块只导出接口，而头文件将所有内容直接或间接地传递给编译器。

遗憾的是，C++20 没有 module std。如果标准库实现尚未提供它，附录 A 解释了如何获取 module std。

定义模块时，我们不需要将声明和定义分离在不同的文件中；如果我们可以导入我们的源码组织方式，但我们没有这样做。我们可以这样定义简单的 Vector 模块：

点击此处查看代码图片

```cpp
export class Vector; // 定义名为 "Vector" 的模块
export class Vector (
    // ...
);
```

