
| 30 | 111.11 |
|---:|------:|
| 40 | 8765.43 |

**图 22.22** 标准库 map 类模板。（第 3 部分，共 3 部分。）

## 22.7 容器适配器

STL 提供了三种容器适配器——stack、queue 和 priority_queue。适配器不是第一类容器，因为它们不提供可存储元素的实际数据结构实现，而且适配器不支持迭代器。适配器类的优势在于，你可以选择合适的底层数据结构。所有三种适配器类都提供成员函数 **push** 和 **pop**，它们分别将元素正确插入每个适配器数据结构，并从每个适配器数据结构中正确移除元素。接下来的几个小节将给出这些适配器类的示例。

### 22.7.1 stack 适配器

**stack** 类允许在底层数据结构的一端进行插入和删除（通常称为*后进先出*数据结构）。栈可以使用任何序列容器实现：vector、list 和 deque。这个示例创建三个整数栈，分别使用标准库中的每种序列容器作为底层数据结构来表示栈。默认情况下，栈使用 deque 实现。栈操作包括：push 用于在栈顶插入元素（通过调用底层容器的 push_back 函数实现），pop 用于移除栈顶元素（通过调用底层容器的 pop_back 函数实现），top 用于获取栈顶元素的引用（通过调用底层容器的 back 函数实现），empty 用于判断栈是否为空（通过调用底层容器的 empty 函数实现），size 用于获取栈中元素的数量（通过调用底层容器的 size 函数实现）。

> **性能提示 22.3**
>
> 栈的每个常见操作都实现为内联函数，该函数调用底层容器中相应的函数。这避免了第二次函数调用的开销。

> **性能提示 22.4**
>
> 为获得最佳性能，请使用 vector 类作为栈的底层容器。

图 22.23 演示了 stack 适配器类。必须包含头文件 `<stack>` 才能使用 stack 类。第 18、21 和 24 行分别实例化三个整数栈。第 18 行指定一个整数栈，它使用默认的 deque 容器作为其底层数据结构。第 21 行指定一个整数栈，它使用整数 vector 作为其底层数据结构。第 24 行指定一个整数栈，它使用整数 list 作为其底层数据结构。

```cpp
} // end main

// push elements onto stack object to which stackRef refers
template< typename T > void pushElements( T &stackRef )
{
   for ( int i = 0; i < 10; ++i )
   {
      stackRef.push( i ); // push element onto stack
      cout << stackRef.top() << " "; // view (and display) top element
   } // end for
} // end function pushElements

// pop elements from stack object to which stackRef refers
template< typename T > void popElements( T &stackRef )
{
   while ( !stackRef.empty() )
   {
      cout << stackRef.top() << " "; // view (and display) top element
      stackRef.pop(); // remove top element
   } // end while
} // end function popElements
```

```text
Pushing onto intDequeStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto intVectorStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto intListStack: 0 1 2 3 4 5 6 7 8 9

Popping from intDequeStack: 9 8 7 6 5 4 3 2 1 0
Popping from intVectorStack: 9 8 7 6 5 4 3 2 1 0
Popping from intListStack: 9 8 7 6 5 4 3 2 1 0
```

**图 22.23** | 标准库 stack 适配器类。（第 2 部分，共 2 部分。）

### 22.7.2 queue 适配器

**queue** 类允许在底层数据结构的后端插入、从前端删除（通常称为*先进先出*数据结构）。队列可以使用 STL 数据结构 list 或 deque 实现。默认情况下，队列使用 deque 实现。队列的常见操作包括：**push** 用于在队列后端插入元素（通过调用底层容器的 **push_back** 函数实现），**pop** 用于移除队列前端的元素（通过调用底层容器的 **pop_front** 函数实现），**front** 用于获取队列中第一个元素的引用（通过调用底层容器的 **front** 函数实现），**back** 用于获取队列中最后一个元素的引用（通过调用底层容器的 **back** 函数实现），**empty** 用于判断队列是否为空（通过调用底层容器的 **empty** 函数实现），**size** 用于获取队列中元素的数量（通过调用底层容器的 **size** 函数实现）。

![](img/bfd978e7e9b192bab46ec2a89e481263_920_0.png)

> **性能提示 22.15**
>
> *为获得最佳性能，请使用 deque 类作为队列的底层容器。*

