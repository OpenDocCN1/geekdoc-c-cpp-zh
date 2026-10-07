

# 序列 (Sequence)

你可以通过添加要求来完善基本概念。序列（sequence）是一个重要的细化，因为 STL 容器类型——`deque`、`forward_list` (C++11)、`list`、`queue`、`priority_queue`、`stack` 和 `vector`——都是序列。（回队列允许在末尾添加元素并从头部移除元素。由 `deque` 表示的双端队列允许在两端进行添加和删除。）要求迭代器至少是前向迭代器（forward iterator），这保证了元素按照特定的顺序排列，且这种顺序在相邻迭代循环之间不会改变。数组类也被归类为序列容器，尽管它并不满足所有的要求。

序列还要求其元素按严格的线性顺序排列。也就是说，有一个第一个元素、最后一个元素，除了第一个和最后一个之外，每个元素恰好有一个紧随在其前的和一个紧随在其后的元素。数组和链表是序列的示例，而分支结构（每个节点指向两个节点）则不是。

由于序列中的元素有确定的顺序，因此在特定位置插入和删除特定范围的操作变得可行。表 16.7 列出了这些以及序列所需的其他操作。该表使用了与表 16.5 相同的符号，增加了 `t` 表示 `t` 的值——即存储在容器中的值的类型；`n` 表示整数；以及 `p`、`q`、`i` 和 `j` 表示迭代器。

# 表 16.7 序列要求

| 表达式 | 返回类型 |  |
| --- | --- | --- |
| X (n,t); | | 声明一个包含 n 个值 t 拷贝的序列 |
| X(n, t) | | 创建一个包含 n 个值 t 拷贝的匿名序列 |
| X a (i, j) | | 声明一个由范围 [i, j] 内容初始化的序列 |
| X(i, j) | | 创建一个由范围 [i, j] 内容初始化的匿名序列 |
| a.insert(p,t) | | 在 p 之前插入一个 t 的拷贝 |
| a.insert(p,n,t) | void | 在 p 之前插入 n 个 t 的拷贝 |
| a.insert(p,i,j) | void | 在 p 之前插入范围 [i, j] 中的元素拷贝 |
| a.erase(p) | iterator | 删除 p 指向的元素 |
| a.erase(p, q) | iterator | 删除范围 [p, q] 内的元素 |
| a.clear() | void | 等同于 erase(begin(), end()) |

由于 `deque`、`list`、`queue`、`priority_queue`、`stack` 和 `vector` 模板类都是序列概念的模型，它们都支持表 16.7 中的运算符。此外，这六个模型中的某些还有可用操作。在允许的情况下，它们具有常数时间复杂度。表 16.8 列出了这些额外操作。

| 表达式 | 返回类型 | 含义 | 容器 |
| --- | --- | --- | --- |
| a.front() | T& | *a.begin() | vector, list, deque |
| a.back() | T& | *--a.end() | vector, list, deque |
| a.push_front(t) | void | *a.insert(a.begin(), t) | list, deque |
| a.push_back(t) | void | *a.insert(a.end(), t) | vector, list, deque |
| a.pop_front() | void | *a.erase(a.begin()) | list, deque |
| a.pop_back() | void | *a.erase(--a.end()) | vector, list, deque |
| a[n] | T& | *(a.begin() + n) | vector, deque |
| a.at(n) | T& | *(a.begin() + n) | vector, deque |

表 16.8 值得几句注释。首先，注意 `a[n]` 和 `a.at(n)` 都返回容器中第 n 个元素（从 0 开始计数）的引用。两者之间的区别是 `a.at(n)` 会进行边界检查，如果 `n` 超出容器的有效范围，则会抛出 `out_of_range` 异常。接下来，你可能会奇怪为什么 `push_front()` 为 `list` 和 `deque` 定义而不为 `vector` 定义。假设你想在一个包含 100 个元素的 `vector` 头部插入一个新值。为了留出现，你需要将元素 99 移动到位置 100，然后移动元素 98，以此此类推。这是一个具有线性时间复杂度的操作，移动 100 个元素花费的时间是移动单个元素的 100 倍。但表 16.8 中的操作应该只有在以常数时间复杂度执行时才被实现。`list` 和双端队列的设计允许元素添加到头部，而无需移动其他元素到新位置，因此它们可以以常数时间复杂度实现 `push_front()`。图 16.4 展示了 `push_front()` 和 `push_back()`。

