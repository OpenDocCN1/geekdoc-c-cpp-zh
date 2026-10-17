
```cpp
template <typename T> struct my_allocator {
  using value_type = T;

  my_allocator() = default;

  template <typename U> my_allocator(const my_allocator<U>&) {}

  T* allocate(size_t n, void* hint = nullptr) {
    return static_cast<T*>(operator new(n * sizeof(T)));
  }

  void deallocate(T* p, size_t n) {
    operator delete(p);
  }

  friend bool operator==(const my_allocator<T>& a, const my_allocator<U>& b) {
    return true;
  }

  friend bool operator!=(const my_allocator<T>& a, const my_allocator<U>& b) {
    return !(a == b);
  }
};
```

# reference

`const_reference`

对 (const) `T` 的引用的类型。

对于作为标准库容器模板参数的分配器，定义必须为：

```cpp
typedef T& reference;
typedef T const& const_reference;
```

`pointer address(reference)`

`const_pointer address(const_reference)`

给定一个 (const) `T` 的引用，产生指向 (const) `T` 的指针函数。

对于作为标准库容器模板参数的分配器，要求定义为：

```cpp
pointer address(reference r) { return &r; }
const_pointer address(const_reference r) { return &r; }
```

这些函数 intended为了抽象内存模型。遗憾的是，为了与标准库容器保持兼容，它们受到了束缚，因为标准库容器需要指针实际上是*裸指针*，这样随机访问迭代器和二分搜索才能高效工作。

尽管这些定义对于标准库容器使用的分配器来说有固定值，但这些定义是必须的，因为 C++98 中的容器代码 使用了它们。例如：

```cpp
typedef size_type allocator::size_type;
```

一些开发者从 `std::allocator` 派生他们的分配器模板，以便无需编写即可获得这些定义。但这种做法是有争议的。毕竟，`std::allocator` 终有一天会改变。它在早期的后期发生过变化，但这些定义是有充分根据的。另一种方法是简单的将这些不变的定义提取出来，如下

```cpp
template <typename T> struct std_allocator_defs {
  typedef T value_type;
  typedef T* pointer;
  typedef T const* const_pointer;
  typedef T& reference;
  typedef T const& const_reference;
  typedef size_t size_type;
  typedef ptrdiffiff_t difference_type;

  pointer address(reference r) { return &r; }
  const_pointer address(const_reference r) { return &r; }
};
```

推到逻辑结论，这些定义可以变成 traits 类（特征类），网络上一些复杂的分配器模板正是这样做。这也是 C++11 最小分配器所做的，只是 traits 类是从正常情况反向操作的。traits 类查看分配器模板是否具有这些定义中的任何，如果分配器没有，则提供标准定义。然后，容器代码引用 `allocator_traits` 类，而不是分配器，如下

```cpp
typedef std::allocator_traits<MyAllocator<T>>::value_type value_type;
```

处理完这些模板代码后，是时候查看重要的定义了（记住，第 346 页“最小 C++11 分配器”中讨论的最小分配器定义也包含在内）：

```cpp
void construct(pointer p, const T&)
```

该函数使用 `new` 拷贝构造 `T` 的实例：

```cpp
new(p) T(val);
```

对于 C++11，此函数可以定义为可以向构造函数提供参数：

```cpp
template <typename U, typename... Args>
void construct(U* p, Args&&... args) {
  new(p) U(std::forward<Args>(args...));
}
```

`destroy(pointer p)`

该函数销毁指向 `T` 的指针，调用 `p->~T()`。

`rebind:value`

`struct rebind` 的声明位于分配器的核心。它通常看起来如下：

```cpp
template <typename U> struct rebind {
  typedef allocator<U> value;
};
```

`rebind` 给出了给定 `allocator<T>::list<T>` 的情况下，为新类型 `U` 创建分配器的公式。每个分配器都必须提供此项。这是 `std::list<T>` 这样的容器分配 `std::list<T>` 实例的方式。在大多数容器中，不分配 `T` 的节点是很重要的。

示例 13-8 是一个完整的 C++98 风格分配器，等同于示例 13-7 中的 C++11 最小分配器。

## 示例 13-8. C++98 分配器