![](img/bfd978e7e9b192bab46ec2a89e481263_921_0.png)

> **性能提示 22.16**
>
> 队列的每个常见操作都实现为内联函数，该函数调用底层容器中相应的函数。这避免了第二次函数调用的开销。

图 22.24 演示了 queue 适配器类。必须包含头文件 `queue` 才能使用队列。第 9 行实例化一个存储 double 值的队列。第 12–14 行使用 push 函数向队列添加元素。第 19–23 行的 while 语句使用 empty 函数（所有容器都提供）判断队列是否为空（第 19 行）。当队列中还有更多元素时，第 21 行使用 queue 的 front 函数读取（但不移除）队列中的第一个元素用于输出。第 22 行使用 pop 函数（所有适配器类都提供）移除队列中的第一个元素。

```cpp
// Fig. 22.24: Fig22_24.cpp
// Standard Library adapter queue test program.
#include <iostream>
#include <queue> // queue adapter definition
using namespace std;

int main()
{
    queue<double> values; // queue with doubles

    // push elements onto queue values
    values.push(3.2);
    values.push(9.8);
    values.push(5.4);

    cout << "Popping from values: ";

    // pop elements from queue
    while (!values.empty())
    {
        cout << values.front() << ' '; // view front element
        values.pop(); // remove element
    } // end while

    cout << endl;
} // end main
```

```text
Popping from values: 3.2 9.8 5.4
```

**图 22.24** | 标准库 queue 适配器类模板。

### 22.7.3 priority_queue 适配器

priority_queue 类提供的功能允许按排序顺序插入底层数据结构，并从底层数据结构前端删除。priority_queue 可以使用 STL 序列容器 vector 或 deque 实现。默认情况下，priority_queue 使用 vector 作为底层容器。当元素添加到 priority_queue 时，它们按优先级顺序插入，因此最高优先级的元素（即最大值）将是从 `priority_queue` 中移除的第一个元素。这通常通过将元素排列成一种称为**堆**的二叉树结构来实现，该结构始终将最大值（即最高优先级元素）保持在数据结构的前端。我们将在 22.8.12 节讨论 STL 的堆算法。默认情况下，元素比较使用比较器函数对象 `less<>` 执行，但你可以提供不同的比较器。

`priority_queue` 有几种常见操作。`push` 根据优先队列的优先级顺序将元素插入适当位置（通过调用底层容器的 `push_back` 函数实现，然后使用堆排序重新排列元素）。`pop` 移除 `priority_queue` 中最高优先级的元素（在移除堆顶元素后，通过调用底层容器的 `pop_back` 函数实现）。`top` 获取 `priority_queue` 顶部元素的引用（通过调用底层容器的 `front` 函数实现）。`empty` 判断 `priority_queue` 是否为空（通过调用底层容器的 `empty` 函数实现）。`size` 获取 `priority_queue` 中元素的数量（通过调用底层容器的 `size` 函数实现）。

> **性能提示 22.17**
>
> *`priority_queue` 的每个常见操作都实现为内联函数，该函数调用底层容器中相应的函数。这避免了第二次函数调用的开销。*

> **性能提示 22.18**
>
> *为获得最佳性能，请使用 `vector` 类作为 priority_queue 的底层容器。*

图 22.25 演示了 `priority_queue` 适配器类。必须包含头文件 `<queue>` 才能使用 `priority_queue` 类。第 9 行实例化一个存储 `double` 值的 `priority_queue`，并使用 `vector` 作为底层数据结构。第 12–14 行使用 `push` 函数向 `priority_queue` 添加元素。第 19–23 行的 `while` 语句使用 `empty` 函数（所有容器都提供）判断 `priority_queue` 是否为空（第 19 行）。当还有更多元素时，第 21 行使用 `priority_queue` 的 `top` 函数获取 `priority_queue` 中最高优先级的元素用于输出。第 22 行使用 `pop` 函数（所有适配器类都提供）移除 `priority_queue` 中最高优先级的元素。

```cpp
// Fig. 22.25: Fig22_25.cpp
// Standard Library adapter priority_queue test program.
#include <iostream>
#include <queue> // priority_queue adapter definition
using namespace std;

int main()
{
    priority_queue<double> priorities; // create priority_queue
}
```

**图 22.25** | 标准库 `priority_queue` 适配器类。（第 1 部分，共 2 部分。）

