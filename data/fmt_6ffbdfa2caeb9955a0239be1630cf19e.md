
`unordered_map` 与 `map` 的区别在于它不维护元素的顺序。给定一个良好的哈希函数，对于大型容器，`unordered_map` 比 `map` 快得多。然而，在哈希函数糟糕的情况下，`unordered_map` 的最坏情况性能比 `map` 糟糕得多。

## 12.7 分配器

默认情况下，标准库容器使用 `new` 分配空间。`new` 和 `delete` 运算符提供了一个自由存储区（也称为动态内存或堆），它可以存放任意大小且由用户控制生命周期的对象。这意味着会产生时间和空间开销，而这些开销在特殊情况下是可以被消除的。因此，标准库容器提供了在需要时安装具有特定语义的分配器的机会。这被用于解决与性能（例如，池分配器）、安全（作为内存清理一部分的分配器）、每线程分配以及非统一内存架构（在特定内存中分配并使用匹配的指针类型）相关的各种问题。这里不是讨论这些内容的地方，它们是非常专业且通常是高级的技术。然而，我将提供一个由真实世界启发的示例，其中池分配器是解决方案。

一个重要的、长期运行的系统使用事件队列（见 §18.4），使用 `vector` 作为传递 `shared_ptr` 的事件。最后一个事件会隐式地删除它：

```cpp
struct Event {
    vector<int> data = vector<int>{512};
};

list<shared_ptr<Event>> q;

void producer() {
    for (int n = 0; n < LOTS; ++n) {
        lock_guard lock(m); // m 是互斥锁，见 §18.3
        q.push_back(make_shared<Event>());
        cv.notify_one(); // cv 是条件变量，见 §18.4
    }
}
```

从逻辑角度来看，这运行得很好。它在逻辑上是合理的，因此代码是健壮且可维护的。遗憾的是，这导致了严重的碎片。在 16 个生产者和 4 个消费者之间传递了 100,000 个事件后，消耗了超过 6GB 的内存。

碎片问题的传统解决方案是重写代码使用池分配器。池分配器是一种管理固定大小对象并一次性为多个对象分配空间的分配器，而不是使用单独分配。幸运的是，C++ 提供了直接支持。池分配器定义在 std 的 `pmr`（“多态内存资源”）命名空间中。

```cpp
pmr::synchronized_pool_resource pool; // 创建一个池
```

```cpp
struct Event {
    vector<int> data = vector<int>{512, pool};
};; // 让 Events 使用该池
```

```cpp
list<shared_ptr<Event>> q (&pool); // 让 q 使用该池
```

```cpp
void producer() {
  for (int n = 0; n != LOTS; ++n) {
    scoped_lock lk(m);
    // m 是互斥锁 (§18.3)
    q.push_back(allocate<Event, pmr::polymorphic_allocator<Event>>(&pool));
    cv.notify_one();
  }
}
```

现在，在 16 个生产者和 4 个消费者之间传递了 100,000 个事件后，消耗的内存小于 3MB。这大约改进了 2000 倍！实际上实际使用的内存量（与碎片浪费的内存相比）并没有变化。在消除碎片后，内存保持稳定，直到系统可以运行数月。这类技术从 C++ 早期开始已得到良好效果，但通常需要重写代码以使用特殊容器。现在，容器的标准是使用 `new` 和 `delete`。其他多态资源包括：

- `unsynchronized_polymorphic_resource`；例如 `polymorphic_resource` 只能由一个线程使用。
- `monotonic_polymorphic_resource`；作为一种快速分配器，仅在析构时释放内存，且只能由一个线程使用。

多态资源必须派生自 `memory_resource` 并定义成员 `allocate()`、`deallocate()` 和 `is_equal()`。其理念是让用户构建自己的资源来调优代码。

## 12.8 容器概览

标准库提供了一些最通用且实用的容器类型，允许程序员选择最符合应用程序需求的容器：

