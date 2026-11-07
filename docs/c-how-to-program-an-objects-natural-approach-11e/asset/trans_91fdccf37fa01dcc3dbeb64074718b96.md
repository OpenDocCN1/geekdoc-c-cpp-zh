
其第二个参数中指定的值。第 92 行使用列表成员函数 `remove` 从列表中删除值 4 的所有副本。

```cpp
// replace contents of values with elements of otherValues
values.assign(otherValues.begin(), otherValues.end());
std::cout << "\nAfter assign, values contains: ";
printList(values);

// remove otherValues elements and insert into values in sorted order
values.merge(otherValues);
std::cout << "\nAfter merge, values contains: ";
printList(values);

values.remove(4); // remove all 4s
std::cout << "\nAfter remove(4), values contains: ";
printList(values);
std::cout << "\n";
}
```

```text
After assign, values contains: 2 3 4 6 8
After merge, values contains: 2 2 3 3 4 4 6 8 8
After remove(4), values contains: 2 2 3 3 6 8 8
```

## 13.10 **deque 序列容器**

类 deque（头文件 `<deque>`）——是“double-ended queue”的简称——在一个容器中提供了 vector 和 list 的许多优点。它的实现可提供高效的索引访问（使用下标操作）来读取和修改元素，就像 vector 或数组一样。它还像 list 一样，**能在其前端和后端高效插入和删除**。类 deque 支持随机访问迭代器，因此 deque 可用于所有标准库算法。deque 的一个常见用途是维护元素先进先出队列。事实上，deque 是队列适配器<sup>16</sup>（第 13.12.2 节）的默认容器。

deque 的额外存储空间可以在任一端按内存块分配，这些内存块通常维护为**指向这些块的指针的内置数组**。<sup>17</sup> 由于 deque 的**非连续内存布局**，其迭代器必须比 vector、数组或内置数组的迭代器更“智能”。deque 提供与 vector 相同的操作，但像 list 一样，增加了成员函数 `push_front` 和 `pop_front`，以便在 deque 开头高效插入和删除。

图 13.5 演示了 deque 的若干特性。图 13.2 至图 13.4 中介绍的许多函数也可用于 deque。

```cpp
// fig13_05.cpp
// Standard library deque class template.
#include <algorithm> // copy algorithm
#include <deque> // deque class-template definition
#include <iostream>
#include <iterator> // ostream_iterator

int main() {
    std::deque<double> values; // create deque of doubles
    std::ostream_iterator<double> output(std::cout, " ");

    // insert elements in values
    values.push_front(2.2);
    values.push_front(3.5);
    values.push_back(1.1);

    std::cout << "Values contains: ";

    // use subscript operator to obtain elements of values
    for (size_t i{0}; i < values.size(); ++i) {
        std::cout << values[i] << ' ';
    }

    values.pop_front(); // remove first element
    std::cout << "\nAfter pop_front, values contains: ";
    std::ranges::copy(values, output);

    // use subscript operator to modify element at location 1
    values[1] = 5.4;
    std::cout << "\nAfter values[1] = 5.4, values contains: ";
    std::ranges::copy(values, output);
    std::cout << "\n";
}
```

```text
Values contains: 3.5 2.2 1.1
After pop_front, values contains: 2.2 1.1
After values[1] = 5.4, values contains: 2.2 5.4
```

**图 13.5**  标准库 deque 类模板。

第 9 行实例化一个可存储 double 值的 deque，然后第 13–15 行使用成员函数 **push_front** 和 **push_back** 在 deque 的开头和末尾插入元素。第 20–22 行使用下标运算符获取每个元素的值以便输出。循环条件使用成员函数 size 确保我们不会尝试访问 deque 边界之外的元素。这里我们使用计数器控制的 for 循环，仅仅是为了演示 [] 运算符。通常，应使用基于范围的 for 循环来处理容器的所有元素。

第 24 行使用 **pop_front** 删除 deque 的第一个元素。第 29 行使用下标运算符获得左值，并用其为 deque 的第 1 个元素赋新值。

## 13.11 **关联容器**