```cpp
template <typename T> struct my_allocator_98 :
  public std_allocator_defs<T> {
  template <typename U> struct rebind {
    typedef my_allocator_98<U> other;
  };

  my_allocator_98() { /*empty*/ }
  my_allocator_98(const my_allocator_98&) { /*empty*/ }

  void construct(pointer p, const T& t) {
    new(p) T(t);
  }

  void destroy(pointer p) {
    p->~T();
  }

  size_type max_size() const {
    return std::allocator<T>::max_size();
  }

  pointer allocate(size_type n) {
    return reinterpret_cast<pointer>(::operator new(n * sizeof(T)));
  }

  void deallocate(pointer p, size_type n) {
    ::operator delete(p);
  }

  template <typename U>
  inline bool operator==(const my_allocator_98<T>&, const my_allocator_98<U>&) {
    return true;
  }

  template <typename U, typename U2>
  inline bool operator!=(const my_allocator_98<U>& a, const my_allocator_98<U2>& b) {
    return !(a == b);
  }
};
```

在互联网上检查分配器代码时，开发者会遇到各种不同的类型。一个谨慎的开发者会这样写 `allocate()` 函数的签名：

```cpp
pointer allocate(
  size_type n,
  typename std::allocator<T>::const_pointer = 0);
```

而一个不太谨慎的开发者可能会为用于标准库容器的分配器写相同的签名：

```cpp
T* allocate(size_t n, void* = 0);
```

第一种签名是最符合技术标准的，第二种签名可以成功编译并具有简洁的优点。这就是模板荒野世界中的运作方式。

互联网上分配器代码的另一个问题是，如果无法满足请求，必须抛出 `std::bad_alloc`。因此，例如以下代码调用 `malloc()` 分配内存是不符合标准的：

```cpp
pointer allocate(
    size_type n,
    typename std::allocator<T>::const_pointer = nullptr) {
    return reinterpret_cast<T*>(malloc(n * sizeof(T)));
};
```

# 一个固定块分配器

标准库类 `std::list`、`std::map`、`std::multimap`、`std::set` 和 `std::multiset` 使用了分配器。固定块分配器在示例 13-9 中显示。示例 13-8 是一个完整的 C++98 风格分配器，等同于示例 13-7 中的 C++11 最小分配器。

# 用于字符串的固定块分配器

`std::string` 将其内容存储在 `char` 的动态数组中。由于数组会随着字符串的增长而重新分配到更大的尺寸，它似乎并不是前一节中简单固定块分配器的候选对象。有时甚至这种局限性也可以被克服。如果开发者知道程序中可能接收字符串的最大大小，就可以创建一个始终产生最大大小固定尺寸块的分配器。这种情况意外地常见，因为百万字符字符串的应用场景有限。

示例 13-11 是用于字符串的固定块分配器的部分列表。

## 示例 13-11. 用于字符串的固定块分配器

```cpp
template <typename T> class NewAllocator {
public:
    pointer allocate(size_type n,
        typename std::pointer<const void> const nullptr = ::nullptr)
        return reinterpret_cast<pointer>(string_memory_manager.allocate(512));

    void deallocate(pointer p, size_type) {
        ::operator delete(p);
    }
};
```

该分配器的重要特性是 `allocate()` 完全忽略了大小请求，并返回一个固定大小的块。

# 字符串分配器的性能

我在第 4 章示例 4-1 的 `remove_ctrl()` 版本中测试了字符串分配器。该函数对 `std::string` 的使用效率低下，创建了很多临时字符串。示例 13-12 是修改后的函数。

## 示例 13-12. 使用固定块字符串分配器的 `remove_ctrl()` 版本

```cpp
typedef std::basic_string<
    char,
    std::char_traits<char>,
    StatelessStringAllocator<char>> fixed_block_string;

fixed_block_string remove_ctrl_fixed_block(std::string s) {
    fixed_block_string result;
    for (size_t i = 0; i<s.length(); ++i) {
        if (s[i] >= 0x20)
            result = result + s[i];
    }
    return result;
}
```

移除 `memory_ctrl()` 的实验运行了 2693 毫秒。示例 13-12 中的改进版本在 1124 毫秒内完成了相同的测试，大约快 1.4 倍。这种性能提升是显著的，但正如我们在第 4 章中看到的，其他优化的效果更好。

编写自定义内存管理器或分配器可能是有效的，但它的收益少于完全消除对内存管理器调用的优化。

## 总结

