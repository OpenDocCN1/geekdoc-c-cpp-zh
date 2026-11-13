

```cpp
#ifndef MATRIX_H
#define MATRIX_H

#include <vector>
using namespace std;

template <typename Object>
class matrix
{
  public:
    matrix( int rows, int cols ) : array( rows )
    {
        for( auto & thisRow : array )
            thisRow.resize( cols );
    }

    matrix( vector< vector< Object > > v ) : array{ v }
    { }

    matrix( vector< vector< Object > > && v ) : array{ std::move( v ) }
    { }

    const vector< Object > & operator[]( int row ) const
    { return array[ row ]; }

    vector< Object > & operator[]( int row )
    { return array[ row ]; }

    int numrows( ) const
    { return array.size( ); }

    int numcols( ) const
    { return numrows( ) ? array[ 0 ].size( ) : 0; }

  private:
    vector< vector< Object > > array;
};
#endif
```

**图 1.26** 一个完整的矩阵类

## 1.7.2 operator[]

operator[] 的思想是，如果我们有一个矩阵 m，那么 m[i] 应该返回与矩阵 m 的第 i 行对应的向量。如果这样做，那么 m[i][j] 将使用普通向量索引给出向量 m[i] 中位置 j 的条目。因此，矩阵 operator[] 返回一个 vector<Object> 而不是一个 Object。

我们现在知道 `operator[]` 应该返回类型为 `vector<Object>` 的实体。我们应该使用按值返回、按引用返回还是按常量引用返回？我们立即排除按值返回，因为返回的实体很大，但调用后保证存在。因此，我们只剩下按引用返回或按常量引用返回。考虑以下方法（忽略别名或大小不兼容的可能性，这两者都不影响算法）：

```
void copy( const matrix<int>& from, matrix<int>& to )
{
    for( int i = 0; i < to.numrows( ); ++i )
        to[ i ] = from[ i ];
}
```

在 copy 函数中，我们试图将矩阵 `from` 中的每一行复制到矩阵 `to` 的对应行中。显然，如果 `operator[]` 返回常量引用，那么 `to[i]` 不能出现在赋值语句的左侧。因此，看起来 `operator[]` 应该返回一个引用。但是，如果我们这样做，那么诸如 `from[i]=to[i]` 这样的表达式将能够编译，因为 `from[i]` 将不是一个常量向量，尽管 `from` 是一个常量矩阵。在良好的设计中，这是不允许的。

所以我们真正需要的是 `operator[]` 对 `from` 返回常量引用，而对 `to` 返回普通引用。换句话说，我们需要两个版本的 `operator[]`，它们仅在返回类型上有所不同。这是不允许的。然而，有一个漏洞：由于成员函数的 const-ness（即函数是访问器还是修改器）是签名的一部分，我们可以让 `operator[]` 的访问器版本返回常量引用，并让修改器版本返回简单引用。这样一切就都没问题了。如图 1.26 所示。

## 1.7.3 Big-Five

这些都会自动处理，因为 `vector` 已经处理好了。因此，这是一个功能完整的 `matrix` 类所需的全部代码。

## 摘要

本章为本书其余部分奠定了基础。算法面对大量输入时所耗费的时间，将是判断其是否为好算法的重要标准。（当然，正确性最为重要。）我们将在下一章开始解决这些问题，并将使用本章讨论的数学来建立形式模型。

## 练习

- 1.1 编写一个程序来解决选择问题。令 k = N/2。绘制一个表格，显示程序在不同 N 值下的运行时间。

- 1.2 编写一个程序来解决单词谜题问题。

- 1.3 编写一个函数，仅使用 `printDigit` 进行 I/O 来输出任意 double 数字（可能是负数）。

- 1.4 C++ 允许以下形式的语句：
  
  ```
  #include filename
  ```
  
  该语句读取 `filename` 并将其内容插入到 `include` 语句的位置。`Include` 语句可以嵌套；换句话说，文件 `filename` 本身可能包含一个 include 语句，但显然，一个文件在任何链中都不能包含它自身。编写一个程序，读取一个文件并输出由 `include` 语句修改后的文件。

- 1.5 编写一个递归函数，返回 N 的二进制表示中 1 的个数。利用这一事实：这等于 N/2 的表示中 1 的个数，如果 N 是奇数，则加 1。

- 1.6 编写具有以下声明的例程：
  
  ```
  void permute( const string & str );
  void permute( const string & str, int low, int high );
  ```
  
  第一个例程是一个驱动程序，它调用第二个例程并打印字符串 str 中字符的所有排列。如果 str 是 "abc"，那么输出的字符串为 abc、acb、bca、bac、cab 和 cba。对第二个例程使用递归。

