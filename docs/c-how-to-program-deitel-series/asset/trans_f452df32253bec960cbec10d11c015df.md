

## 16 标准库算法

> 历史学家是反向的先知。
>
> ——弗里德里希·冯·施莱格尔

> 坚持到底，切勿犹疑观望；世上无难事，只怕有心人。
>
> ——罗伯特·赫里克

### 目标

在本章中，你将：

- 使用数十种标准库算法进行编程。
- 将迭代器与算法结合，访问并操作标准库容器中的元素。
- 将函数指针、函数对象和 lambda 表达式传入标准库算法。

![](img/b42ba5cd262b1358d16610173f975e4d_725_0.png)

![](img/b42ba5cd262b1358d16610173f975e4d_726_0.png)

- 16.1 引言
- 16.2 迭代器的最低要求
- 16.3 算法
    - 16.3.1 `fill`、`fill_n`、`generate` 和 `generate_n`
    - 16.3.2 `equal`、`mismatch` 和 `lexicographical_compare`
    - 16.3.3 `remove`、`remove_if`、`remove_copy` 和 `remove_copy_if`
    - 16.3.4 `replace`、`replace_if`、`replace_copy` 和 `replace_copy_if`
    - 16.3.5 数学算法
    - 16.3.6 基本查找与排序算法
    - 16.3.7 `swap`、`iter_swap` 和 `swap_ranges`
    - 16.3.8 `copy_backward`、`merge`、`unique` 和 `reverse`
    - 16.3.9 `inplace_merge`、`unique_copy` 和 `reverse_copy`
    - 16.3.10 集合运算
    - 16.3.11 `lower_bound`、`upper_bound` 和 `equal_range`
    - 16.3.12 堆排序
    - 16.3.13 `min`、`max`、`minmax` 和 `minmax_element`
- 16.4 函数对象
- 16.5 Lambda 表达式
- 16.6 标准库算法总结
- 16.7 本章小结

摘要 | 自测练习 | 自测练习答案 | 练习

### 16.1 引言

本章继续讨论标准库的容器、迭代器和算法，重点介绍执行常见数据操作的算法，例如*搜索*、*排序*以及*比较元素或整个容器*。标准库提供了 90 多种算法，其中许多是 C++11 新增的。完整列表可在 C++ 标准文档的第 25 节和第 26.7 节中找到，同时也有各种在线参考资料可以了解每种算法，例如 en.cppreference.com/w/cpp/algorithm。大多数算法使用迭代器访问容器元素。你会看到，各种算法可以接收*函数指针*（指向函数代码的指针）作为参数。此类算法使用该指针调用函数——通常以一个或两个容器元素作为参数。本章将更详细地介绍函数指针。在本章后面，我们将介绍*函数对象*的概念，它类似于函数指针，但实现为具有重载的函数调用运算符（`operator()`）的类的对象，因此该对象可以像函数名一样使用。最后，我们将介绍 *lambda 表达式*——C++11 中用于创建*匿名函数对象*（即没有名称的函数对象）的新简写机制。

### 16.2 迭代器的最低要求

除少数例外情况外，标准库将算法与容器分离。这使得添加新算法变得更加容易。每个容器的一个重要特征是其支持的迭代器类型（图 15.7）。这决定了哪些算法可以应用于该容器。例如，vector 和 array 都支持*随机访问迭代器*，它们提供了图 15.9 中显示的所有迭代器操作。所有标准库算法都可以操作 vector，而那些不修改容器大小的算法也可以操作 array。每个接受迭代器参数的标准库算法都要求这些迭代器提供最低级别的功能。例如，如果某个算法需要*前向迭代器*，那么该算法可以操作任何支持*前向迭代器*、*双向迭代器*或*随机访问迭代器*的容器。

![](img/b42ba5cd262b1358d16610173f975e4d_727_0.png)

**软件工程观察 16.1**

标准库算法不依赖于其所操作的容器的实现细节。只要容器（或内置数组）的迭代器满足算法的要求，该算法就可以在该容器上工作。

