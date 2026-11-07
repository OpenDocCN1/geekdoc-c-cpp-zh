
```cpp
vecList = {5, 6, 5, 6, 8, 3, 40, 36, 98};
```

示例 H-5 使用一个 C++ 程序展示了前面语句的效果。在展示示例 H-5 之前，下面先描述一种特殊类型的迭代器，称为 **ostream 迭代器**，它与函数 copy 配合良好，可将容器中的元素复制到输出设备。

## ostream 迭代器与函数 copy

输出容器内容的一种方法是使用 for 循环，并用函数 begin 初始化 for 循环控制变量，用函数 end 设置上限。然而，函数 copy 也可以用于输出容器的元素。在这种情况下，类型为 ostream 的迭代器指定目标。（ostream 迭代器将在本附录后面讨论。）创建 ostream 类型的迭代器时，我们还要指定该迭代器将输出的元素类型。

下面的语句说明如何创建元素类型为 int 的 ostream 迭代器：

```cpp
ostream_iterator<int> screen(cout, " ");    //Line A
```

该语句创建 screen 为一个 ostream 迭代器，元素类型为 int。迭代器 screen 有两个实参：对象 cout 和一个空格。这意味着迭代器 screen 使用对象 cout 进行初始化，并且当该迭代器输出元素时，元素之间用空格分隔。

语句：

```cpp
copy(intArray, intArray + 9, screen);
```

将 intArray 的元素输出到屏幕上。

类似地，语句：

```cpp
copy(vecList.begin(), vecList.end(), screen);
```

将容器 vecList 的元素输出到屏幕上。

我们将经常使用函数 copy 和 ostream 迭代器来输出容器中的元素。另外，在详细讨论 ostream 迭代器之前，我们将使用与行 A 中语句类似的语句来创建 ostream 迭代器。

当然，我们可以在函数 copy 中直接指定 ostream 迭代器。例如，下面的语句（前面已展示）：

```cpp
copy(vecList.begin(), vecList.end(), screen);
```

等价于下面的语句：

```cpp
copy(vecList.begin(), vecList.end(),
     ostream_iterator<int>(cout, " "));
```

最后，语句：

```cpp
copy(vecList.begin(), vecList.end(),
     ostream_iterator<int>(cout, ", "));
```

输出 vecList 的元素，元素之间用逗号和空格分隔。

示例 H-5 说明如何在程序中使用函数 copy 和 ostream 迭代器。

### 示例 H-5

```cpp
#include <algorithm>
#include <vector>
#include <iterator>
#include <iostream>

using namespace std;

int main()
{
    int intArray[] = {5, 6, 8, 3, 40,
                      36, 98, 29, 75};                  //Line 1

    vector<int> vecList(9);                              //Line 2

    ostream_iterator<int> screen(cout, " ");            //Line 3

    cout << "Line 4: intArray: ";                       //Line 4
    copy(intArray, intArray + 9, screen);                //Line 5
    cout << endl;                                        //Line 6

    copy(intArray, intArray + 9, vecList.begin());       //Line 7

    cout << "Line 8: vecList: ";                        //Line 8
    copy(vecList.begin(), vecList.end(), screen);        //Line 9
    cout << endl;                                        //Line 10

    copy(intArray + 1, intArray + 9, intArray);          //Line 11
    cout << "Line 12: After shifting the elements "
         << "one position to the left," << endl
         << "        intArray: ";                       //Line 12
    copy(intArray, intArray + 9, screen);                //Line 13
    cout << endl;                                        //Line 14

    copy(vecList.rbegin() + 2, vecList.rend(),
         vecList.rbegin());                              //Line 15
    cout << "Line 16: After shifting the elements "
         << " down by two positions," << endl
         << "        vecList: ";                         //Line 16
    copy(vecList.begin(), vecList.end(), screen);        //Line 17
    cout << endl;                                        //Line 18

    return 0;
}
```

### 示例运行

```text
Line 4: intArray: 5 6 8 3 40 36 98 29 75
Line 8: vecList: 5 6 8 3 40 36 98 29 75
Line 12: After shifting the elements one position to the left,
         intArray: 6 8 3 40 36 98 29 75 75
Line 16: After shifting the elements down by two positions,
         vecList: 5 6 5 6 8 3 40 36 98
```

## 序列容器：`deque`

本节介绍序列容器 deque。术语 **deque** 表示双端队列。deque 容器实现为动态数组，因此可以在两端插入元素。于是，deque 可以向任一方向扩展。元素也可以插入到中间。在开头或末尾插入元素很快；然而，在中间插入元素很耗时，因为队列中的元素需要移动。

