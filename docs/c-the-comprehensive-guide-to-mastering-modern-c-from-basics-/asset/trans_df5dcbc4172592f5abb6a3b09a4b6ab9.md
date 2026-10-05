

### 列表 24.9 迭代器适配器改变操作的行为。

每当类型为 `ostream_iterator` 的迭代器 `out_it` 被解引用并赋值时，它就会输出到 `cout`。在元素之间，它会打印一个带有空格的逗号 ", "。因此 *out_it = 42 的结果输出为 42.*。来自 `<algorithm>` 头文件的 `copy` 算法现在对 `data.begin()` 到 `data.end()` 范围内的所有元素执行恰好这种赋值。结果是你可以在 `cout` 上看到所有元素。

在 `<iterator>` 头文件中，还有其他用于迭代器的有用工具。例如，你可以使用 `reverse_iterator` 反转一个范围，或者使用 `make_move_iterator` 将拷贝算法转换为移动算法。关于具体功能，我建议参阅标准库参考，例如 https://cppreference.com。

## 24.3 分配器：内存问题

容器不断请求新内存来存储它们的元素。这是一项复杂的任务，特别是对于像 `list` 或 `set` 这样的非连续容器。为了给用户干预的能力，每个容器都配备了一个分配器。如果你不指定，它默认使用 `std::allocator<Elem>`。

## 分配器是一个专家级话题

> 我建议你使用 `std::allocator` 而不要实现你自己的分配器。如果你要实现，请使用来自 Boost 项目或其他主要提供者的分配器。当前标准库中实现的分配器概念引起了很大争议，并让所有专家都不满意。除非你真的需要，否则你不应该费精力深入研究这个课题。

为了向你展示如何使用分配器，我现在将定义一个非常简单的分配器。有很多更复杂的，但那些适用于通用和特定情况。

```cpp
// https://godbolt.org/z/3dYh6n5f
#include <set>
#include <vector>
#include <iostream>

template<class T> class GobAllocator {
public:
    using value_type = T;
    T* allocate(size_t count) {
        size_t add = sizeof(T)*count;
```

```cpp
        std::cout << "allocate"<<(buf_.size())-current_ << "current_";
    if(current_ +add > buf_.size()) throw std::bad_alloc();
    char* result = buf_.data()+current_;
    current_ += add;
    return reinterpret_cast<T*>(result);
}
void deallocate(T* p, size_t count) {
    size_t t = sizeof(T)*count;
    std::cout << "deallocate"<<del << "\n";
    if(current_ == p && reinterpret_cast<T*>(buf_.data())) {
        std::cout << "...all free.\n";
        current_ = 0; // release everything again
    }
}

GobAllocator() : GobAllocator(1024) {}
explicit GobAllocator(size_t mx)
    buf_(mx, 0),
    current_(0) { }

private:
    std::vector<char> buf;
    size_t current_;
```

```cpp
int main() {
constexpr size_t CNT = 1*1000*1000;
using Gob = GobAllocator<int>;
try {
    Gob gob(sizeof(int)); // prepare allocator
    std::vector<int,Gob> data(gob); // get memory in one go
    data.reserve(CNT);
    for(int val=0; val < (int)CNT; ++val)
        data.push_back(val);
} catch(std::bad_alloc &ex) {
    std::cout << "Memory exhausted.\n";
}
```

## 列表 24.10 一个简单的分配器及其用法。

`GobAllocator` 在创建时获取一个 `vector<char>` 作为内存储备池。当容器通过 `allocate()` 请求内存时，它可以分配内存，但它很少释放内存。容器通过 `deallocate()` 请求此操作。只有当 `deallocate()` 想要释放所有请求的内存时，`GobAllocator` 才会实际执行并释放其所有内存以供新请求。

使用 `current_`，`GobAllocator` 跟踪它已经管理了多少内存。当被要求通过 `allocate()` 为 `count` 个对象分配内存时，它简单地增加 `current_` 计数器这些对象所需的字节数。返回旧的位置作为数据存储并并转换为目标类型的原始指针。这意味着容器将它的元素存储在此位置。

同样重要的是，如果分配器未能获取请求的内存，它会抛出 `bad_alloc` 异常。这可以使用 `try/catch` 进行捕获。例如，在列表 24.10 中省略 `data.reserve(CNT);` 并观察 `GobAllocator` 如何耗尽空间：vector 现在想要持续增长，并在 `allocate()` 和 `deallocate()` 调用之间切换，以请求越来越大的内存并释放旧内存。然而，这个愚拙的分配器无法做到，最终必须放弃。

这在理论上可以用于重用已经获取过的内存。

在这里，来自 `gob` 的内存将被完全使用两次，但前提是 `data1` 或 `data2` 的增长不会超过 `cnt` 个元素：

```cpp
Gob gob(CNT*sizeof(int)); // prepare common allocator
{
  std::vector<int,Gob> data1(gob);
  data1.reserve(CNT);
  // ...
```

```cpp
  std::vector<int,Gob> data2(gob);
data2.reserve(CNT);
// ...
```

总而言之，这个简单的分配器在实践中相当没用。但它至少向你展示了如何为容器配备分配器。

## 所有容器都支持分配器

标准库中的所有容器都使用分配器。如果你不指定，标准库使用 `std::allocator<Elem>`。你可以通过传递其类型作为模板参数来指定自己的分配器。此外，你可以选择性将分配器的实例传递给构造函数，或者如果你不想，就让容器创建一个新的。

这里描述的经典分配器有一个弱点：两个本质相同但具有不同分配器的容器是不同的类型，因为分配器是容器类型的一部分。这意味着在实践中，你不能在它们之间赋值。

解决方案是带有`多态分配器`的容器。使用这些分配器的容器即使使用不同的分配器，也是相同的类型。因此，从 C++17 开始，所有容器在 `std::pmr` 命名空间可用——例如 `std::pmr::vector`（多态内存资源）。

接下来，我将省略分配器模板参数并将其作为构造函数参数传递给所有容器，以及 pmr 变体。

## 24.4 容器的共性

在设计标准库的这部分时，付出了巨大精力为容器提供了一个通用接口（在有意义的情况下）。我没有列出特殊情况——这些将在特定容器中解释——仅给出一个粗略概述：

- begin() end()
所有容器都提供这两个函数来获取迭代器。其他此外，这允许你在范围的 for 循环中使用它们，因为它们也作为自由函数存在。

- size() empty() std::size()
获取任何容器中的元素数量。从 C++17 开始，它们也作为自由函数存在，从 C++20 开始有一个自由函数 `ssize()`，它以符号形式返回 `size()`。这避免了符号和无符号比较的警告，例如 `(int i=0; i<cont.size(); ++i)`。只需写 `i<ssize(cont)`。

- resize() reserve() clear()
你可以通过单个调用调整或收缩序列容器（数组除外）。vector 和无序容器可以告知你打算存储大约多少元素。这在实际插入时节省了管理工作。

- operator[] at() data()
通过 `cont[where]` 或 `cont.at(where)` 在容器的任意位置读写。并非所有容器都支持此项。序列容器需要一个数字作为 `where`，而关联容器则需要你选择的键的数据类型。通过 `data()`，你可以访问某些容器中元素的连续内存。这对于 C 函数等非常有用。`data()` 也可以作为自由函数可用。

- insert() insert_range() emplace()
使用这些函数在任意位置插入或删除元素。注意 vector 可以这样做，但它很慢。在 `insert()` 中，元素已经存在并被拷贝（对于临时值则被移动），而对于