# vector

你已经见过好几个使用 `vector` 模板的示例，它在 `<vector>` 头文件中被声明。简而言之，`vector` 是数组的表示。该类提供了自动内存管理，允许 `vector` 的大小动态增长，并在元素被移除时收缩。它提供了随机访问能力。元素可以在常数时间内从末尾添加或移除，但开头的插入和移除是线性时间操作。

除了是序列外，`vector` 还是可逆概念（reversible）的模型。这意味着 `rbegin()` 返回一个反向起始迭代器，`rend()` 返回反向结束迭代器。

```cpp
vector<int> v(1, 2, 3, 4, 5);
for (auto it = v.rbegin(); it != v.rend(); ++it)
    cout << *it << " "; // 输出: 5 4 3 2 1
```

`rbegin()` 返回容器中最后一个元素的迭代器，`rend()` 返回指向第一个元素之前的迭代器。假设你想在一个一个包含 100 个元素的 `vector` 头部插入一个新值。如代码所示 所示：

```cpp
vector<int> v = {1, 2, 3, 4, 5};
v.insert(v.begin(), 0); // v 现在变为 {0, 1, 2, 3, 4, 5}
```

```cpp
deque<int> d = {1, 2, 3, 4, 5};
d.push_front(0); // d 现在变为 {0, 1, 2, 3, 4, 5}
```

图 16.4 展示了 `push_front()` 和 `push_back()`。

# deque

`deque` 模板类（在 `<deque>` 头文件中声明）表示双端队列，通常被称为“双端”。它与 `vector` 类似，都支持随机访问，但它在头部插入和删除也是常数时间复杂度。

```cpp
deque<int> d = {1, 2, 3, 4, 5};
d.push_front(0); // d 现在变为 {0, 1, 2, 3, 4, 5}
d.push_back(6);  // d 现在变为 {0, 1, 2, 3, 4, 5, 6}
d.pop_front();   // d 现在变为 {1, 2, 3, 4, 5, 6}
d.pop_back();    // d 现在变为 {1, 2, 3, 4, 5}
```

# list

`list` 模板类（在 `<list>` 头文件中声明）表示双向链表。与 `vector` 不同，它不支持随机访问，但在任何位置插入和删除元素都是常数时间复杂度。

```cpp
list<int> l = {1, 2, 3, 4, 5};
l.push_front(0); // l 现在变为 {0, 1, 2, 3, 4, 5}
l.push_back(6);  // l 现在变为 {0, 1, 2, 3, 4, 5, 6}
l.pop_front();   // l 现在变为 {1, 2, 3, 4, 5, 6}
l.pop_back();    // l 现在变为 {1, 2, 3, 4, 5}
```

`list` 迭代器与 `vector` 迭代器不同，它不是随机访问迭代器，因此不能使用 `+` 或 `-` 操作。

```cpp
list<int> l = {1, 2, 3, 4, 5};
auto it = l.begin();
advance(it, 3); // it 现在指向元素 4
cout << *it;    // 输出: 4
```

`deque` 迭代器与 `list` 迭代器类似，它们不是随机访问迭代器，因此不能使用 `+` 或 `-` 操作，但它们是双向迭代器，因此可以使用 `++` 和 `--` 操作。

```cpp
deque<int> d = {1, 2, 3, 4, 5};
auto it = d.begin();
advance(it, 3); // it 现在指向元素 4
cout << *it;    // 输出: 4
```

