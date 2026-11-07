
第30行解引用 `constIterator` 以获取当前元素的值。请记住，迭代器的作用类似于指向元素的指针，并且运算符 `*` 被重载以返回对该元素的引用。表达式 `++constIterator`（第29行）将迭代器定位到 vector 的下一个元素。你可以将这段循环替换为以下更直接的基于范围的 `for` 语句：

```cpp
for (auto const& item : integers) {
    std::cout << item << ' ';
}
```

基于范围的 `for` 在“底层”使用迭代器。

### 使用 const_reverse_iterators 反向显示 vector 的内容

第36–39行反向遍历 vector。vector 的成员函数 `crbegin` 和 `crend` 分别返回 `const_reverse_iterator`，表示反向遍历容器时的起始点和结束点。大多数序列容器和有序关联容器支持反向迭代。类 `vector` 还提供成员函数 `rbegin` 和 `rend` 来获得非 `const` 的 `reverse_iterator`。

```cpp
33        std::cout << "\nOutput integers in reverse using iterators: ";
34
35        // display vector in reverse order using const_reverse_iterator
36        for (auto reverseIterator{integers.crbegin()};
37             reverseIterator != integers.crend(); ++reverseIterator) {
38           std::cout << *reverseIterator << ' ';
39        }
40
41        std::cout << "\n";
42    }
```

```text
Output integers in reverse using iterators: 10 9 8 7 6 5 4 3 2 1
```

### shrink_to_fit

你可以调用成员函数 `shrink_to_fit`，请求 vector 或 deque 将不需要的内存归还给系统，将其容量缩减到容器当前元素数量。根据 C++ 标准，实现可以忽略此请求，以便执行特定于实现的优化。

## 13.8.2 vector 元素操作函数

图13.3 展示了用于获取和操作 vector 元素的函数。第12行使用花括号初始化器初始化一个 `vector<int>`。在本例中，我们将 vector 的类型声明为 `std::vector`。编译器使用类模板实参推导（CTAD）从初始化列表中的 `int` 值推断元素类型。第13行使用一个接受两个迭代器作为实参的 vector 构造函数，用范围 `values.cbegin()` 到但不包括 `values.cend()` 中元素的副本初始化其元素。

```cpp
// fig13_03.cpp
// Testing standard library vector class template
// element-manipulation functions.
#include <algorithm> // copy algorithm
#include <format>
#include <iostream>
#include <ranges>
#include <iterator> // ostream_iterator iterator
#include <vector>

int main() {
   std::vector values{1, 2, 3, 4, 5}; // class template argument deduction
   std::vector<int> integers{values.cbegin(), values.cend()};
   std::ostream_iterator<int> output{std::cout, " "};
}
```

**图 13.3** | vector 容器元素操作函数。

### ostream_iterator

第14行定义了一个名为 output 的 ostream_iterator，可用于通过 cout 输出以单个空格分隔的整数。`ostream_iterator<int>` 只输出 `int` 类型的值。构造函数的第一个实参指定输出流，第二个实参是指定输出值分隔符的字符串——在本例中是一个空格字符。本例中我们使用 `ostream_iterator`（头文件 `<iterator>`）输出 vector 的内容。

### copy 算法

第17行使用标准库算法 `copy`（头文件 `<algorithm>`）将 `integers` 的内容输出到标准输出。该版本的算法接受三个实参。前两个是指定从 vector `integers` 复制哪些元素的迭代器——从 `integers.cbegin()` 到但不包括 `integers.cend()`。它们必须满足输入迭代器要求，例如 `const_iterator`，从而能够从容器读取值。它们还必须引用同一个容器，以便对第一个迭代器反复应用 `++` 最终会到达第二个迭代器实参。第三个实参指定将元素复制到哪里。它必须是一个输出迭代器，可以通过它存储或输出值。输出迭代器是附加到 `cout` 的 `ostream_iterator`，因此第17行将元素复制到标准输出。

```cpp
std::cout << "integers contains: ";
std::copy(integers.cbegin(), integers.cend(), output);
```

```text
integers contains: 1 2 3 4 5
```

### 公共范围

在 C++20 之前，容器元素的“范围”由指定起始位置和末尾后一位置的迭代器来描述，通常通过调用容器的 `begin` 和 `end`（或类似）成员函数来实现。从 C++20 起，C++ 标准将此类范围称为公共范围，以免与 C++20 ranges 混淆。此后，在讨论由两个迭代器确定的范围时，我们将使用术语“公共范围”，而在讨论 C++20 ranges 时使用术语“range”。