| 标准容器摘要 | 描述 |
| :--- | :--- |
| `vector<T>` | 变长度的 vector (§12.2) |
| `list<T>` | 双向链表 (§12.3) |
| `forward_list<T>` | 单向链表 |
| `deque<T>` | 双端队列 |
| `map<K,V>` | 关联数组 (§12.5) |
| `multimap<K,V>` | 键可以出现多次的 map |
| `unordered_map<K,V>` | 使用哈希查找的 map (§12.6) |
| `unordered_multimap<K,V>` | 使用哈希查找的 multimap |
| `set<T>` | set（带有键但没有值的 map） |
| `multiset<T>` | 值可以出现多次的 set |
| `unordered_set<T>` | 使用哈希查找的 set |
| `unordered_multiset<T>` | 使用哈希查找的 multiset |

`unordered` 容器针对键（通常是字符串）的查找进行了优化；换句话说，它们是哈希表。

容器定义在 `std` 命名空间中，并在 `<vector>`, `<list>`, `<map>` 等头文件中给出 (§9.4)。此外，标准库还提供了容器适配器 `queue<T>`、`stack<T>` 和 `priority_queue<T>`。如果需要，请查询它们。标准库还提供了更专门的类容器类型，如 `array<T,N>` (§15.3.1) 和 `bitset<N>` (§15.3.2)。

标准容器及其基本操作从名义上被设计为相似的。此外，这些操作的机制对于各种容器都是高效的。基本操作适用于所有有意义且可以高效实现的各种容器：

### 标准容器操作（部分内容）

| value_type | 描述 |
| :--- | :--- |
| `p=c.begin()` | `p` 指向 `c` 的第一个元素；`cbegin()` 返回指向 const 的迭代器 |
| `p=c.end()` | `p` 指向 `c` 最后一个元素的之后；同样 `cend()` 返回指向 const 的迭代器 |
| `k=c.size()` | `k` 是 `c` 中元素的数量 |
| `c.empty()` | `c` 是否为空？ |
| `k=c.capacity()` | `k` 是 `c` 可以容纳的元素数量 |
| `c.reserve(k)` | 如果需要，将容量增加到 `k` |
| `c.resize(k)` | 将容器大小调整为 `k` 个元素 |
| `c.at(k)` | 访问索引 `k` 处的元素，如果无效则抛出 `out_of_range` |
| `c.push_back(x)` | 将 `x` 添加到 `c` 的末尾 |
| `c.emplace_back(a)` | 在末尾直接构造元素 |
| `c.insert(p, x)` | 在位置 `p` 前插入元素 |
| `c.erase(p)` | 删除位置 `p` 处的元素 |
| `b=c` | 容器内容的赋值 |
| `b==c` | 等性检查 |
| `b<c` | 字典序比较 |
| `b>c` | 字典序比较 |

- [27] 检查你是否有一个可接受哈希函数的实验；§12.6。
- [28] 通过使用异或运算符 (`^`) 组合元素的标准哈希函数得到的哈希函数通常是很好的；§12.6。
- [29] 熟悉标准库容器，并优先使用它们而不是手工构造的数据结构；§12.8。
- [30] 如果你的应用程序面临内存相关的性能问题，请尽量减少自由存储（free store）的使用和/或考虑使用特殊的分配器；§12.7。

# 13 算法

> 不要在一个必要的情况下增加实体。– 威廉·奥卡

* 引言
* 迭代器的使用
* 迭代器类型
  * 流迭代器
* 谓词的使用
* 算法概述
* 并行算法
* 建议

## 13.1 引言

数据结构（如 `list` 或 `vector`）本身并没有很有用。要使用它们，我们需要基本访问的操作，例如添加和删除元素（如 `list` 和 `vector` 所提供的）。此外，我们很少仅仅将对象存储在容器中。我们对它们进行排序、打印、提取子集、删除元素、搜索对象等。因此，标准库通过提供最多的容器类型提供了容器最常用的算法。例如，我们可以简单高效地对一个 `list`：`vector` 元素并放置每个唯一 `vector` 元素的拷贝和 `Entries`。

