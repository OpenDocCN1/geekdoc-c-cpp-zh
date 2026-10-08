

-   `unordered_map` 需要一个相等函数（默认是 `==`）；它在元素之间不保持任何顺序。

在函数良好的情况下，对于大型容器，`unordered_map` 比 `map` 快得多。然而，如果由于哈希函数很差，`unordered_map` 的最坏情况会比 `map` 糟糕得多。

## 12.7 分配器 (Allocators)

默认情况下，标准库容器使用 `new` 分配空间。`new` 和 `delete` 运算符提供了一个空闲（也称为动态内存），它可以容纳任意大小和由用户控制生命周期的对象。因此，标准库容器提供了安装我们所需的语义的分配器的机会。这被用于解决与性能（例如池分配器）、安全（在删除时清理内存的分配器）、每线程分配以及非均质性内存分配器（在具有特定指针类型的特定内存中分配）相关的各种问题。这里不是讨论这些重要、但非常专业且高级的技术的地方。然而，我将给出一个由现实问题启发的示例，在该问题中池分配器是解决方案：

一个重要的长时间运行系统使用事件队列（见 §18.4），使用作为事件的 `shared_ptr` 传递事件。这样，事件的使用者就会隐式地删除它：

点击此处查看代码图像

```
struct Event {
    vector<int> data = vector<int>(52);
};

list<shared_ptr<Event>> q;

void producer() {
    for (int n = 0; n!=nLOT; ++n) {
        lock_guard lock(m);
        q.push_back(make_shared<Event>());
        cv.notify_one();
    }
}
```

从逻辑角度来看，这运行得很好。逻辑上确实如此，代码是健壮且易于维护的。遗憾的是，这导致了内存碎片。在 16 个生产者和 4 个消费者之间传递了 100,000 个事件后，消耗了超过 6GB 的内存。

碎片问题的传统解决方案是重写代码以使用池分配器。池分配器管理固定大小的对象，并一次为许多对象分配空间，而不是使用单独的分配。幸运的是，C++为此提供了直接支持。池分配器定义在 `std` 的 `pmr`（“多态内存资源”）子命名中。

点击此处查看代码图像

```
pmr::synchronized_pool_resource;
```

我创建了一个池

```
struct Event {
    vector<int> data = vector<int>(512,&pool);
};
```

```
list<shared_ptr<Event>> q (&pool);
// q 使用池
```

```
void producer() {
    for (int n = 0; n<nLOT; ++n) {
        scoped_lock lock(m); // m 是互斥锁 ($18.3)
        q.push_back(allocate_shared<Event,pmr::polymorphic_allocator<Event>>(&pool));
        cv.notify_one();
    }
}
```

现在，16 个生产者和 4 个消费者传递了 1000 个事件，消耗的内存不到 3MB。这大约是 200 倍的改进！自然，实际使用的内存量（与碎片浪费的内存相比）没有变化。在消除碎片后，内存随时间保持稳定，因此系统可以运行数月。

这类技术在 C++ 早期就已经应用并效果良好，但通常需要将代码重写为专门的容器。现在，标准容器只需要分配器。默认情况下容器使用 `new` 和 `delete`。其他多态内存资源包括：

-   `unsynchronized_polymorphic_resource`；多态资源只能由一个线程使用。
-   `monotonic_polymorphic_resource`；一种快速分配器，仅在销毁时释放其内存，且只能由一个线程使用。

多态资源必须派自 `memory_resource` 并定义成员 `allocate()`、`deallocate()` 和 `is_equal()`。其核心思想是让用户构建自己的资源来调整代码。

## 12.8 容器概览 (Container Overview)

标准库提供了一些最实用且通用的容器类型，允许程序员选择最符合应用程序需求的容器：

| 标准容器总结 |
|------|
| `vector<T>` | 变尺寸的向量 ($12.2) |
| `list<T>` | 双向链表 ($12.3) |
| `forward_list<T>` | 单向链表 |
| `deque<T>` | 双端队列 |
| `map<K,V>` | 关联数组 ($12.5) |
| `multimap<K,V>` | 一个键可以对应多个值的 map |
| `unordered_map<K,V>` | 使用哈希查找的 map ($12.6) |
| `unordered_multimap<K,V>` | 使用哈希查找的重映射 map |
| `set<T>` | 集合（一个只有键没有值的 map） |
| `multiset<T>` | 元素可以出现多次的集合 |
| `unordered_set<T>` | 使用哈希查找的集合 |
| `unordered_multiset<T>` | 使用哈希查找的重值集合 |

无序容器（unordered containers）针对使用值（通常是字符串）的查找进行了优化；换句话说，它们是哈希。
容器定义在 `std` 命名空间中，并在头文件 `<vector>`、`<list>`、`<map>` 等中 ($9.3)。此外，标准库提供了容器适配器 `queue<T>`、`stack<T>` 和 `priority_queue<T>`。如果需要，请查询它们。标准库还提供了专门的类容器类型，例如 `array<T,N>` ($15.3) 和 `bitset<N>` ($15.2)。
标准容器及其基本操作在符号表示上被设计得是简单的。此外，各种类型容器的操作含义是等价的。基本操作适用于其有意义且可以实现的容器：

| 操作 | 说明 |
|------|---|
| `p=c.begin()` | p 指向 c 的第一个元素；对于常量迭代器使用 `cbegin()` |
| `p=c.end()` | p 指向 c 最后一个元素之后的位置；对于常量迭代器使用 `cend()` |
| `k=c.size()` | k 是 c 中元素的数量 |
| `c.empty()` | c 是否为空？ |
| `k=c.capacity()` | k 是 c 在不进行新分配的情况下可以容纳的元素数量 |
| `c.reserve(k)` | 将容量增加到 k；如果 $k<c.capacity()$，则 `reserve(k)` 不起作用 |
| `c.resize(k)` | 将大小调整为 k |
| `c.push_back(k)` | 在 c 尾部添加元素 |
| `c.emplace_back(k)` | 在 c 尾部就地构造元素 |