- 1.7 证明以下公式：
  a. 对于所有 X > 0，log X < X
  b. log(A^B) = B log A

- 1.8 计算以下求和：
  a. \sum_{i=0}^{\infty} \frac{1}{4^i}
  b. \sum_{i=0}^{\infty} \frac{i}{4^i}
  * c. \sum_{i=0}^{\infty} \frac{i^2}{4^i}
  ** d. \sum_{i=0}^{\infty} \frac{i^3}{4^i}

- 1.9 估计
  
  \sum_{i=\lfloor N/2 \rfloor}^{N} \frac{1}{i}

- *1.10 2^{100} (mod 5) 是多少？

- 1.11 设 F_i 为第 1.2 节中定义的斐波那契数。证明以下内容：
  a. \sum_{i=1}^{N} F_i = F_{N+2} - 2
  b. F_N < \phi^N，其中 \phi = (1 + \sqrt{5})/2

- ** 给出 F_N 的精确闭式表达式。

- 1.12 证明以下公式：
  a. \sum_{i=1}^{N} (2i - 1) = N^2
  b. \sum_{i=1}^{N} i^3 = \left( \sum_{i=1}^{N} i \right)^2

- 1.13 设计一个类模板 `Collection`，它存储一个 `Object` 对象的集合（在数组中），以及集合的当前大小。提供 `public` 函数 `isEmpty`、`makeEmpty`、`insert`、`remove`，以及 `contains(x)`，当且仅当集合中存在等于 `x` 的 `Object` 对象时返回 true。

- 1.14 设计一个类模板 `OrderedCollection`，它存储一个 `Comparable` 对象的集合（在数组中），以及集合的当前大小。提供公共函数 `isEmpty`、`makeEmpty`、`insert`、`remove`、`findMin` 和 `findMax`，其中 `findMin` 和 `findMax` 分别返回集合中最小和最大元素的引用。解释如果对空集合执行这些操作可以做什么。

- 1.15 定义一个 `Rectangle` 类，提供 `getLength` 和 `getWidth`。使用图 1.25 中的 `findMax` 例程，编写一个 `main` 函数，创建一个 `Rectangle` 数组，并首先基于面积，然后基于周长找到最大的 `Rectangle`。

- 1.16 对于 `matrix` 类，添加一个 `resize` 成员函数和一个无参构造函数。

## 参考文献

有许多优秀的教材涵盖了本章回顾的数学内容。其中一小部分是 [1]、[2]、[3]、[9]、[14] 和 [16]。参考文献 [9] 专门针对算法分析。它是三卷本系列的第一卷，将在全书中引用。更高级的内容在 [6] 中介绍。

在全书中，我们将假设读者具备 C++ 知识。大部分情况下，[15] 描述了 C++11 的最终草案标准，并且由于它是由 C++ 的原始设计者编写的，仍然是最权威的参考。另一本标准参考书是 [10]。C++ 的高级主题在 [5] 中讨论。两部分系列 [11, 12] 对 C++ 中的许多陷阱进行了精彩的讨论。我们将在全书中调查的标准模板库在 [13] 中有描述。1.4–1.7 节的内容旨在概述我们将在本教材中使用的特性。我们还假设读者熟悉指针和递归（本章中的递归摘要旨在快速复习）。我们将在教材中适当的地方尝试提供关于它们使用的提示。不熟悉这些内容的读者应查阅 [17] 或任何优秀的中级编程教材。

几本书讨论了一般教材风格。一些经典著作是 [4]、[7] 和 [8]。

- 1. M. O. Albertson 和 J. P. Hutchinson, *算法离散数学*, John Wiley & Sons, New York, 1988.
- 2. Z. Bavel, *计算机科学数学伴侣*, Reston Publishing Co., Reston, Va., 1982.
- 3. R. A. Brualdi, *组合数学导论*, 第 5 版, Pearson, Boston, Mass, 2009.
- 4. E. W. Dijkstra, *编程的纪律*, Prentice Hall, Englewood Cliffs, N.J., 1976.
- 5. B. Eckel, *C++ 程序设计思想*, 第 2 版, Prentice Hall, Englewood Cliffs, N.J., 2002.
- 6. R. L. Graham, D. E. Knuth, 和 O. Patashnik, *具体数学*, Addison-Wesley, Reading, Mass., 1989.
- 7. D. Gries, *编程科学*, Springer-Verlag, New York, 1981.