```cpp
void f(vector<Entry>& vec, list<Entry>& lst)
{
  sort(vec.begin(), vec.end());
  unique_copy(vec.begin(), vec.end(), lst.begin());
}
```

为了使此代码工作，`Entry` 必须定义小于（`<`）和等于（`==`）。例如：

```cpp
bool operator<(const Entry& x, const Entry& y) const 
{ return x.name < y.name; // 按它们的名称对 Entries 排序 }
}
```

标准算法是用元素的（半开区间）序列表示的。序列由一对迭代器表示，指定第一个元素和最后一个元素之后的元素：

- 迭代器：`begin()`, `end()`
- 元素：

在示例中，`sort()` 排序了由迭代器对 `vec.begin()` 和 `vec.end()` 定义的序列，这正好是 `vector` 的所有元素。对于写入（输出），我们需要指定要写入的第一个元素。如果写入了多个元素，初始元素之后的元素将被覆盖。为了避免这种情况，`list` 的元素至少要等于 `vec` 中唯一值的数量。

遗憾的是，标准库没有支持向容器进行范围检查写入的抽象。但是，我们可以定义：

显然显然，这并不是标准库级别的代码，但它展示了思路：

```cpp
vector<int> v1 (1, 2, 3); // 三元素
vector<int> v2;
```

```cpp
copy(v1, v2.begin()); // 将溢出
copy(v1, Checked_iter(v2)); // 将抛出异常
```

如果在“随机和排序”示例中，我们想将唯一元素放置在一个新的 `list` 中，我们可以这样写：

```cpp
list<Entry> f(vector<Entry> &vec)
{
  list<Entry> res;
  sort(vec.begin(), vec.end());
  unique_copy(vec.begin(), vec.end(), back_inserter(res)); // 追加到 res
  return res;
}
```

调用 `back_inserter(res)` 为 `res` 构建了一个迭代器，该迭代器向容器添加元素，扩展容器以为它们留出空间。因此，这节省了我们先分配空间再填充它的麻烦。标准容器 `back_inserter(xl)` 消除了使用 `realloc()` 进行易出错的 C 风格内存管理的需要。标准库 `list` 有一个构造函数（§6.2.2），使得按值返回 `res` 是高效的（即使对于数千个元素的列表也是如此）。

当我们发现迭代器风格的代码（如 `sort(vec.begin(), vec.end())`）繁琐时，我们可以使用范围算法并编写 `sort(vec)` (§6.5)。这两个版本是等价的。同样，`for-for` 循环大致等同于使用迭代器的 C 风格循环：

```cpp
for (auto x : v) cout << x; // 输出所有元素
for (auto p = v.begin(); p != v.end(); ++p) cout << p; // 输出所有元素
```

除了更简单且不易出错之外，范围 `for` 版本也是高效的。

## 13.2 迭代器的使用

对于容器，可以获取几个指向有用元素的迭代器；`begin()` 和 `end()` 是此的绝佳示例。此外，许多算法返回迭代器。例如，标准的 `find` 在序列中查找值并返回找到元素的迭代器：

```cpp
bool has_c(const string &s, char c)
{
  auto p = find(s.begin(), s.end(), c);
  if (p != s.end())
    return true;
  else
    return false;
}
```

正如许多标准算法，`find` 返回一个迭代器来指示是否找到：

```cpp
bool has_c(const string& s, char c)
{
    auto p = find(s.begin(), s.end(), c);
    return p != s.end();
}
```

当我们发现迭代器风格的代码（如 `sort(vec.begin(), vec.end())`）繁琐时，我们可以使用范围算法并编写 `sort(vec)` (§6.5)。这两个版本是等价的。同样，`for-for` 循环大致等同于使用迭代器的 C 风格循环：

```cpp
for (auto x : v) cout << x; // 输出所有元素
for (auto p = v.begin(); p != v.end(); ++p) cout << p; // 输出所有元素
```

除了更简单且不易出错之外，范围 `for` 版本也是高效的。
