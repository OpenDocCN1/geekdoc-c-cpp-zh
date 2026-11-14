

![](img/5682e787fc967e93d7e33e8bac5f58a0_336_0.png)

**图 4-1：STL 容器与算法的互操作性**

要在经典 C 和 Fortran 编程中对 n 种数据结构实现 m 种算法，需要：

m · n 种实现。

使用迭代器时，我们首先需要为所有容器提供接口，但之后每种算法只需一种实现，从而将总编程工作量降低到：

m + n 种实现！

### 4.1.2.1 类别

并非所有算法都可以用于每种数据结构。哪种算法适用于给定的数据结构（例如线性查找或二分查找）取决于容器提供的迭代器类型。迭代器可以按访问形式区分：

- InputIterator：用于读取所引用条目的迭代器概念（仅一次）。

- OutputIterator：用于向所引用条目写入的迭代器概念（仅一次）。

需要注意的是，写入能力并不意味着可读性；例如，`ostream_iterator` 是一个用于向 `cout` 或输出文件等输出流写入的 STL 接口。迭代器的另一种区分方式是遍历形式：

**ForwardIterator：**一种适用于可以从一个元素移动到下一个元素的迭代器的概念，即提供 `operator++` 的类型。它是 `InputIterator` 和 `OutputIterator` 的细化¹。与那些不同，`ForwardIterator` 允许读取值两次并进行多次遍历。

1. 这里的含义见 §3.10。

**BidirectionalIterator：**一种适用于支持逐步前向和后向遍历的迭代器的概念，即同时具有 `operator++` 和 `operator--` 的类型。它细化了 `ForwardIterator`。

**RandomAccessIterator：**一种适用于可以添加任意正或负偏移量的迭代器的概念，即此外还提供 `operator[]` 的类型。它细化了 `BidirectionalIterator`。

仅使用简单迭代器接口（如 `InputIterator` 的接口）的算法实现可以应用于更多的数据结构。反之，提供更丰富迭代器接口（例如建模 `RandomAccessIterator`）的数据结构可以用于更多的算法。

所有迭代器接口的一个巧妙设计选择是，它们的操作也由指针提供。每个指针都建模 `RandomAccessIterator`，因此所有 STL 算法都可以通过指针应用于旧式数组。

### C++11 4.1.2.2 使用迭代器

所有标准容器模板都提供一组丰富且一致的迭代器类型。下面这个非常简单的示例展示了迭代器的典型用法：

点击此处查看代码图片

```cpp
using namespace std;
std::list<int> l= {3, 5, 9, 7};        // C++11
for (list<int>::iterator it= l.begin(); it != l.end(); ++it)
{
    int i= *it;
    cout << i << endl;
}
```

在这个第一个示例中，我们仅限于 C++03 特性（列表初始化除外），以证明使用迭代器在 C++11 中并非新事物。在本节的其余部分，我们将使用更多 C++11 特性，但原理保持不变。

如代码片段所示，迭代器通常成对使用，其中第一个处理实际迭代，第二个标记容器的末尾。迭代器由相应的容器类使用标准方法 `begin()` 和 `end()` 创建。`begin()` 返回的迭代器指向第一个元素，而 `end()` 返回指向元素末尾之后的迭代器。`end` 迭代器仅用于比较，在大多数情况下尝试访问其值会失败。STL 中的所有算法都使用右开区间 [b, e) 实现，对 b 所引用的值进行操作，然后递增直到 b = e。因此，[x, x) 表示一个空区间。成员函数 `begin()` 和 `end()` 保持容器的常量性：

- 如果容器对象是可变的，则这些方法返回指向可变容器条目的 `iterator` 类型。
- 对于常量容器，这些方法返回 `const_iterator`，它通过常量引用访问容器条目。

通常 `iterator` 可以隐式转换为 `const_iterator`，但你不应依赖此特性。回到现代 C++，我们首先为迭代器引入类型推导：

点击此处查看代码图片

