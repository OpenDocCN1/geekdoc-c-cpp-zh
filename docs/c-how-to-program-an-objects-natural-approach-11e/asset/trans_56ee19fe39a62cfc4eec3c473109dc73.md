
- **push** 正确地将一个元素插入适配器的底层容器中。
- **pop** 正确地从适配器的底层容器中移除一个元素。

我们来看适配器类的示例。

### 13.12.1 Stack 适配器

类 stack（来自头文件 `<stack>`）允许在底层容器的一端（顶部）插入和删除元素。因此，stack 通常被称为后进先出（last-in, first-out）数据结构。stack 可以用 vector、list 或 deque 实现。默认情况下，stack 用 deque 实现。²⁰ stack 的操作包括

- **push** 在 stack 的**顶部**插入一个元素——通过调用底层容器的 **push_back** 成员函数实现，
- **emplace** 在 stack 的**顶部**就地构造一个元素，
- **pop** 移除 stack 的**顶部**元素——通过调用底层容器的 **pop_back** 成员函数实现，
- **top** 获取对 stack 的**顶部**元素的引用——通过调用底层容器的 **back** 成员函数实现，
- **empty** 判断 stack 是否为空——通过调用底层容器的 **empty** 成员函数实现，以及
- **size** 获取 stack 的元素个数——通过调用底层容器的 **size** 成员函数实现。

图 13.10 演示了 stack。该示例创建三个 int 类型的 stack，分别使用 **deque**（第 26 行）、**vector**（第 27 行）和 **list**（第 28 行）作为底层数据结构。

```cpp
// fig13_10.cpp
// Standard library stack adaptor class
#include <iostream>
#include <list> // list class-template definition
#include <ranges>
#include <stack> // stack adaptor definition
#include <vector> // vector class-template definition

// pushElements generic lambda to push values onto a stack
auto pushElements = [](auto& stack) {
    for (auto i : std::views::iota(0, 10)) {
        stack.push(i); // push element onto stack
        std::cout << stack.top() << ' '; // view (and display) top element
    }
};

// popElements generic lambda to pop elements off a stack
auto popElements = [](auto& stack) {
    while (!stack.empty()) {
        std::cout << stack.top() << ' '; // view (and display) top element
        stack.pop(); // remove top element
    }
};

int main() {
    std::stack<int> dequeStack{}; // uses a deque by default
    std::stack<int, std::vector<int>> vectorStack{}; // use a vector
    std::stack<int, std::list<int>> listStack{}; // use a list

    // push the values 0-9 onto each stack
    std::cout << "Pushing onto dequeStack: ";
    pushElements(dequeStack);
    std::cout << "\nPushing onto vectorStack: ";
    pushElements(vectorStack);
    std::cout << "\nPushing onto listStack: ";
    pushElements(listStack);

    // display and remove elements from each stack
    std::cout << "\n\nPopping from dequeStack: ";
    popElements(dequeStack);
    std::cout << "\nPopping from vectorStack: ";
    popElements(vectorStack);
    std::cout << "\nPopping from listStack: ";
    popElements(listStack);
    std::cout << '\n';
}
```

```text
Pushing onto dequeStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto vectorStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto listStack: 0 1 2 3 4 5 6 7 8 9

Popping from dequeStack: 9 8 7 6 5 4 3 2 1 0
Popping from vectorStack: 9 8 7 6 5 4 3 2 1 0
Popping from listStack: 9 8 7 6 5 4 3 2 1 0
```

**图 13.10** | 标准库 stack 适配器类。

泛型 lambda pushElements（第 10–15 行）将 0–9 压入一个 stack。第 32、34 和 36 行对每个 stack 调用此 lambda。第 12 行使用函数 push（每个适配器类都提供）将一个整数放到 stack 的顶部。第 13 行使用 stack 函数 top 获取 stack 的顶部元素用于输出。函数 top 不会移除顶部元素。

泛型 lambda popElements（第 18–23 行）从 stack 中弹出元素。第 40、42 和 44 行对每个 stack 调用此 lambda。第 20 行使用 stack 函数 top 获取 stack 的顶部元素用于输出。第 21 行使用函数 pop（每个适配器类都提供）移除 stack 的顶部元素。函数 pop 不返回值。因此，在从 stack 中弹出该元素之前，必须先调用 top 获取顶部元素的值。