![](img/b42ba5cd262b1358d16610173f975e4d_727_1.png)

**可移植性提示 16.1**

由于标准库算法仅通过迭代器间接处理容器，因此一种算法通常可以用于许多不同的容器。

![](img/b42ba5cd262b1358d16610173f975e4d_727_2.png)

**软件工程观察 16.2**

标准库容器实现简洁。算法与容器分离，仅通过迭代器间接操作容器中的元素。这种分离使得编写适用于各种容器类的泛型算法更加容易。

![](img/b42ba5cd262b1358d16610173f975e4d_727_3.png)

**软件工程观察 16.3**

使用能够产生可接受性能的“最弱迭代器”有助于生成最大程度可重用的组件。例如，如果某个算法只需要前向迭代器，那么它可以与任何支持前向迭代器、双向迭代器或随机访问迭代器的容器一起使用。然而，需要随机访问迭代器的算法只能用于具有随机访问迭代器的容器。

#### 迭代器失效

迭代器只是指向容器元素，因此当发生某些容器修改时，迭代器可能变得无效。例如，如果对 vector 调用 clear，则其所有元素都会被移除。如果在调用 clear 之前程序有指向该 vector 元素的任何迭代器，那么这些迭代器现在将无效。C++ 标准的第 23 节讨论了每个标准库容器中迭代器（以及指针和引用）失效的所有情况。此处我们总结在 insert 和 erase 操作期间迭代器何时失效。

向以下容器插入时：

- **vector**——如果 vector 被重新分配，则指向该 vector 的所有迭代器都会失效。否则，从插入点到 vector 末尾的迭代器都会失效。
- **deque**——所有迭代器都会失效。
- **list 或 forward_list**——所有迭代器*保持有效*。
- **有序关联容器**——所有迭代器*保持有效*。
- **无序关联容器**——如果需要重新分配容器，则所有迭代器都会失效。

从容器中删除元素时，指向已删除元素的迭代器会失效。此外：

- **vector**——从被删除元素到 vector 末尾的迭代器都会失效。
- **deque**——如果删除了 deque 中间的元素，则所有迭代器都会失效。

### 16.3 算法

第 16.3.1 节至第 16.3.13 节演示了许多标准库算法。

#### 16.3.1 fill、fill_n、generate 和 generate_n

图 16.1 演示了算法 fill、fill_n、generate 和 generate_n。算法 fill 和 fill_n 将容器元素范围内的每个元素设置为特定值。算法 generate 和 generate_n 使用生成器函数为容器元素范围内的每个元素创建值。生成器函数不接受参数，并返回一个可以放入容器元素中的值。

```cpp
// Fig. 16.1: Fig16_01.cpp
// Algorithms fill, fill_n, generate and generate_n.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <array> // array class-template definition
#include <iterator> // ostream_iterator
using namespace std;

char nextLetter(); // prototype of generator function

int main()
{
   array<char, 10> chars;
   ostream_iterator<char> output(cout, " ");
   fill(chars.begin(), chars.end(), '5'); // fill chars with 5s

   cout << "chars after filling with 5s:\n";
   copy(chars.cbegin(), chars.cend(), output);

   // fill first five elements of chars with As
   fill_n(chars.begin(), 5, 'A');

   cout << "\n\nchars after filling five elements with As:\n";
   copy(chars.cbegin(), chars.cend(), output);

   // generate values for all elements of chars with nextLetter
   generate(chars.begin(), chars.end(), nextLetter);

   cout << "\n\nchars after generating letters A-J:\n";
   copy(chars.cbegin(), chars.cend(), output);

   // generate values for first five elements of chars with nextLetter
   generate_n(chars.begin(), 5, nextLetter);

   cout << "\n\nchars after generating K-O for the"
        << " first five elements:\n";
   copy(chars.cbegin(), chars.cend(), output);
   cout << endl;
} // end main
```

**图 16.1** | 算法 fill、fill_n、generate 和 generate_n。（第 1 部分，共 2 部分。）