```cpp
std::list<int> l= {3, 5, 9, 7};
for (auto it= begin(l), e= end(l); it != e; ++it) {
    int i= *it;
    std::cout << i << std::endl;
}
```

我们还改用 C++11 引入的更符合习惯的 `begin` 和 `end` 自由函数表示法。由于它们是 `inline` 函数，此更改不影响性能。说到性能，我们引入了一个新的临时变量来保存 `end` 迭代器，因为我们无法 100% 确定编译器能否优化对 `end` 函数的重复调用。

虽然在仅读取数据的上下文中我们可以使用 `const_iterator`，但推导出的迭代器允许我们修改所引用的条目。这里有多种方法可以确保循环内不修改列表。一种行不通的方法是 `const auto`：

点击此处查看代码图片

```cpp
for (const auto it = begin(l), e = end(l); ...) // Error
```

这推导出的不是 `const_iterator`，而是 `const iterator`。这是一个微小但重要的区别：前者是指向常量数据的（可变）迭代器，而后者本身是一个常量，因此不能递增。如前所述，`begin()` 和 `end()` 对常量列表返回 `const_iterator`。因此，我们可以将列表声明为常量，但缺点是它只能在构造函数中设置。或者我们可以为该列表定义一个 `const` 引用：

点击此处查看代码图片

```cpp
const std::list<int>& lr = l;
for (auto it = begin(lr), e = end(lr); it != e; ++it) ...
```

或者将列表强制转换为 const 引用：

点击此处查看代码图片

```cpp
for (auto it = begin(const_cast<const std::list<int>&>(l)),
     e = end(const_cast<const std::list<int>&>(l));
     it != e; ++it) ...
```

[C++17] 使用 C++17 函数 `as_const` 可以更轻松地创建 const 引用：

点击此处查看代码图片

```cpp
for (auto it = begin(as_const(l)), e = end(as_const(l));
     it != e; ++it) ...
```

[C++14] 此外，C++11 引入了成员函数 `cbegin` 和 `cend`，它们对常量和可变容器都返回 `const_iterator`。相应的自由函数是在 C++14 中引入的：

点击此处查看代码图片

```cpp
for (auto it = cbegin(l); it != cend(l); ++it) ...
```

这种基于 `begin-end` 的遍历模式如此常见，成为引入基于范围的 `for`（§1.4.4.3）的动机。迄今为止，我们仅将其用于过时的 C 数组，现在很高兴能最终将其应用于真正的容器：

点击此处查看代码图片

```cpp
std::list<int> l = {3, 5, 9, 7};
for (auto i : l)
    std::cout << i << std::endl;
```

循环变量 `i` 是内部使用的遍历整个容器的迭代器的解引用值。因此，`i` 依次指向每个容器条目。由于所有 STL 容器都提供 `begin` 和 `end` 函数，我们可以使用这个简洁的 `for` 循环遍历它们。

[C++17] 为了确保内部使用 `const_iterator`，我们可以对列表应用 `as_const`：

```cpp
for (auto i : as_const(l))
    std::cout << i << std::endl;
```

细心的读者会意识到，在这种情况下差异实际上并不重要，因为我们在此循环中复制了每个条目，但可能存在其他情况，我们希望强制内部使用 `const_iterator`。

更一般地说，我们可以将这个 `for` 循环应用于所有具有返回迭代器的 `begin` 和 `end` 函数的类型：例如表示子容器的类或用于反向遍历返回迭代器的帮助类。这个包含所有容器的更广泛概念称为 *范围*，这也毫不奇怪地是基于范围的 `for` 循环名称的来源。尽管我们在本书中主要在容器上使用它，但值得提及，因为范围在 C++ 演变中日益重要，并最终在 C++20 中成为语言的一部分。为了避免将容器条目复制到 `i` 的开销，我们可以创建一个类型推导的引用：

```cpp
for (auto& i : l)
    std::cout << i << std::endl;
```

引用 `i` 与 `l` 具有相同的常量性：如果 `l` 是可变/常量容器（范围），则引用也是可变/常量的。为了确保条目不能被更改，我们可以声明一个 `const` 引用：
