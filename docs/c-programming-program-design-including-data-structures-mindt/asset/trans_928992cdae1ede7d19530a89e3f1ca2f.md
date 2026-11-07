
## 序列容器共有的成员函数

上一节介绍了所有容器共有的成员函数。除了这些成员函数外，表 21-6 描述了所有序列容器（即 **vector**、**deque** 和 **list** 类型的容器）共有的成员函数。（假设 **seqCont** 是序列容器。）

**表 21-6** 所有序列容器共有的成员函数

| 表达式 | 描述 |
|---|---|
| `seqCont.insert(position, elem);` | 将 `elem` 的一个副本插入到迭代器 `position` 指定的位置。返回新元素的位置。 |
| `seqCont.insert(position, n, elem);` | 将 `elem` 的 `n` 个副本插入到迭代器 `position` 指定的位置。 |
| `seqCont.insert(position, beg, end);` | 将从 `beg` 开始直到 `end-1` 的元素副本插入到 `seqCont` 中迭代器 `position` 指定的位置。此外，`beg` 和 `end` 都是迭代器。 |
| `seqCont.push_back(elem);` | 将 `elem` 的一个副本插入到 `seqCont` 的末尾。 |
| `seqCont.pop_back();` | 删除最后一个元素。 |
| `seqCont.erase(position);` | 删除迭代器 `position` 指定位置上的元素。 |
| `seqCont.erase(beg, end);` | 删除从 `beg` 开始直到 `end-1` 的所有元素。`beg` 和 `end` 都是迭代器。 |
| `seqCont.clear();` | 从容器中删除所有元素。 |
| `seqCont.resize(num);` | 将元素个数改为 `num`。如果 `size` 增大，则新元素由其默认构造函数创建。 |
| `seqCont.resize(num, elem);` | 将元素个数改为 `num`。如果 `size` 增大，则新元素是 `elem` 的副本。 |

### copy 算法

例 21-4 使用 `for` 循环输出 vector 容器的元素。STL 借助函数 `copy` 提供了一种便捷方式来输出容器元素。函数 `copy` 是泛型算法的一部分，可用于任何容器类型。由于我们经常需要输出容器元素，在继续讨论容器之前，先介绍这个函数。

函数 `copy` 的作用不止是输出容器元素。一般来说，它允许我们把元素从一个位置复制到另一个位置。例如，要输出 vector 的元素，或把 vector 的元素复制到另一个 vector，可以使用函数 `copy`。函数模板 `copy` 的原型如下：

```cpp
template <class InputIterator, class OutputIterator>
OutputIterator copy(InputIterator first1, InputIterator last,
                    OutputIterator first2);
```

参数 `first1` 指定开始复制元素的位置；参数 `last` 指定结束位置。参数 `first2` 指定将元素复制到哪里。因此，参数 `first1` 和 `last` 指定源；参数 `first2` 指定目标。

注意，范围 `first1...last-1` 内的元素会被复制。

函数模板 `copy` 的定义包含在头文件 `algorithm` 中。因此，要使用函数 `copy`，程序必须包含语句

```cpp
#include <algorithm>
```

函数 `copy` 的工作方式如下。考虑以下语句：

```cpp
int intArray[] = {5, 6, 8, 3, 40, 36, 98, 29, 75};
```

该语句创建一个包含九个分量的数组 `intArray`。这里，`intArray[0] = 5`、`intArray[1] = 6`，依此类推。

语句

```cpp
vector<int> vecList(9);
```

创建一个包含九个 `int` 类型分量的 `vector` 容器。

回顾一下，数组名 `intArray` 实际上是一个指针，包含数组的基地址。因此，`intArray` 指向数组的第一个分量，`intArray + 1` 指向数组的第二个分量，依此类推。

现在考虑以下语句：

```cpp
copy(intArray, intArray + 9, vecList.begin());
```

该语句将从位置 `intArray`（即数组 `intArray` 的第一个分量）开始，直到 `intArray + 9 - 1`（即 `intArray + 8`，也就是数组 `intArray` 的最后一个元素）的元素复制到容器 `vecList` 中。（注意，这里 `first1` 是 `intArray`，`last` 是 `intArray + 9`，`first2` 是 `vecList.begin()`。）执行前面的语句后：