定义 deque 容器的类名为 deque。此外，类 deque 的定义以及用于实现对 deque 对象各种操作的函数都包含在头文件 deque 中。因此，要在程序中使用 deque 容器，程序必须包含以下语句：

```cpp
#include <deque>
```

类 deque 包含多个构造函数。因此，deque 对象在声明时可以用多种方式初始化。表 H-7 描述了声明 deque 对象的多种方式。

**表 H-7** 声明 `deque` 对象的多种方式

| 语句 | 描述 |
|---|---|
| `deque<elementType> deq;` | 创建一个空的 deque 容器 deq。（调用默认构造函数。） |
| `deque<elementType> deq(otherDeq);` | 创建 deque 容器 deq，并将其初始化为 otherDeq 的元素；deq 和 otherDeq 类型相同。 |
| `deque<ElementType> deq(size);` | 创建大小为 size 的 deque 容器 deq。deq 使用默认构造函数初始化。 |
| `deque<ElementType> deq(n, elm);` | 创建大小为 n 的 deque 容器 deq。deq 使用元素 elm 的 n 个副本初始化。 |
| `deque<ElementType> deq(beg, end);` | 创建 deque 容器 deq。deq 初始化为范围 [beg, end) 中的元素，即范围 beg...end-1 中的所有元素。beg 和 end 都是迭代器。 |

除了所有容器共有的操作（见表 H-6）之外，表 H-8 描述了可用于操作 deque 容器元素的操作。实现这些操作的函数名以粗体显示。语句还展示了如何使用某个特定函数。（假设 deq 是一个 deque 容器。）

**表 H-8** 可对 `deque` 对象执行的各种操作

| 表达式 | 描述 |
|---|---|
| `deq.assign(n,elem)` | 将 elem 的 n 个副本赋给容器。 |
| `deq.assign(beg, end)` | 赋予范围 beg...end-1 中的所有元素。 |
| `deq.push_front(elem)` | 将 elem 插入 deq 的开头。 |
| `deq.pop_front()` | 从 deq 中移除第一个元素。 |
| `deq.at(index)` | 返回由 index 指定位置处的元素。 |
| `deq[index]` | 返回由 index 指定位置处的元素。 |
| `deq.front()` | 返回第一个元素。（不检查容器是否为空。） |
| `deq.back()` | 返回最后一个元素。（不检查容器是否为空。） |

```cpp
    copy(intDeq.begin(), intDeq.end(), screen);    //Line 23
    cout << endl;                                  //Line 24

    return 0;
}
```

### 示例运行

```text
Line 7:  intDeq: 13 75 28 35
Line 12: After adding two more elements, one at the front
         and one at the back, intDeq: 0 13 75 28 35 100
Line 17: After removing the first two elements,
         intDeq: 75 28 35 100
Line 22: After removing the last two elements,
         intDeq: 75 28
```

第 1 行中的语句声明一个元素类型为 int 的 deque 容器 intDeq，即 intDeq 的所有元素都是 int 类型。第 2 行中的语句声明 screen 为一个 ostream 迭代器，并将其初始化为标准输出设备。第 3 行到第 6 行中的语句使用 push_back 操作将四个数——13、75、28 和 35——插入 intDeq。第 8 行中的语句输出 intDeq 的元素。在输出中，参见标记为 Line 7 的那一行，它包含第 7 行到第 9 行中语句的输出。

第 10 行中的语句在 intDeq 的开头插入 0；第 11 行中的语句在 intDeq 的末尾插入 100。第 13 行中的语句输出修改后的 intDeq。

第 15 行和第 16 行中的语句使用 pop_front 操作移除 intDeq 的前两个元素，第 18 行中的语句输出修改后的 intDeq。第 20 行和第 21 行中的语句使用 pop_back 操作移除 intDeq 的最后两个元素，第 23 行中的语句输出修改后的 intDeq。

## 序列容器：`list`

本节介绍序列容器 list。list 容器实现为双向链表。因此，list 中的每个元素都指向其直接前驱和直接后继（第一个和最后一个元素除外）。回想一下，链表不是随机访问数据结构，例如数组。因此，要访问 list 中的第五个元素，必须先遍历前四个元素。

包含类 list 定义的类名为 list。此外，类 list 的定义以及用于实现对 list 各种操作的函数定义都包含在头文件 list 中。因此，要在程序中使用 list，程序必须包含以下语句：

```cpp
#include <list>
```
