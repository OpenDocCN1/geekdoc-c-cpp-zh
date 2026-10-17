
同样，你可以使用 `C++11` 列表初始化来初始化从函数返回的对象。例如，以下代码返回一个包含 `int` 和 `double` 的 `pair`：

```cpp
return {15, 2.7};
```

第 22–25 行向 `multimap` 插入了五个关联对对。第 30–32 行的基于范围的 `for` 语句输出了 `multimap` 的内容，包括键和值。我们使用关键字 `auto` 推导出循环控制变量（一个包含 `int` 和 `double` 值的 `pair`）的类型。第 31 行访问 `multimap` 中每个元素中当前 `pair` 的成员。注意，键是按升序排列的。

### C++11：初始化键值对容器

在例例中，我们使用成员函数向 `multimap` 插入键值对。如果你预先知道键值对，可以在创建 `multimap` 时使用列表初始化。以下语句初始化了一个包含三个键值对的 `multimap`，这些对由主初始化器中的列表表示：

```cpp
multimap<int, double, less<int>> pairs{
{10, 22.22}, {20, 9.345}, {5, 77.54}};
```

### 15.6 map 关联容器

关联容器（来自头文件 `<map>`）对唯一的键和值进行快速存储和检索。不允许有重复的键——每个键只能关联一个值。这被称为一对一映射。例如，一家公司使用员工编号（如 100、200 和 300），该可能可能有一个 `map`，将员工与他们的电话分机号（如 4321、4115 和 5217）关联起来。通过 `map`，你可以指定键并快速获取关联的数据。在 `map` 的下标运算符 `[]` 中提供键，可以定位到 `map` 中与该键相关联的值。插入和删除操作可以在 `map` 的任何位置进行。如果键的顺序不重要，你可以使用 `unordered_map`（改用 `<unordered_map>` 头文件）。

图 15.8 展示了下标运算符（在第 8 行创建）并显示了图 15.17 的特征。第 27–28 行使用了 `map` 类的下标运算符。当下标是 `map` 中已存在的键时（第 27 行），该运算符返回关联值的引用。当下标是 `map` 中不存在的键时（第 28 行），该运算符将该键插入 `map`，并返回一个可用于与该键关联值的引用。第 27 行替换了键 25 的值（原先为 33.33），第 28 行在 `map` 中插入了一个新的键值对（创建了一个关联）。此示例中的 `map` 原本可以使用 `pair` 的初始化列表进行初始化，正如我们在第 15.6.3 节中所示。

```cpp
// Fig. 15.18_cpp
// 标准库 map 类模板。
#include <iostream>
#include <map> // map 类-模板定义
using namespace std;
int main() {
    map<int, double, less<int>> pairs;
    // 在 pairs 中 插入每个 value-type 对象
    pairs[25] = 33.33;
    pairs[20] = 9.345;
    pairs[10] = 22.22;
    pairs[15] = 2.7;
    pairs[5] = 77.54;
    cout << "After inserts, there are " << pairs.count(15)
         << "pairs with key 15\n\n";
    cout << "Multimap contains:\nKey\tValue\n";
    // 遍历 pairs 的元素
    for (auto mapItem : pairs) {
        cout << mapItem.first << "\t" << mapItem.second << "\n";
    }
    cout << endl;
}
```

## 15.7 容器适配器

三个适配器是 `stack`、`queue` 和 `priority_queue`。容器适配器不是类容器，因为它们不提供迭代器。适配器类的处是你可以选择合适的数据结构。后续章节提供了示例

### 15.7.1 stack 适配器

`stack` 类（来自头文件 `<stack>`）允许在底层容器的一端（顶部）进行插入和删除，因此栈通常被称为后进先出数据结构。我们在第 6.11 节讨论函数时介绍过栈。栈可以用 `vector`、`list` 或 `deque` 实现。默认情况下，栈用 `deque` 实现。栈的操作包括：`push` 在栈顶插入元素（通过调用底层容器的 `push_back`）、`pop` 栈顶元素（通过调用底层容器的 `pop_back`）、`top` 获取栈顶引用（通过调用底层容器的 `back`）、`empty` 判断栈是否为空以及 `size` 获取栈中元素的数量（通过调用底层容器的 `size`）。在第 19 章中，我们将展示如何开发你自定义的栈类。

图 15.19 展示了栈适配器类。第 17、20 和 23 行使用默认的 `deque` 作为底层数据结构实例化栈。第 20 行指定了使用 `vector<int>` 作为底层数据结构的整数栈；第 23 行指定了使用 `list<int>` 作为底层数据结构的整数栈。

```cpp
// Fig. 1519_stack.cpp
// 标准库 stack 适配器类。
#include <iostream>
#include <stack> // stack 适配器定义
#include <vector> // vector 类-模板定义
#include <list> // list 类-模板定义
using namespace std;
// pushElements-模板原型
template<typename T> void pushElements(T& stackRef);
// popElements 函数-模板原型
template<typename T> void popElements(T& stackRef);
int main() {
    // 使用底层 deque 的栈
    stack<int> intDequeStack;
    // 使用底层 vector 的栈
    stack<int, vector<int>> intVectorStack;
}
```

// 使用底层列表实现的栈
`stack<int, list<int>> intListStack;`

```cpp
// 将元素推入 stackRef 指向的栈对象
template<typename T> void pushElements(T& stackRef) {
    for (int i=0; i < 10; i++) { // 将 i < i 修复为 i < 10
        stackRef.push(i); // 将元素推入栈
        cout << stackRef.top() << ' '; // 查看（并显示）顶元素
    }
}
```