```cpp
vecList = {5, 6, 8, 3, 40, 36, 98, 29, 75}
```

接下来，考虑以下语句：

```cpp
copy(intArray + 1, intArray + 9, intArray);
```

这里，`first1` 是 `intArray + 1`；也就是说，`first1` 指向数组 `intArray` 第二个元素的位置，而 `last` 是 `intArray + 9`。此外，`first2` 是 `intArray`；也就是说，`first2` 指向数组 `intArray` 第一个元素的位置。因此，第二个数组元素被复制到第一个数组分量中，第三个数组元素被复制到第二个数组分量中，依此类推。执行前面的语句后：

```cpp
intArray = {6, 8, 3, 40, 36, 98, 29, 75, 75}
```

显然，数组 `intArray` 的元素向左移动了一个位置。现在考虑以下语句：

```cpp
copy(vecList.rbegin() + 2, vecList.rend(), vecList.rbegin());
```

回顾一下，函数 `rbegin`（反向开始）返回指向容器中最后一个元素的指针；它用于按逆序处理容器元素。因此，`vecList.rbegin() + 2` 返回指向容器 `vecList` 中倒数第三个元素的指针。类似地，函数 `rend`（反向结束）返回指向容器中第一个元素的指针。前面的语句将容器 `vecList` 的元素向右移动两个位置。执行前面的语句后，容器 `vecList` 为

```cpp
vecList = {5, 6, 5, 6, 8, 3, 40, 36, 98}
```

例 21-5 用一个 C++ 程序展示了上述语句的效果。在讨论例 21-5 之前，让我们描述一种特殊类型的迭代器，称为 ostream 迭代器。这些迭代器与函数 `copy` 配合良好，可将容器元素复制到输出设备。

### *ostream* 迭代器与 *copy* 函数

输出容器内容的一种方法是使用 `for` 循环，用函数 `begin` 初始化 `for` 循环控制变量，并用函数 `end` 设置限制。另一种方法是使用函数 `copy` 输出容器元素。在这种情况下，类型为 ostream 的迭代器指定目标。（本章后面会详细讨论 ostream 迭代器。）创建 ostream 类型的迭代器时，我们还要指定该迭代器将输出的元素类型。

以下语句说明如何创建元素类型为 int 的 ostream 迭代器：

```cpp
ostream_iterator<int> screen(cout, " ");        //Line A
```

该语句创建 `screen`，它是一个元素类型为 `int` 的 `ostream` 迭代器。迭代器 `screen` 有两个参数：对象 `cout` 和一个空格。因此，迭代器 `screen` 使用对象 `cout` 初始化。当该迭代器输出元素时，元素之间用空格分隔。

语句

```cpp
copy(intArray, intArray + 9, screen);
```

将 `intArray` 的元素输出到屏幕上。类似地，语句

```cpp
copy(vecList.begin(), vecList.end(), screen);
```

将容器 `vecList` 的元素输出到屏幕上。

我们将经常使用函数 `copy`，通过 ostream 迭代器输出容器元素。此外，在详细讨论 ostream 迭代器之前，我们将使用类似 A 行的语句来创建 ostream 迭代器。

当然，我们可以在函数 `copy` 中直接指定 ostream 迭代器。例如，语句（前面已展示）

```cpp
copy(vecList.begin(), vecList.end(), screen);
```

等价于语句

```cpp
copy(vecList.begin(), vecList.end(),
              ostream_iterator<int>(cout, " "));
```

最后，语句

```cpp
copy(vecList.begin(), vecList.end(),
              ostream_iterator<int>(cout, ", "));
```

输出 `vecList` 的元素，元素之间用逗号和空格分隔。

例 21-5 展示了如何在程序中使用函数 `copy` 和 ostream 迭代器。

### 例 21-5

```cpp
#include <algorithm>                        //Line 1
#include <vector>                           //Line 2
#include <iterator>                         //Line 3
#include <iostream>                         //Line 4

using namespace std;                        //Line 5

int main()                                  //Line 6
{                                           //Line 7
    int intArray[] = {5, 6, 8, 3, 40,
                      36, 98, 29, 75};      //Line 8

    vector<int> vecList(9);                 //Line 9
```