- 寻找性能改进的地方可能比内存管理器更具成效。
- 在几个大型开源程序中，替换默认内存管理器带来的全程序性能提升从微乎其微到 30% 不等。
- 相同大小请求的内存管理器特别容易编写，且运行高效。
- 特定类实例的所有分配请求都请求相同字节数。
- `operator new()` 可以在类级别进行重写。
- 标准库容器类 `std::list`、`std::map`、`std::multimap`、`std::set` 和 `std::multiset` 都从许多相同的节点创建数据结构。
- 标准库容器接受一个 `Allocator` 参数，这允许与类特有的 `operator new()` 相同的自定义内存管理能力。
- 编写自定义内存管理器或分配器可能是有效的，但它的收益少于完全消除对内存管理器调用的优化。

# 索引

# 符号

- `#ifdef`, 169
- 标准库, 321
- 80/20 原则, 29
- 90/10 原则, 29
- `::` (全局范围作用符), 331
- `~` (波浪), 332

# A

- "A Toolbox of Strings Classes" (Panzer), 86
抽象类, 167
准确性, 41
获取语义, 289
待优化的活动
剖析, 205
识别, 204
地址, 15
高级配置与电源接口 (ACPI), 48
算法（均包含所有和搜索）
更改/替换, 206
高效算法, 96-98
高效排序算法, 98-100
优化的影响, 91
优化模式
批处理, 100, 102
缓存, 101, 103
双重检查, 101, 105
哈希, 101, 105
提示, 101, 105
惰性计算, 100, 102
优化预期路径, 101, 105
预计算, 100-102
专门化, 101, 104
迈更大的步子, 101, 104
其他成本, 96
并行化, 96
C++ 代码优化策略, 6-12
其时间成本, 92-96
用于优化搜索和排序的工具包。
96, 203-208
分配器
C++98 分配器, 347
重新分配的后果, 237
自定义标准库分配器, 343
动态变量, 324
固定块分配器, 352
最小 C++11 分配器, 346
减少重新分配, 127-128
选择, 87
用于的模板, 115
阿姆达 定律, 31, 323
摊销时间成本, 95
算术表达式（见表达式）
赋值运算符, 129
关联中心, 230
`<async>` 头文件, 296
异步函数调用, 293
异步任务, 295
`<atomic>` 头文件, 301
原子性, 289-304
特殊函数的生成, 141
存储周期, 109

# B

- 基准测量, 204
`BasicLockable` 锁, 299
批处理, 100, 102
大端计算机, 200
大-O 表示法, 93
二分查找, 97, 216-220
二叉树, 123
块区域, 338
Boost 库
`Boost` 图库 (BGL), 262
`Boost` 字符串算法, 84, 87
`Boost.Container` 库, 262
`Boost.Coroutine`, 320
`Boost.heap` 库, 262
`Boost.Intrusive` 库, 262
`Boost.lockfree` 库, 262
`Boost.Multithreaded` 库, 262
`Boost.Thread`, 320
`Boost.circular_buffer` 库, 261
标准线程池和队列, 310
缓冲区
容量, 237
环形, 124
创建大的, 121
使用输入缓冲区, 272
字符串优化和, 148
字符串实现, 69
C++ 并发工作组, 305
并发设施, 291-305
容器
关联容器, 230
收益, 229
优化重点, 229
优化实验, 231-236
序列容器, 230
无序关联容器, 231
通用用途, 187-190
用...优化, 226-228
其哲学, 188
共享内存支持, 280
C++ 字符串工具包 (StrTk), 84
C++ 表达式模板, 86
C++98 装饰器, 347
缓存内存
算法优化, 103
速度, 19
收益, 19
目标, 103
循环结束, 149
优化模式, 101
变体, 150

# C

C++ AMP 库, 321
C++ 代码
变量中的行为, 108-113
C 字符串键, 210
转换为 std::, 89
动态变量, 113-119
for 循环语法, 149
隐式函数调用, 155
优化策略, 6-12
简单自定义模型, 16
语句行为, 24-25
C++ 编译器
在 operator 版本中, 333
文档, 7
其中启用优化, 7
移动语义和, 140
其中预计算, 102
性能分析工具, 37-40
选择, 7-8, 82
（另见软件计时器）
闭式计算, 180
并发, 279-321
原子性, 289
收益, 280
已定义, 280
标准库中的设施, 291-305
提高同步效率, 314-320
在现代计算中, 279
交错执行, 285
支持库, 320-321
提供的机制, 280-285
优化挑战, 281
优化线程程序
挑战, 305