```cpp
// 从 stackRef 指向的栈对象弹出元素
template<typename T> void popElements(T& stackRef) {
    while (!stackRef.empty()) {
        cout << stackRef.top() << ' '; // 查看（并显示）顶元素
        stackRef.pop(); // 移除顶元素
    }
}
```

向 `intDequeStack` 推入: 0 1 2 3 4 5 6 7 8 9
向 `intVectorStack` 推入: 0 1 2 3 4 5 6 7 8 9
向 `intListStack` 推入: 0 1 2 3 4 5 6 7 8 9

从 `intDequeStack` 弹出: 9 8 7 6 5 4 3 2 1 0
从 `intVectorStack` 弹出: 9 8 7 6 5 4 3 2 1 0
从 `intListStack` 弹出: 9 8 7 6 5 4 3 2 1 0

图 15.19 | 标准库栈 适配器类。（2 个部分中的第 2 部分。）

函数 `pushElements`（第 45–50 行）将元素推入每个栈中。第 47 行使用函数（在每个适配器类中可用）将一个整数放在栈顶。第 48 行使用栈函数获取栈的顶元素用于输出。`top` 函数不会移除顶元素。
函数 `popElements`（第 53–58 行）从每个栈中弹出元素。第 55 行使用栈函数获取栈的顶元素。第 56 行使用 `func-`

## 15.7 容器适配器

### 15.7.2 queue 适配器

`pop`（在每个适配器类中可用）以移除栈的顶元素。`pop` 函数不返回值。

队列类似于等待队列。在队列中时间最长的项先被移除——因此队列被称为先进进先出（FIFO）数据结构。
`queue` 类（来自头文件 `<queue>`）仅允许在底层数据的末尾插入，仅允许从前端删除。队列可以按照标准库的 `list` 或 `deque` 顺序存储其元素。默认情况下，队列实现为 `deque`。常见的队列操作包括：在队列末尾插入元素（通过调用底层容器的 `push_back` 实现）、通过 `pop` 移除队列前端元素（通过调用底层容器的 `pop_front` 函数实现）、`front` 获取队列中的第一个元素、`back` 获取队列中最后一个元素的引用（通过调用底层容器的 `back` 实现）、`empty` 判断队列是否为空（这会调用底层容器的 `empty`）以及 `size` 获取队列中的元素数量（这会调用底层容器的 `size`）。在第 19 章，我们将向你展示如何开发自定义队列类模板。

图 15.20 展示了队列适配器类。第 18 行初始化了一个 `double` 类型的队列。第 11–13 行使用 `push` 函数向队列添加元素。第 18–21 行的 `while` 语句使用 `empty` 函数（在所有容器中可用）确定队列是否为空（第 18 行）。如果队列中还有更多元素，第 19 行使用队列函数 `front` 获取（但不移除）队列中的第一个元素用于输出。第 20 行使用 `pop` 函数（在所有适配器类中均可用）移除队列中的第一个元素。

```cpp
// Fig. 15.20: fig15_queue.cpp
#include <iostream>
#include <queue> // queue 适配器定义
using namespace std;
int main() {
    queue<double> values; // 带有 double 的队列
    // 将元素推入队列 values
    values.push(3.2);
    values.push(9.8);
    values.push(5.4);
    cout << "Popping from values: ";
    // 从队列弹出元素
    while (!values.empty()) {
        cout << values.front() << ' '; // 查看前端元素
        values.pop(); // 移除元素
    }
    cout << endl;
}
```

**图 15.20** | 标准库队列适配器类模板。（2 个部分中的第 I 部分）

从 `values` 弹出: 3.2 9.8 5.4

图 15.20 | 标准库队列适配器类模板。（2 个部分中的第 2 部分）

## 15.7 priority_queue 适配器

`priority_queue` 类提供了能够按排序顺序向数据结构中插入元素并从底层数据前端进行删除的功能。默认情况下，`priority_queue` 的元素存储在 `vector` 中。当元素被添加到 `priority_queue` 时，它们按照优先级顺序插入，使得元素按优先级顺序重新排列，优先级最高的元素（即最大值）成为第一个从 `priority_queue` 中移除的元素。这通常通过将元素安排在一个名为堆（heap，不要与动态分配内存的堆混淆）的数据结构中来实现，堆将最大值（即最高优先级元素）维护在数据结构的最前端。元素的比较默认使用比较器函数 `less<>` 执行，但你可以选择不同的比较器。

有几种常见的 `priority_queue` 操作。`push` 根据 `priority_queue` 的优先级顺序在适当位置插入元素，从而按优先级顺序重新排列元素。`pop` 移除 `priority_queue` 中优先级最高的元素（通过调用底层容器的函数实现）。`top` 获取 `priority_queue` 顶元素的引用，`empty` 在 `priority_queue` 为空时返回真。`size` 获取 `priority_queue` 中的元素数量（通过调用底层容器的 `size` 实现）。

图 15.21 展示了 `priority_queue` 适配器类。第 8 行实例化了一个存储 `double` 值的 `priority_queue` 并使用 `vector` 作为底层数据结构。第 11–13 行使用 `push` 函数向队列添加元素。第 18–21 行的 `while` 语句使用 `empty` 函数（在所有容器中可用）确定队列是否为空（第 18 行）。如果队列中还有更多元素，第 19 行使用队列函数 `front` 获取（但不移除）队列中的第一个元素用于输出。第 20 行使用 `pop` 函数（在所有适配器类中均可用）移除队列中的第一个元素。

表达式

```
b <<= n;
```

将位 `set` `b` 中的位左移 `n` 位。

表达式

```
b.to_string()
```

```
b.to_ulong()
```
