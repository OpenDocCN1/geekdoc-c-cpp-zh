
表明 `generate` 期望参数为代表处理元素范围的 `ForwardIterators` 以及一个 `Generator` 函数。标准解释说，算法调用 `Generator` 函数来为 `ForwardIterators` 指定范围内的每个元素获取一个值。标准还规定 `Generator` 不接受任何参数，并返回一个可以赋值给元素的值。

对于每个可以接收函数指针、对象或 lambda 表达式的算法，都提供了类似的文档。在本章的大多数示例中，当我们展示每个示例时，都指定了此类参数的要求。

## 16.4.2 equal, mismatch 和 lexicographical_compare

16.3 展示了使用算法 `equal`、`mismatch` 和 `lexicographical_compare` 对值进行等的比较。第 11–13 行创建并初始化了三个数组。当调用数组的构造函数（第 12 行）时，你不能使用大括号，因为

```cpp
array<int, SIZE> a[2];
```

前面的声明会导致编译错误，因为编译器将大括号中的内容视为数组元素的值列表。在这种情况下，编译器将用数组对象初始化 a2 的第一个元素——从数组对象到单个 int 值没有隐式转换。

```cpp
// Fig.16.3: fig16_03.cpp
// Algorithms equal, mismatch and lexicographical_compare.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <array> // array-template definition
#include <iterator> // ostream_iterator
```

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_755_0.png)

## 第16 章 标准库算法

```cpp
using namespace std;
int main() {
  const size_t SIZE{10};
  array<int, SIZE> a1={1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  array<int, SIZE> a2(a1);
  array<int, SIZE> a3={1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  ostream_iterator<int> output(cout, " ");
  cout << "a1 contains:";
  copy(a1.begin(), a1.end(), output);
  cout << "\na2 contains:";
  copy(a2.begin(), a2.end(), output);
  cout << "\na3 contains:";
  copy(a3.begin(), a3.end(), output);
  // compare a1 and a2 for equality
  bool result=equal(a1.begin(), a1.end(), a2.begin(), a2.end());
  cout << "\n" << (result ? " is: " : " is not") " equal to a2";
  // compare a1 and a3 for equality
  result = equal(a1.begin(), a1.end(), a3.begin(), a3.end());
  cout << "\n" << (result ? " is: " : " is not") " equal to a3";
  // check for mismatch between a1 and a3
  auto location = mismatch(a1.begin(), a1.end(), a3.begin(), a3.end());
  cout << "\nwhere is a mismatch between a1 and a3 at location ";
  cout << location.first << " - " << a1.begin() << " and a3 contains " << location.second;
  cout << "\n";
  char c1[SIZE] = "HELLO";
  char c2[SIZE] = "BYE";
  // perform lexicographical comparison of c1 and c2
  result = lexicographical_compare(cbegin(c1), cend(c1), cbegin(c2), cend(c2));
  cout << "\n" << (result ? " is less than " : " is greater than or equal to") << c2 << endl;
}
```

a1 contains: 1 2 3 4 5 6 7 8 9 10
a2 contains: 1 2 3 4 5 6 7 8 9 10
a3 contains: 1 2 3 4 10 6 7 8 9 10

a1 is equal to a2
a is not equal to a3
There is a mismatch between a1 and a3 at location 4
where a1 contains 5 and a3 contains 10
HELLO is greater than or equal to BYE

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_756_0.png)

### equal 算法

第 24 行使用 C++14 版本的 `equal` 算法比较两个值序列。第二个序列必须包含相同数量的元素——如果序列长度不同，`equal` 返回 false。`==` 运算符（无论是内置还是重载的）执行比较。在本示例中，从 `a1.begin()` 到但不包括 `a3.end()` 的元素与从 `a2.begin()` 开始到但不包括 `a2.end()` 的元素进行比较。在本示例中，a1 和 a2 是相等的。这四个迭代器至少是输入迭代器（即它们可以用于序列的输入（*前向方向*））。第 28 行使用函数 `equal` 比较 a1 和 a3，它们是不相等的。

### 带有二元谓词函数的 equal 算法

`equal` 算法的每个版本都有一个重载版本，接受二元谓词函数作为最后一个参数。二元谓词接收待比较的两个元素并返回一个指示元素是否等的 bool 值。这对于存储对象或值指针而非实际值的序列非常有用，因为你可以定义一个或多个比较。例如，你可以根据年龄、社会安全号或位置比较 Employee 对象，而不是比较实体对象。你可以比较指针而不是指针值。

### mismatch 算法

