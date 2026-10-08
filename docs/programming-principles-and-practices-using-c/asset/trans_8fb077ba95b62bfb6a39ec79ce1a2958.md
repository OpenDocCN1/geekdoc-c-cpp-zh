
如果拿不准，就去核实、做实验！不要只是一味地绝望，也不要只是阅读文档。除非你经验丰富，否则很容易误解与数值相关的高度技术性文档。

## 试一试

运行 `g0`。修改 `f0` 以打印出 `c`、`s`、`i` 等。用各种各样的值来测试它。

整数的表示及其转换将在 §25.5.3 中进一步考察。只要有可能，我们倾向于将自己限制在少数几种数据类型上。这有助于最大限度地减少混淆。例如，在一个程序中不使用 `float`，而只使用 `double`，就能消除从 `double` 转换为 `float` 的问题。事实上，我们倾向于将计算仅限于使用 `int`、`double` 和 `complex`（见 §24.9），字符使用 `char`，逻辑实体使用 `bool`。只有迫不得已时，我们才处理其余的算术类型。

### 24.2.1 数值限制

在 `<limits>`、`<climits>`、`<limits.h>` 和 `<float.h>` 中，每种 C++ 实现都指定了内置类型的属性，以便程序员可以使用这些属性来检查限制、设置哨兵值等。这些值列在 §B.9.1 中，对于底层工具构建者来说可能至关重要。如果你认为需要这些值，那你可能离硬件太近了，但它们也有其他用途。例如，对语言实现的某些方面感到好奇（例如“`int` 有多大？”或“`char` 是有符号的吗？”）并不罕见。试图在系统文档中找到确切且正确的答案可能很困难，而且标准只规定了最低要求。然而，编写一个给出答案的程序是非常简单的：

```cpp
cout << "number of bytes in an int: " << sizeof(int) << '\n';
cout << "largest int: " << INT_MAX << '\n';
cout << "smallest int value: " << numeric_limits<int>::min() << '\n';

if (numeric_limits<char>::is_signed)
    cout << "char is signed\n";
else
    cout << "char is unsigned\n";

char ch = numeric_limits<char>::min();       // smallest positive value
cout << "the char with the smallest positive value: " << ch << '\n';
cout << "the int value of the char with the smallest positive value: "
    << int(ch) << '\n';
```

当你编写旨在多种硬件上运行的代码时，向程序提供这类信息偶尔会变得非常有价值。否则，通常的做法是将答案硬编码到程序中，从而带来维护隐患。

当需要检测溢出时，这些限制也可能很有用。

## 24.3 数组

*数组* 是一组元素序列，我们可以按其索引（位置）访问元素。描述这一通用概念的另一个词是 *向量*。这里我们特别关注元素本身也是数组的数组：多维数组。多维数组的一个常用词是 *矩阵*。名称的多样性表明了通用概念的普及程度和实用性。标准的 *vector*（§ B.4）、*array*（§ 20.9）以及内置数组（§ A.8.2）是一维的。那么，如果我们需要两个维度（例如矩阵）怎么办？如果需要七个维度呢？

我们可以像这样将一维和二维数组可视化：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_927_0.png)

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_927_1.png)

数组是大多数计算（“数值处理”）的基础。大多数有趣的科学、工程、统计和金融计算都严重依赖数组。

我们经常将数组视为由行和列组成：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_927_2.png)

一列是具有相同第一个（x）坐标的元素序列。一行是具有相同第二个（y）坐标的元素集合。

## 24.4 C 风格多维数组

C++ 内置数组可以用作多维数组。我们只是将多维数组视为数组的数组，也就是说，以数组为元素的数组。例如：

```cpp
int ai[4];          // 1-dimensional array
double ad[3][4];    // 2-dimensional array
char ac[3][4][5];   // 3-dimensional array
ai[1] = 7;
ad[2][3] = 7.2;
ac[2][3][4] = 'c';
```

这种方法继承了一维数组的优点和缺点：

- 优点
  - 直接映射到硬件
  - 对底层操作效率较高
  - 语言直接支持
