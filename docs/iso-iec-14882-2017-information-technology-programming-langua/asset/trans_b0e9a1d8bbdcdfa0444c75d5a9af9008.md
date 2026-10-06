

# ISO/IEC 14882:2017(E)

```cpp
template <class T, class Allocator>
void swap(deq<T, Allocator>& x, deq<T, Allocator>& y)
noexcept(noexcept(x.swap(y)));
```

```cpp
namespace pr {
    template <class T>
    using deque = std::deque<T, polymorphic_allocator<T>>
}
```

## 26.3.4 头 <forward_list> 摘要

```cpp
#include <initializer_list>

namespace std {
    // 36.3.9.
    template <class T, Allocator = allocator<T>> class forward_list {
    template <class T, Allocator>
    forward_list(const forward_list<T, Allocator>& x, const Allocator& x = Allocator());
    template <class T, Allocator>
    bool operator==(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator!=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    void swap(forward_list<T, Allocator>& x, forward_list<T, Allocator>& y)
    noexcept(noexcept(x.swap(y)));
```

```cpp
namespace pr {
    template <class T>
    using forward_list = std::forward_list<T, polymorphic_allocator<T>>
}
```

## 26.3.5 头 <initializer_list> 摘要

```cpp
#include <initializer_list>

namespace std {
    // 36.3.10.
    template <class T, Allocator = allocator<T>> class list {
    template <class T, Allocator>
    list(const list<T, Allocator>& x, const Allocator& x = Allocator());
    template <class T, Allocator>
    bool operator==(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator!=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator!=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    list<T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, class Allocator>
    void swap(list<T, Allocator>& x, list<T, Allocator>& y) 
    noexcept(noexcept(x.swap(y)));
```

```cpp
namespace pmr {
    template <class T>
    using list = std::list<T, polymorphic_allocator<T>>;
}
```

## 26.3.6 头 <vector> 摘要

```cpp
#include <initializer_list>

namespace std {
    // 26.3.11, class vector
    template <class T, class Allocator = allocator<T>> class vector;
    template <class T, class Allocator>
    bool operator==(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template <class T, class Allocator>
    bool operator>(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template <class T, class Allocator>
    bool operator<=(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template <class T, class Allocator>
    bool operator>=(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template <class T, class Allocator>
    bool operator!=(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template <class T, class Allocator>
    bool operator<=(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template <class T, class Allocator>
    void swap(vector<T, Allocator>& x, vector<T, Allocator>& y)
    noexcept(noexcept(x.swap(y)));

    // 26.3.19, class vector
    template <class Allocator> class vector<bool, Allocator>;

    // hash support
    template <class T> struct hash;
    template <class Allocator> struct hash<bool, Allocator>;
}
```

## 26.3.7 类 array

### 26.3.7.1 类概述

`<array>` 定义用于存储固定大小序列的类。array 是一个连续容器 (26.2.1)。`array<T, N>` 存储 N 个 T 元素，使得 `size() == N` 是不变的。array 是一个聚合体 (11.6.1)，可以用转换为 T 的元素初始化。array 满足容器和可逆容器 (26.2) 的所有要求，只是默认对象为空且 swap 具有常数复杂度。array 满足序列容器 (26.2.3) 的某些要求。此处提供了在表中描述的 array 操作以及额外的语义信息。

```cpp
namespace std {
template<class T, size_t N>
struct array {
    // 类型
    using value_type = T;
    using pointer = T*;
    using const_pointer = const T*;
    using reference = T&;
    using const_reference = const T&;
    using size_type = size_t;
    using difference_type = ptrdiff_t;
    using implementation_defined; // 见 26.2
    using const_iterator = implementation-defined; // 见 26.2
    using reverse_iterator = std::reverse_iterator<iterator>;
    using const_reverse_iterator = std::reverse_iterator<const_iterator>;

// // 聚合类型的显式构造/拷贝/析构
```cpp
void fill(array&) noexcept(is_nothrow_swappable<T>);
void swap(array&&) noexcept;
```

// 迭代器:
```cpp
const_iterator begin() noexcept;
const_iterator begin() const noexcept;
const_iterator end() noexcept;
const_iterator end() const noexcept;

reverse_iterator rbegin() noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() noexcept;
const_reverse_iterator rend() const noexcept;
```
```cpp
const_iterator cbegin() noexcept;
const_iterator cend() const noexcept;
const_reverse_iterator cbegin() const noexcept;
const_reverse_iterator crend() const noexcept;
```

// 容量:
```cpp
bool empty() noexcept;
size_type size(size_t n) const noexcept;
size_type max(size_t n) const noexcept;
```

// 元素访问:
```cpp
const_reference operator[](size_type n);
const_reference operator[](size_type n) const;
const_reference at(size_type n);
const_reference at(size_type n) const;
const_reference front();
const_reference front() const;
const_reference back();
```

```cpp
constexpr const_reference back() const {
    constexpr T *data() noexcept;
    constexpr T *data() const noexcept;
};
```

## 26.3.7.2 array 构造函数、拷贝和赋值

必须满足聚合体 (11.6.1) 的条件。类可能要求成员函数 (15.1、15.4 和 15.8) 符合 26.2 中的容器要求。除了容器表中指定的要求外，array 的隐式构造函数和移动赋值运算符要求 T 分别是可移动构造或可移动的。

```cpp
template<class T, class... U>
array(T, U...) -> array<T, 1 + sizeof...(U));
```

- 2: 要求：(is_same_v<T> && ... ) 为真。否则该 array 是格式错误的。

## 26.3.7.3 array 特化算法

```cpp
template<class T, size_t N>
void swap(T& x, T& y) noexcept(noexcept(x.swap(y)));
```

- 1: 备注：除非 N == 0 且 is_swappable<T> 为真，否则此函数不参与重载解析。
- 2: 影响：等于 x.swap(y)。
- 3: 复杂度：相对于 N 线性。

## 26.3.7.4 array::size

```cpp
template<class T, size_t N> constexpr size_type array<T, N>::size() const noexcept;
```

- 1: 返回：N。

## 26.3.7.5 array::data

```cpp
constexpr T *data() noexcept;
constexpr T *data() const noexcept;
```

- 1: 返回：一个指针，使得 data() == addressof(front()), data(), data() + size() 是一个有效范围。

## 26.3.7.6 array::fill

```cpp
void fill(const T& u, N n);
```

- 1: 影响：等同 fill_n(begin(), N, u)。

## 26.3.7.7 array::swap

```cpp
void swap(array& x, array& y) noexcept(no_othrow_swappable<array>);
```

- 1: 影响：等同于 swap_ranges(begin(), end(), y.begin())。
- 2: 注意：与其他容器的 swap 函数不同，array::swap 消耗线性时间，可能会通过异常退出，并且不会让迭代器关联到另一个容器。-- 备注结束