关联容器提供通过键直接存储和检索元素的能力。四种有序关联容器是 **multiset、set、multimap** 和 **map**。它们中的每一种都按键的排序顺序维护键。还有四种对应的无序关联容器——**unordered_multiset、unordered_set、unordered_multimap** 和 **unordered_map**——它们提供与有序对应容器大致相同的能力。**有序关联容器与无序关联容器的主要区别在于，无序关联容器不按键的排序顺序维护键。** 如果键不可比较，则必须使用无序容器。本节重点介绍有序关联容器。

在不需要按键的排序顺序维护键的情况下，无序关联容器通过哈希提供更好的查找性能——**O(1)**，最坏情况为 **O(n)**，而有序关联容器为 **O(log n)**。但是，这要求键可哈希。有关可哈希类型的要求，请参阅 `std::hash` 的文档。有关哈希的介绍，请参阅第 13.3 节。

遍历有序关联容器时，会按该容器的排序顺序进行遍历。类 multiset 和 set 提供用于操作值集合的操作，其中值本身就是键。**multiset 与 set 的主要区别在于，multiset 允许重复键，而 set 不允许。** 类 multimap 和 map 提供用于操作与键关联的值的操作（这些值有时称为映射值）。**multimap 与 map 的主要区别在于，multimap 允许同一个键对应多个值，而 map 每个键只允许一个值。** 除了常见的容器成员函数外，有序关联容器还支持若干关联容器特有的成员函数。可以使用 **merge** 函数合并同类型关联容器的内容。接下来几个小节将介绍有序关联容器及其常见成员函数的示例。

### 13.11.1 **multiset 关联容器**

**multiset** 有序关联容器（来自头文件 `<set>`）提供键的快速存储和检索，并允许重复键。元素的顺序由比较器函数对象确定。函数对象是重载了圆括号运算符的类的实例，使得该对象可以像函数一样被“调用”。例如，在整数 **multiset** 中，可以通过使用比较器函数对象 `less<int>` 对键排序，从而按升序排列元素；该函数对象知道如何比较两个 int 值以确定第一个是否小于第二个。这使得整数 **multiset** 能按升序排列其元素。第 14.5 节详细讨论函数对象。这里，我们只展示在声明有序关联容器时如何使用 `less<int>`。

所有有序关联容器中键的数据类型都必须支持基于**比较器函数对象**的比较——使用 `less<T>` 排序的键必须支持用 `operator<` 进行比较。如果有序关联容器中使用的键是用户定义的数据类型，则这些类型必须提供比较运算符。**multiset 支持双向迭代器。** 如果键的顺序不重要，可考虑 **unordered_multiset**（头文件 `<unordered_set>`），但请记住它只支持前向迭代器。

### 创建 multiset

图 13.6 演示了键为 int 且按升序排序的 **multiset 有序关联容器**。容器 **multiset** 和 **set**（第 13.11.2 节）提供相同的基本功能。第 12 行创建该 multiset，使用函数对象 `std::less<int>` 指定键的排序顺序。编译器知道该 multiset 包含 int 值，因此可以将 `std::less<int>` 简写为 `std::less<>`——编译器会推断 `std::less` 比较的是 int 值。此外，`std::less<>` 是 **multiset** 的默认值，因此第 12 行可以简化为

```
std::multiset<int> ints{};  // multiset of int values
```

```cpp
// fig13_06.cpp
// Standard library multiset class template
#include <algorithm> // copy algorithm
#include <format>
#include <iostream>
#include <iterator> // ostream_iterator
#include <ranges>
#include <set> // multiset class-template definition
#include <vector>

int main() {
    std::multiset<int, std::less<int>> ints{}; // multiset of int values
```

**图 13.6**  |  标准库 multiset 类模板。

### multiset 成员函数 count

第 13 行使用函数 **count**（所有关联容器均可用）统计当前 **multiset** 中值 15 的出现次数。

```
std::cout << std::format("15s in ints: {}\n", ints.count(15));
```

```text
15s in ints: 0
```

### multiset 成员函数 insert

第 16–17 行使用 **insert** 成员函数的若干重载版本之一，将值 15 两次添加到 multiset 中。**insert** 的第二个版本接受一个迭代器和一个值作为参数，并从指定的迭代器位置开始搜索插入点。**insert** 的第三个版本接受两个指定公共范围的迭代器，从另一个容器向 **multiset** 添加元素。有关其他若干重载版本，请参见

https://en.cppreference.com/w/cpp/container/multiset/insert