### vector 成员函数 `front` 和 `back`

第19–20行通过成员函数 `front` 和 `back` 获取 vector 的第一个和最后一个元素，大多数序列容器都提供这些函数。注意函数 `front` 与 `begin` 的区别。函数 `front` 返回对 vector 第一个元素的引用，而函数 `begin` 返回指向 vector 第一个元素的迭代器。类似地，函数 `back` 返回对 vector 最后一个元素的引用，而 `end` 返回指向最后一个元素之后位置的迭代器。对空 vector 调用 `front` 和 `back` 的结果是未定义的。

```cpp
std::cout << std::format("\nfront: {}\nback: {}\n",
    integers.front(), integers.back());
```

```text
front: 1
back: 5
```

### 访问 vector 元素

第22–23行展示了访问 vector（或 deque）元素的两种方式。第22行使用 `[]` 运算符，它返回对指定位置值的引用，或返回对该 const 值的引用，取决于容器是否为 const。函数 `at`（第23行）执行相同操作，但会进行边界检查。`at` 成员函数首先检查其实参并确定它是否在 vector 的边界内。如果不在，`at` 函数会抛出 `out_of_range` 异常，如第6.15节所示。

```cpp
integers[0] = 7;  // set first element to 7
integers.at(2) = 10; // set element at position 2 to 10
```

### vector 成员函数 `insert`

第26行使用了每个序列容器提供的若干重载 `insert` 成员函数之一（`array` 大小固定，`forward_list` 改用函数 `insert_after`，二者除外）。第26行将值22插入到第一个实参中迭代器指定位置处的元素之前。这里，迭代器指向第二个元素，因此22成为第二个元素，原来的第二个元素现在成为第三个。`insert` 的其他版本允许

- 从给定位置开始插入同一值的多个副本，或
- 从给定位置开始插入来自另一个容器的一段值。

第26行中的 `insert` 版本返回一个指向所插入项的迭代器。

```cpp
// insert 22 as second element
integers.insert(integers.cbegin() + 1, 22);

std::cout << "Contents of vector integers after changes: ";
std::ranges::copy(integers, output);
```

```text
Contents of vector integers after changes: 7 22 2 10 4 5
```

### C++20 ranges 算法 `copy`

第29行使用 `std::ranges` 命名空间中的 C++20 `copy` 算法将 `integers` 的元素复制到标准输出。该版本的 `copy` 仅接收要复制的范围以及表示将范围元素复制到何处的输出迭代器。第一个实参是表示元素范围的对象，其输入迭代器表示该范围的开始和结束——在本例中是一个 vector。`<algorithm>` 头文件中大多数 C++20 之前的算法现在在 `std::ranges` 命名空间中都有 C++20 ranges 版本。`std::ranges` 算法通常重载为一个接受范围对象的版本和一个接受迭代器与哨兵的版本。在 C++20 ranges 中，哨兵是表示已到达容器末尾的对象。第14章演示了许多 C++20 ranges 算法。

### vector 成员函数 `erase`

第31行和第36行使用了大多数序列容器和关联容器都提供的两个 `erase` 成员函数——`array` 大小固定，`forward_list` 改用函数 `erase_after`，二者除外。第31行删除其迭代器实参指定位置处的元素——在本例中是第一个元素。第36行删除两个迭代器实参指定的公共范围内的元素——在本例中是所有元素。第38行使用成员函数 `empty`（为所有容器和适配器定义）确认 vector 为空。

```cpp
integers.erase(integers.cbegin()); // erase first element
std::cout << "\n\nintegers after erasing first element: ";
std::ranges::copy(integers, output);

// erase remaining elements
integers.erase(integers.cbegin(), integers.cend());
std::cout << std::format("\nErased all elements: integers {} empty\n",
    integers.empty() ? "is" : "is not");
```

```text
integers after erasing first element: 22 2 10 4 5
Erased all elements: integers is empty
```

通常，`erase` 会销毁它删除的对象。然而，删除作为指向动态分配对象的指针的元素并不会删除它指向的对象，可能导致内存泄漏。这也是你不应使用原始指针管理动态分配内存的原因。`unique_ptr`（第11.5节）元素会释放动态分配的内存。如果元素是 `shared_ptr`（第20章），则引用