- 问题
  - C 风格多维数组是数组的数组（见下文）。
  - 固定大小（即在编译时固定）。如果你想让大小在运行时确定，就必须使用自由存储。
  - 无法干净地传递。数组在稍微有点刺激（provocation）的情况下就会变成指向其第一个元素的指针。
  - 没有范围检查。一如既往，数组不知道自己的大小。
  - 没有数组操作，甚至连赋值（复制）都没有。

内置数组广泛用于数值计算。它们也是*主要*的 bug 和复杂性来源。对大多数人来说，编写和调试它们非常痛苦。如果你被迫使用它们（例如，在 *The C++ Programming Language* 中查找）。不幸的是，C++ 与 C 共享其多维数组，所以有很多代码“在外面”使用它们。

最根本的问题是你不能干净地传递多维数组，因此你不得不退回到使用指针并在多维数组中显式计算位置。例如：

```cpp
void f1(int a[3][5]);              // useful for [3][5] matrices only

void f2(int [ ] [5], int dim1);    // 1st dimension can be a variable

void f3(int [5] [ ], int dim2);    // error: 2nd dimension cannot be a variable

void f4(int [ ], int dim1, int dim2);  // error (and wouldn't work anyway)

void f5(int* m, int dim1, int dim2)    // odd, but works
{
    for (int i=0; i<dim1; ++i)
        for (int j = 0; j<dim2; ++j) m[i*dim2+j] = 0;
}
```

在这里，尽管 `m` 是一个二维数组，但我们将其作为 `int*` 传递。只要第二维需要是变量（参数），实际上就没有办法告诉编译器 `m` 是一个（`dim1`，`dim2`）数组，所以我们只是传递指向存储它的内存起始位置的指针。表达式 `m[i*dim2+j]` 实际上意味着 `m[i,j]`，但因为编译器不知道 `m` 是一个二维数组，我们必须计算 `m[i,j]` 在内存中的位置。

这在我们看来过于复杂、原始且容易出错。它也可能很慢，因为显式计算元素位置会使优化复杂化。与其尝试教你所有相关知识，我们将专注于一个 C++ 库，该库消除了内置数组的问题。

## 24.5 **矩阵库**

对于面向数值计算的数组/矩阵，我们想要的基本“事物”是什么？

- “我的代码应该看起来非常像我在数学/工程教科书中关于数组的内容。”
  - 或者关于向量、矩阵、张量。
- 编译时和运行时检查。
- 任意维度的数组。
- 具有任意元素数量的维度。
- 数组是合适的变量/对象。
  - 你可以随意传递它们。
- 常规数组操作：
  - 下标索引：()
  - 切片：[]
  - 赋值：=
  - 标量运算（+=, -=, *=, %= 等）
  - 融合向量操作（例如，res[i] = a[i]\*c+b[i]）
  - 点积（res = a[i]\*b[i] 之和；也称为 inner_product()）
- 基本上，将传统的数组/向量表示法转换为你不得不费力自己编写的代码（并且运行效率至少等同于该代码）。
  - 你可以根据需要自行扩展（其实现中没有使用“魔法”）。

矩阵库做到了这些，并且仅做这些。如果你想要更多，例如高级数组函数、稀疏数组、内存布局控制等，你必须自己编写它，或者（最好）使用一个更能近似满足你需求的库。然而，许多这样的需求可以通过在 Matrix 之上构建算法和数据结构来满足。Matrix 库不是 ISO C++ 标准库的一部分。你可以在书籍支持站点找到 Matrix.h。它在命名空间 Numeric_lib 中定义了其功能。我们选择“matrix”这个名字，因为“vector”和“array”在 C++ 库中被使用得更为频繁。matrix 的复数形式是 matrices（matrice s 是更罕见的形式）。当 Matrix 指代 C++ 语言实体时，我们将使用 Matrices 作为复数形式以避免混淆。Matrix 库的实现使用了高级技术，此处不作描述。

### 24.5.1 维度和访问

考虑一个简单的例子：

```cpp
#include "Matrix.h"
using namespace Numeric_lib;

void f(int n1, int n2, int n3)
{
    Matrix<double,1> ad1(n1);  // elements are doubles; one dimension
    Matrix<int,1> a11(n1);     // elements are ints; one dimension
    ad1(7) = 0;                // subscript using () -- Fortran style
    ad1[7] = 8;                // [] also works -- C style
}
```

