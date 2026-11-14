

- 4. 两种类型都完全已知，我们可以将此指针静态向下转型为 point*。
- 5. 由于我们知道 inequality<point> 的 this 指针是向上转型为 point 的 this 指针，因此将其向下转型回其原始类型是安全的。
- 6. point 的相等运算符被调用并实例化（如果之前未完成）。

每个带有相等运算符的类 U 都可以以相同方式从 inequality<U> 派生。由 Jeremy Siek 和 David Abrahams 提供的 Boost.Operators 提供了一组此类用于运算符默认实现的 CRTP 模板。

### 6.6.2 可复用的访问运算符

```
=> c++11/matrix_crtp_example.cpp
```

CRTP 惯用法使我们能够解决之前提到的一个问题（§2.6.4）：使用可复用实现的方括号运算符访问多维数据结构。当时我们不知道所需的语言特性，尤其是模板和继承。现在我们知道了，并将运用这些知识，通过一个二元调用运算符实现两个方括号运算符调用，即将 A[i][j] 求值为 A(i, j)。

假设我们有一个名为 some_matrix 的优雅矩阵类型，其 operator() 仅访问 a_ij。为与向量表示法保持一致，我们更倾向于使用方括号运算符。它们只接受一个参数，因此我们需要一个代表对矩阵行访问的代理。该代理反过来提供一个方括号运算符，用于访问对应行中的列，即产生矩阵的一个元素：

```
class some_matrix; // Forward declaration

class simple_bracket_proxy
{
public:
    simple_bracket_proxy(some_matrix& A, size_t r) : A(A), r(r) {}

    double& operator[](size_t c){ return A(r, c); } // Error
private:
    some_matrix& A;
    size_t r;
};

class some_matrix
{
// ...

    double& operator()(size_t r, size_t c) { ... }

    simple_bracket_proxy operator[](size_t r)
    {
        return simple_bracket_proxy(*this, r);
    }
};
```

其思想是 A[i] 返回一个指代 A 并包含 i 的代理 p。调用 A[i][j] 对应于 p[j]，而 p[j] 反过来应调用 A(i, j)。不幸的是，此代码无法编译。当我们在 simple_bracket_proxy::operator[] 中调用 some_matrix::operator() 时，some_matrix 类型仅被声明而未完全定义。互换两个类定义只会反转依赖关系并导致更多无法编译的代码。此代理实现的问题是我们需要两个相互依赖的完整类型。

这是模板的一个有趣方面：由于其延迟代码生成，它们允许我们打破相互依赖。向代理添加模板参数可消除依赖：

```cpp
template <typename Matrix, typename Result>
class bracket_proxy
{
public:
    bracket_proxy(Matrix& A, size_t r) : A(A), r(r) {}

    Result& operator[](size_t c){ return A(r, c); }

private:
    Matrix& A;
    size_t r;
};

class some_matrix
{
    // ...
    bracket_proxy<some_matrix, double> operator[](size_t r)
    {
        return bracket_proxy<some_matrix, double>(*this, r);
    }
};
```

最后，我们可以编写 A[i][j]，并在内部通过两参数应用运算符执行它。现在我们可以编写许多具有完全不同的 operator() 实现的矩阵类，并且它们都可以以完全相同的方式部署 bracket_proxy。

在实现了多个矩阵类后，我们发现所有矩阵类中的 operator[] 看起来都非常相似：只是返回一个带有矩阵引用和行参数的代理。我们可以添加另一个 CRTP 类，仅实现一次此方括号运算符：

```cpp
template <typename Matrix, typename Result>
class bracket_proxy { ... };

template <typename Matrix, typename Result>
class crtp_matrix
{
    using const_proxy = bracket_proxy<const Matrix, const Result>;

public:
    bracket_proxy<Matrix, Result> operator[](size_t r)
    {
        return {static_cast<Matrix&>(*this), r};
    }

    const_proxy operator[](size_t r) const
    {
        return {static_cast<const Matrix&>(*this), r};
    }
};
class matrix
: public crtp_matrix<matrix, double>
{
    // ...
};
```

请注意，C++11 特性仅用于简洁；我们也可以用 C++03 实现此代码，只是会多一些冗长。此 CRTP 矩阵类可以为每个带有双参数应用运算符的矩阵类提供方括号运算符。然而，在功能齐全的线性代数包中，我们需要注意哪些矩阵是可变的，以及返回的是引用还是值。这些区别可以使用第 5 章中的元编程技术安全地处理。

尽管代理方法会创建一个额外对象，但我们的基准测试表明，方括号运算符的使用速度与应用运算符一样快。显然，现代编译器中精巧的引用转发可以消除代理的实际创建。

## 6.7 练习

### 6.7.1 非冗余菱形

实现第 6.3.2 节中的菱形，使名称仅打印一次。在派生类中区分 all_info() 和 my_info() 并适当调用这两个函数。

### 6.7.2 继承向量类

修订第 2 章中的向量示例。引入基类 vector_expression 用于 size 和 operator()。使 vector 从此基类继承。然后创建一个类 ones，它是一个全为 1 的向量，并且也从 vector_expression 继承。

### 6.7.3 克隆函数

为名为 clone() 的成员函数编写一个 CRTP 类，该函数复制当前对象——类似于 Java 的 clone 函数（http://en.wikipedia.org/wiki/Clone_%28Java_method%29）。请注意，该函数的返回类型必须是克隆对象的类型。

## 第 7 章
科学项目

在前几章中，我们主要关注 C++ 的语言特性以及如何将它们最好地应用于相对较小的学习示例。本章最后一章应为您提供构建大型项目的一些思路。第一节（§7.1）由作者的朋友 Mario Mulansky 撰写，讨论了库之间互操作性的主题。它将让您一窥 odeint 的内部工作原理：一个与多个其他库以非常紧密的方式无缝互操作的通用库。然后，我们将介绍如何从许多程序源和库存档构建可执行文件（§7.2.1）以及工具如何支持此过程（§7.2.2）。最后，我们讨论如何将程序源适当地分布到多个文件中（§7.2.3）。

### 7.1 ODE 求解器的实现

Mario Mulansky 撰写

在本节中，我们将介绍设计数值库的主要步骤。这里的重点不是提供最完整的数值功能，而是达到一种确保最大通用性的稳健设计。作为示例，我们将考虑用于求解常微分方程（ODE）的数值算法。遵循第 3 章的精神，我们的目标是通过使用泛型编程使实现尽可能通用。我们首先简要介绍算法的数学背景，然后给出一个简单直接的实现。从此，我们将能够识别实现的各个部分，并逐一使其可交换，从而达到一个完全通用的库。我们相信，在学习了这个通用库设计的详细示例后，读者将能够将此技术应用于其他数值算法。

### 7.1.1 常微分方程

常微分方程是建模物理、生物、化学或社会过程的基本数学工具，也是科学和工程中最重要的概念之一。除了少数简单情况外，ODE 的解无法通过解析方法找到，我们必须依赖数值算法来获得至少一个近似解。在本章中，我们将开发 Runge-Kutta-4 算法的通用实现，这是一种通用 ODE 求解器，因其简单性和鲁棒性而被广泛使用。