### 13.12.2 queue 适配器

queue 类似于排队等待的队伍。排在队伍最前面的元素最先被移除。因此，queue 被称为先进先出（FIFO）数据结构。类 queue（来自头文件 `<queue>`）只允许在底层数据结构的后端插入，并且只允许从前端删除。queue 将其元素存储在 list 或 deque 序列容器对象中——默认是 deque。²¹ queue 的常用操作包括

- **push** 在 queue 的**后端**插入一个元素——通过调用底层容器的 **push_back** 成员函数实现，
- **emplace** 在 queue 的**后端**就地构造一个元素，
- **pop** 移除 queue 的**前端**元素——通过调用底层容器的 **pop_front** 成员函数实现，
- **front** 获取对 queue 的**第一个**元素的引用——通过调用底层容器的 **front** 成员函数实现，
- **back** 获取对 queue 的**最后一个**元素的引用——通过调用底层容器的 **back** 成员函数实现，
- **empty** 判断 queue 是否为空——这会调用底层容器的 **empty** 成员函数，以及
- **size** 获取 queue 的元素个数——这会调用底层容器的 **size** 成员函数。

图 13.11 演示了 queue 适配器类。第 7 行实例化一个 double 类型的 queue。第 10–12 行使用 push 向 queue 添加元素。第 17–20 行中的 while 语句使用 empty（所有容器都提供）判断 queue 是否为空（第 17 行）。当 queue 中还有更多元素时，第 18 行使用 front 读取（但不移除）queue 的第一个元素用于输出。第 19 行使用 pop（所有适配器类都提供）移除 queue 的第一个元素。

```cpp
// fig13_11.cpp
// Standard library queue adaptor class template.
#include <iostream>
#include <queue> // queue adaptor definition

int main() {
    std::queue<double> values{}; // queue with doubles

    // push elements onto queue values
    values.push(3.2);
    values.push(9.8);
    values.push(5.4);

    std::cout << "Popping from values: ";

    // pop elements from queue
    while (!values.empty()) {
        std::cout << values.front() << ' '; // view front element
        values.pop(); // remove element
    }

    std::cout << '\n';
}
```

```text
Popping from values: 3.2 9.8 5.4
```

**图 13.11** | 标准库 queue 适配器类模板。

### 13.12.3 priority_queue 适配器

类 priority_queue（来自头文件 `<queue>`）允许按排序顺序插入底层数据结构，并允许从底层数据结构的前端删除。默认情况下，priority_queue 将其元素存储在 vector 中。²² 添加到 priority_queue 的元素按优先级顺序插入，因此最高优先级的元素将最先被移除。这通常通过将元素组织为堆²³来实现，该堆始终将其最高优先级元素保持在数据结构的前端。元素比较默认使用比较器函数对象 `less<T>` 执行。

priority_queue 的操作包括

- **push** 根据**优先级顺序**将元素插入适当位置。
- **emplace** 就地构造元素，并重新将 priority_queue 按优先级顺序排序。
- **pop** 移除 priority_queue 中最高优先级的元素。
- **top** 获取对 priority_queue 顶部元素的引用——通过调用底层容器的 **front** 成员函数实现。
- **empty** 判断 priority_queue 是否为空——通过调用底层容器的 **empty** 成员函数实现。
- **size** 获取 priority_queue 的元素个数——通过调用底层容器的 **size** 成员函数实现。

图 13.12 演示了 priority_queue。第 7 行实例化一个 double 类型的 priority_queue，并使用 vector 作为底层数据结构。第 10–12 行使用成员函数 push 向 priority_queue 添加元素。第 17–20 行使用 empty 成员函数（所有容器都提供）判断 priority_queue 是否为空（第 17 行）。如果不为空，第 18 行使用 priority_queue 函数 top 获取 priority_queue 中最高优先级的元素（即最大值）用于输出。第 19 行调用 pop（所有适配器类都提供）移除 priority_queue 中最高优先级的元素。

21. “queue。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/container/queue.
22. “std::priority_queue。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/container/priority_queue
23. 不要与用于动态分配内存的堆混淆。参见第 14.4.14 节。

