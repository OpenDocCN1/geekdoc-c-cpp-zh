
第 45 行到第 50 行的语句将 Donny、Zippy、Goofy、Hungry、Goofy 和 Donny 插入 `namesMultiSet`。第 52 行的语句输出 `namesMultiSet` 的元素。

## 容器适配器

前面几节讨论了几种类型的容器。除了在通用框架中工作的容器之外，STL 还提供了一些用于适应特殊情况的容器。这些容器称为**容器适配器**，它们是经过适配的标准 STL 容器，以便在特定环境中工作。三种容器适配器是：

- 栈
- 队列
- 优先级队列

容器适配器不支持任何类型的迭代器。也就是说，迭代器不能用于这些类型的容器。接下来的两节介绍两种容器适配器：栈和队列。

### 栈

第 17 章详细讨论了数据结构栈。由于栈是一种重要的数据结构，STL 提供了一个类来在程序中实现栈。定义栈的类名是 `stack`；包含 `class` `stack` 定义的头文件名是 `stack`。表 21-19 定义了栈容器类支持的各种操作。

**表 21-19 —— 对栈对象的各种操作**

| 操作 | 描述 |
|---|---|
| `size` | 返回栈中元素的实际数量。 |
| `empty` | 如果栈为空，则返回 `true`，否则返回 `false`。 |
| `push(item)` | 将 `item` 的副本压入栈中。 |
| `top` | 返回栈顶元素，但不从栈中移除该元素。该操作实现为值返回函数。 |
| `pop` | 移除栈顶元素。 |

除了 `size`、`empty`、`push`、`top` 和 `pop` 这些操作之外，栈容器类还提供关系运算符来比较两个栈。例如，关系运算符 == 可用于判断两个栈是否相同。

示例 21-9 中的程序说明了如何使用栈容器类。

### 示例 21-9

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main()
{
    stack<int> intStack;                         //Line 1

    intStack.push(16);                           //Line 2
    intStack.push(8);                            //Line 3
    intStack.push(20);                           //Line 4
    intStack.push(3);                            //Line 5

    cout << "Line 6: The top element of intStack: "
         << intStack.top() << endl;              //Line 6

    intStack.pop();                              //Line 7

    cout << "Line 8: After the pop operation, "
         << "the top element of intStack: "
         << intStack.top() << endl;              //Line 8

    cout << "Line 9: intStack elements: ";      //Line 9

    while (!intStack.empty())                    //Line 10
    {
        cout << intStack.top() << " ";           //Line 11
        intStack.pop();                          //Line 12
    }

    cout << endl;                                 //Line 13

    return 0;
}
```

**示例运行：**

```text
Line 6: The top element of intStack: 3
Line 8: After the pop operation, the top element of intStack: 20
Line 9: intStack elements: 20 8 16
```

前面的输出不言自明。细节留作练习。

### 队列

第 17 章详细讨论了数据结构队列。由于队列是一种重要的数据结构，STL 提供了一个类来在程序中实现队列。定义队列的类名是 queue，包含类 queue 定义的头文件名是 queue。表 21-20 定义了队列容器类支持的各种操作。

**表 21-20** 对队列对象的各种操作

| 操作 | 描述 |
|---|---|
| `size` | 返回队列中元素的实际数量。 |
| `empty` | 如果队列为空，则返回 `true`，否则返回 `false`。 |
| `push(item)` | 将 `item` 的副本插入队列。 |
| `front` | 返回下一个项，即队列中的第一个元素，但不从队列中移除该元素。该操作实现为值返回函数。 |
| `back` | 返回队列中的最后一个元素，但不从队列中移除该元素。该操作实现为值返回函数。 |
| `pop` | 移除队列中的下一个元素。 |

除了 `size`、`empty`、`push`、`front`、`back` 和 `pop` 这些操作之外，队列容器类还提供关系运算符来比较两个队列。例如，关系运算符 == 可用于判断两个队列是否相同。

示例 21-10 中的程序说明了如何使用队列容器类。

### 示例 21-10

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main()
{
    queue<int> intQueue;                    //Line 1

    intQueue.push(26);                      //Line 2
    intQueue.push(18);                      //Line 3
    intQueue.push(50);                      //Line 4
    intQueue.push(33);                      //Line 5

    cout << "Line 6: The front element of intQueue: "
         << intQueue.front() << endl;       //Line 6

    cout << "Line 7: The last element of intQueue: "
         << intQueue.back() << endl;        //Line 7

    intQueue.pop();                         //Line 8

    cout << "Line 9: After the pop operation, "
         << "the front element of intQueue: "
         << intQueue.front() << endl;       //Line 9

    cout << "Line 10: intQueue elements: "; //Line 10
    while (!intQueue.empty())               //Line 11
    {
        cout << intQueue.front() << " ";    //Line 12
        intQueue.pop();                     //Line 13
    }

    cout << endl;                           //Line 14

    return 0;
}
```

**示例运行：**

```text
Line 6: The front element of intQueue: 26
Line 7: The last element of intQueue: 33
Line 9: After the pop operation, the front element of intQueue: 18
Line 10: intQueue elements: 18 50 33
```

前面的输出不言自明。细节留作练习。

## 容器、关联头文件与迭代器支持

前面几节讨论了各种类型的容器。回想一下，每个容器都是一个类。实现特定容器的类的定义包含在头文件中。表 21-21 描述了容器、其关联头文件以及该容器支持的迭代器类型。

**表 21-21** 容器、其关联头文件以及每个容器支持的迭代器类型

| 顺序容器 | 关联头文件 | 迭代器支持类型 |
|---|---|---|
| `vector` | `<vector>` | 随机访问 |
| `deque` | `<deque>` | 随机访问 |
| `list` | `<list>` | 双向 |
| **关联容器** | **关联头文件** | **迭代器支持类型** |
| `map` | `<map>` | 双向 |
| `multimap` | `<map>` | 双向 |
| `set` | `<set>` | 双向 |
| `multiset` | `<set>` | 双向 |
| **适配器** | **关联头文件** | **迭代器支持类型** |
| `stack` | `<stack>` | 无迭代器支持 |
| `queue` | `<queue>` | 无迭代器支持 |
| `priority_queue` | `<queue>` | 无迭代器支持 |

## 算法

可以为容器定义多种操作。其中一些操作非常特定于某个容器，因此作为容器定义的一部分提供（即作为实现该容器的类的成员函数）。然而，查找、排序和合并等若干操作是所有容器共有的。这些操作以泛型算法形式提供，可应用于所有容器以及内置数组类型。算法通过一对迭代器绑定到特定容器。

泛型算法包含在头文件 `algorithm` 中。本节介绍其中几种算法，并展示如何在程序中使用它们。由于算法是借助函数实现的，因此在本节中，术语*函数*和*算法*含义相同。