第 32-33 行调用 C++14 版本的 `mismatch` 算法比较两个值序列。该算法返回一个迭代器对，指示每个序列中第一个不匹配元素的位置。如果所有元素都匹配，对中的两个迭代器等于每个序列的结束迭代器。我们使用 C++14 的 `auto` 关键字推断对对象 `location` 的类型（第 32 行）。第 35 行通过表达式 `location.first - a1.begin()` 确定数组中不匹配的实际位置，该表达式等于返回对中迭代器之间的元素数量（类似于指针算术；第 8 章）。这对应于示例中的元素编号，因为比较是从数组的开始执行。与 `equal` 一，`mismatch` 将二元谓词函数作为最后一个参数。

> 错误预防提示 16.1
> 始终使用 C++14 版本的 `equal` 和 `mismatch`。在 C++14 之前，这些算法只接收三个迭代器——第三个指示待比较序列的第二个起始点。程序员需要在调用这些算法之前测试序列长度是否相同。首选 C++14 版本，因为它们会为你比较范围长度，消除了潜在的错误源。

### auto 变量和列表初始化

第 32-33 行使用等号（=）而不是初始化变量 `location`。这是由于使用大括号初始化的变量存在一个限制。这是一个在 C++17 中修复此问题的提案。

+ 1. http://cpp-std.org/JTC1/SC22/WG21/docs/papers/2013/n3681.html.

# 第 16 章 标准库算法

> 错误预防技巧 16.2
> 在 C++14 中，初始化用 `auto` 声明的变量时，请使用 `=` 而不是 `=`。

### lexicographical_compare 算法

第 43-44 行使用 `lexicographical_compare` 算法来比较两个由字符构建的迭代器的内容。该算法的四个迭代器参数至少必须是输入迭代器（input iterators）。如你所知，内置数组的指针是随机访问迭代器。前两个迭代器指定了第一个序列中的位置范围。对于第二个序列，我们使用 C++11 的 `begin` 和 `end` 函数来确定每个内置数组的元素范围。在遍历序列时，如果序列中的对应元素不匹配，且第一个序列中的元素小于第二个序列中的对应元素，则该算法返回 `true`；否则，算法返回 `false`。该算法可以按字典序排列序列。通常，此类序列包含字符串。

## 16.4.3 remove, remove_if, remove_copy 和 remove_copy_if

图 16.4 展示了如何使用 `remove`、`remove_if`、`remove_copy` 和 `remove_copy_if` 算法从序列中移除值。

```cpp
// Fig 16.4: fig16_04.cpp
// remove, remove_if, remove_copy and remove_copy_if.
#include <iostream>
#include <algorithm> // algorithm 定义
#include <array> // array 类模板
#include <iterator> // stream_iterator
using namespace std;
int main() {
    const size_t SIZE{10};
    array<int, SIZE> init{10, 2, 10, 4, 16, 6, 14, 8, 12, 10};
    stream_iterator<int> output(cout, "");
    array<int, SIZE> al(init); // 用 init 的拷贝初始化
    cout << "\before removing all 10s:\n";
    copy(al.begin(), al.end(), output);
    // 从 al 中移除所有的 10
    auto end = remove(al.begin(), al.end(), 10);
    cout << "\nal after removing all 10s:\n";
    copy(al.begin(), end, output);
    array<int, SIZE> a2(init); // 用 init 的拷贝初始化
    array<int, SIZE> c0{0}; // 初始化为 0
    cout << "\n\na2 before removing all 10s and copying:\n";
    copy(a2.begin(), a2.end(), output);
    // 将 a2 拷贝到 c2。在此过程中移除 10
    remove_copy(a2.begin(), a2.end(), c.begin(), 10);
    cout << "\na2 after removing all 10s from a2:\n";
    copy(c.begin(), c.end(), output);
    array<int, SIZE> a3(init); // 用 init 的拷贝初始化
    cout << "\na3 before removing all elements greater than 9:\n";
    copy(a3.begin(), a3.end(), output);
    // 从 a3 中移除大于 9 的元素
    newEnd = remove_if(a3.begin(), a3.end(),
      [](auto x) { return x > 9; });
    cout << "\na3 after removing all elements greater than 9:\n";
    copy(a3.begin(), newEnd, output);
    array<int, SIZE> a4(init); // 用 init 的拷贝初始化
    array<int, SIZE> c2(0); // 初始化为 0
    cout << "\na4 before removing all elements\n";
    cout << "\greater than 9 copying:\n";
    copy(a4.begin(), a4.end(), output);
    // 将 a4 拷贝到 c2，在此过程中移除大于
    than元素
    remove_copy(a4.begin(), a4.end(), c2.begin(),
      [](auto x) { return x > 9; });
    cout << "\na2 after removing all elements \n";
    copy(c2.begin(), c2.end(), output);
    cout << endl;
}
```
