
为了兼得两者之长，我们可以构建一个**数组**容器，它具备数组的优点而没有其缺点。**数组**现在是 `<array>` 中定义的标准的一部分，但让我们看看我们该如何定义它。这个想法既简单又实用：

```cpp
template <typename T, int N>
// requires Element<T>()
struct array {
    // not quite the standard array
    using value_type = T;
    using iterator = T*;
    using const_iterator = const T*;
    using size_type = unsigned int;
    // the type of a subscript
    T elems[N];
    // no explicit construct/copy/destroy needed
    iterator begin() { return elems; }
    const_iterator begin() const { return elems; }
    iterator end() { return elems+N; }
    const_iterator end() const { return elems+N; }
    size_type size() const;
    T& operator[](int n) { return elems[n]; }
    const T& operator[](int n) const { return elems[n]; }
    const T& at(int n) const;
    // range-checked access
    T& at(int n);
    // range-checked access
    T * data() { return elems; }
    const T * data() const { return elems; }
};
```

这个定义并不完整，也不完全符合标准，但它能让你了解其大意。如果你的实现尚未提供标准**数组**，它也能给你一些可用的东西。如果可用，它位于 `<array>` 中。请注意，因为**array<T,N>** “知道”其大小为 N，我们可以（并且确实）提供赋值、`==`、`!=` 等，就像对**vector**那样。
举个例子，让我们使用 §20.4.2 中 STL 版本的 **high()** 来配合数组使用：

```cpp
void f()
{
    array<double,6> a = { 0.0, 1.1, 2.2, 3.3, 4.4, 5.5 };
    array<double,6>::iterator p = high(a.begin(), a.end());
    cout << "the highest value was " << *p << '\n';
}
```

请注意，当我们编写 **high()** 时并没有考虑到**数组**。能够将 **high()** 用于**数组**仅仅是遵循两者标准约定后的简单结果。

## 20.10 容器概览

STL 提供了相当多的容器：

| 标准容器 | 描述 |
|---|---|
| **vector** | 连续分配的序列；将其用作默认容器 |
| **list** | 双向链表；当你需要插入和删除元素而不移动现有元素时使用它 |
| **deque** | **list** 和 **vector** 之间的折中方案；除非你对算法和机器架构有专家级知识，否则不要使用它 |
| **map** | 平衡有序树；当你需要通过值访问元素时使用它（参见 §21.6.1–3） |
| **multimap** | 允许有多个键副本的平衡有序树；当你需要通过值访问元素时使用它（参见 §21.6.1–3） |
| **unordered_map** | 哈希表；**map** 的优化版本；在大型 map 中当你需要高性能且能设计良好的哈希函数时使用（参见 §21.6.4） |
| **unordered_multimap** | 允许有多个键副本的哈希表；**multimap** 的优化版本；在大型 maps 中当你需要高性能且能设计良好的哈希函数时使用（参见 §21.6.4） |
| **set** | 平衡有序树；当你需要跟踪单个值时使用它（参见 §21.6.5） |
| **multiset** | 允许有多个键副本的平衡有序树；当你需要跟踪单个值时使用它（参见 §21.6.5） |
| **unordered_set** | 类似于 **unordered_map**，但只包含值，而不是（键，值）对 |
| **unordered_multiset** | 类似于 **unordered_multimap**，但只包含值，而不是（键，值）对 |
| **array** | 固定大小的数组，不受大多数与内置数组相关的问题困扰（参见 §20.9） |

你可以在书籍和在线文档中查阅关于这些容器及其用法的丰富信息。以下是一些高质量的信息来源：

*   Josuttis, Nicolai M. *The C++ Standard Library: A Tutorial and Reference*. Addison-Wesley, 2012. ISBN 978-0321623218. 仅使用第二版。
*   Lippman, Stanley B., Jose Lajoie, and Barbara E. Moo. *The C++ Primer*. Addison-Wesley, 2005. ISBN 0201721481. 仅使用第五版。
*   Stroustrup, Bjarne. *The C++ Programming Language*. Addison-Wesley, 2012. ISBN 978-0321714114. 仅使用第四版。
*   STL 和 iostream 库的 SGI 实现文档：www.sgi.com/tech/stl。注意，他们还提供了完整代码。

你觉得被剥夺了吗？你认为我们应该向你解释所有关于容器及其使用的知识吗？那是不可能做到的。标准设施、有用技术和有用库太多了，你无法一次性全部吸收。编程是一个极其丰富的领域，没有人能掌握所有的设施和技巧——它也可以是一门高尚的艺术。作为一名程序员，你必须养成寻找关于语言设施、库和新技术的习惯。编程是一个动态且快速发展的领域，所以仅仅满足于你已知并熟悉的内容注定会被淘汰。“查阅一下”是许多问题的完全合理的答案，随着你技能的成长和成熟，它将会越来越频繁地成为答案。

另一方面，你会发现，一旦你理解了 **vector**、**list** 和 **map** 以及第 21 章介绍的标准算法，你会发现使用其他 STL 和类 STL 容器很容易。你还会发现你具备了理解非 STL 容器及使用它们的代码的基本知识。

什么是容器？你可以在上述所有来源中找到 STL 容器的定义。这里我们只给出一个非正式的定义。STL 容器：

*   是元素序列 `[begin():end()]`。
*   提供复制元素的复制操作。复制可以通过*赋值*或复制构造函数完成。
*   将其元素类型命名为 **value_type**。
*   具有名为 **iterator** 和 **const_iterator** 的迭代器类型。迭代器提供 `*`、`++`（前缀和后缀）、`==` 和 `!=`，并具有适当的语义。**list** 的迭代器还提供 `--` 以在序列中向后移动；这被称为*双向迭代器*。**vector** 的迭代器还提供 `--`、`[]`、`+` 和 `—`，被称为**随机访问迭代器**。（参见 §20.10.1。）
*   提供 `insert()`、`erase()`、`front()` 和 `back()`、`push_back()` 和 `pop_back()`、`size()` 等；`vector` 和 `map` 还提供下标访问（例如 operator []）。
*   提供比较运算符（`==`、`!=`、`<`、`<=`、`>` 和 `>=`），用于比较元素。容器对 `<`、`<=`、`>` 和 `>=` 使用词典顺序；也就是说，它们从第一个开始按顺序比较元素。

这份列表的目的是给你一个概览。更多细节请参见附录 B。更精确的规范和完整列表请参见 *The C++ Programming Language* 或标准。

一些数据类型提供了标准容器所需的大部分功能，但并非全部。我们有时将其称为“近似容器”。其中最有趣的是：

| “近似容器” | 描述 |
|---|---|
| `T[n]` 内置数组 | 没有 `size()` 或其他成员函数；当你有选择时，首选容器，如 `vector`、`string` 或 `array`，而不是内置数组 |
| `string` | 仅包含字符，但提供对文本操作有用的操作，如连接（`+` 和 `+=`）；首选标准 string 而非其他 string |
| `valarray` | 具有向量操作的数值向量，但有许多限制以鼓励高性能实现；仅当你进行大量向量算术运算时使用 |

此外，许多人和许多组织都生产了满足标准容器要求或几乎满足的容器。
如果有疑问，请使用 `vector`。除非你有充分的理由不使用它，请使用 `vector`。

## 20.10.1 迭代器类别

我们一直在谈论迭代器，好像所有迭代器都可以互换。如果你只执行最简单的操作，例如遍历序列一次并读取每个值一次，那么它们是可以互换的。如果你想要做更多事情，例如向后迭代或下标访问，你需要更高级的迭代器之一。

