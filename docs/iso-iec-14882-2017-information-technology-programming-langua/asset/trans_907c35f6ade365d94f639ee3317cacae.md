

# ISO/IEC 14882:2017(E)

public:

```cpp
using size_type      = size_t;
using difference_type = ptrdiff_t;
using pointer         = T*;
using const_pointer   = const T*;
using reference       = T;
using const_reference = const T;
template <class U> struct bind (using other = allocator<U>);

T* address(const T& x) const noexcept;
const T* address(const T& x) const noexcept;

T* allocate(size_t n, const void* hint);

template<class U, class... Args>
void construct(U* p, Args&&... args);
template<class U>
void destroy(U* p);

size_t max_size() const noexcept;
}
```

T* address(const T& x) const noexcept;
const T* address(const T& x) const noexcept;

- 2 返回: address(x)。

- 3 T* allocate(size_t n, const void* hint);

- 4 返回: 返回一个大小为 n * sizeof(T) 的存储数组的初始元素，该数组对类型为 T 的对象适当对齐。是否支持过度对齐类型（over-aligned types）或如何获取由实现定义 (6.11)。

- 5 备注: 存储通过调用 ::operator new(std::size_t) (21.6.2) 获取，但未指定何时以及如何调用此函数。

- 6 抛出: 如果无法获取存储，则抛出 bad_alloc。

```cpp
template <class U, class... Args>
void construct(U* p, Args&&... args);

影响: 相当于：new((void*)p) U(std::forward<Args>(args)...);

template <class U>
void destroy(U* p);

影响: 相当于：--U(p)。
```

- 7 size_t max_size() const noexcept;

- 8 返回: allocate(N, O) 可能会成功的最大值 N。

# D.10 原始存储迭代器

[depr.storage.iterator] 头文件 <memory> 包含以下新增内容：

```cpp
namespace std {
template <class OutputIterator, class T>
class raw_storage_iterator {
public:
```

```cpp
using iterator_category = output_iterator_tag;
using value_type = void;
using difference_type = void;
using pointer = void;
using reference = void;
```

```cpp
explicit raw_storage_iterator(OutputIterator x);
raw_storage_iterator& operator();
raw_storage_iterator& operator=(const T& element);
raw_storage_iterator& operator=(T&& element);
raw_storage_iterator& operator++();
raw_storage_iterator operator++(int);
base() const;
}
```

提供 raw_storage_iterator 是为了让算法能够将其结果存储在未初始内存中。模板参数 OutputIterator 要求其 operator* 返回一个定义了 operator* 且返回 T 类型指针针的对象，并且要求满足输出迭代器的要求 [27.2.4]。

```cpp
explicit raw_storage_iterator(OutputIterator x);
```

影响: 初始化迭代器使其指向与 x 指向的相同的值。

```cpp
raw_storage_iterator& operator() const;
```

```cpp
raw_storage_iterator& operator=(const T& element);
```

要求: T 应当是可拷贝构造（CopyConstructible）。

```cpp
raw_storage_iterator& operator=(T&& element);
```

影响: 在迭代器指向的位置从 element 构造一个值。

返回: 迭代器的引用。

```cpp
raw_storage_iterator& operator++() const;
```

要求: T 应当是可移动构造（MoveConstructible）。

影响: 在迭代器指向的位置从 std::move(element) 构造一个值。

返回: 迭代器的引用。

```cpp
raw_storage_iterator operator++(int);
```

影响: 前置递：推进迭代器并返回更新后的迭代器的引用。

影响: 后置递：推进迭代器并返回迭代器的旧值。

```cpp
OutputIterator base() const;
```

返回: 一个类型为 OutputIterator 的迭代器，其指向与 *this 指向的相同的值。

# D.11 临时缓冲区 [depr.temporary.buffer]

头文件 <memory> 包含以下新增内容：

```cpp
namespace std {
  template <class T >
```

```cpp
pair<T*, ptrdiff_t> get_temporary_buffer(ptrdiff_t n) noexcept;
template <class T>
void return_temporary_buffer(T* p);
}
```

template<class T>
pair<T*, ptrdiff_t> get_temporary_buffer(ptrdiff_t n) noexcept;

- 影响: 返回一个指向初始化器的指针，对于非负整数 N，返回 N 个相邻类型 T 对象的连续存储。是否支持过度对齐对象由实现定义 (6.11)。

- 备注: 使用正数 n 调用 get_temporary_buffer 是一个返回 n 个类型 T 对象的存储的非绑定性请求。在这种情况下，允许实现返回非负整数 N 个对象的存储（包括 N = 0）。[注意：返回结果对 n 对象的返回是非绑定的，以允许针对实现特定的管理优化留出余地，并可能被忽略]。

- 返回: 如果 n < 0 或无法获取空指针，则返回一个对 P，其中 first 为空指针，second 指向未初始化存储的地址，second 指其容量 N（单位为 sizeof(T)）。

```cpp
template <class T> void return_temporary_buffer(T* p);
```

- 影响: 释放 p 返回的存储。

- 要求: p 是之前调用 get_temporary_buffer 返回的指针值，且未被中间的 return_temporary_buffer(T) 调用失效。

- 抛出: 无。

# D.12 特性性 [depr.meta.types]

头文件 <traits> 包含以下新增：

```cpp
namespace std {
template<class T> constexpr is_type_v = is_type<T>::value;
```

# D.13 废弃迭代器原语 [depr.iterator.primitives]

### D.13.1 基础迭代器 [depr.iterator.basic]

头文件 <iterator> 包含以下新增内容：

```cpp
namespace std {
template<class Category, class T, class Distance = ptrdiff_t,
class Pointer = T*, class Reference = T*>
struct iterator {
    using iterator_category = Category;
    using value_type = T;
    using difference_type = Distance;
    using pointer = Pointer;
    using reference = Reference;
};
```

- 新迭代器可以作为基类，以简化新迭代器所需类型的定义。
- [注意：如果新迭代器是基类模板，那么这些别名在迭代器类的定义内部不可见，仅对该类的调用者可见。]
- [示例：如果一个 C++ 程序想要为包含 double 的数据结构定义双向迭代器，并且在实现的大型内存上工作，可以这样做：

```cpp
class MyIterator : public iterator<bidirectional_iterator_tag, double, long, T*> {
    // 实现 ++ 等代码
};
```

