
`template<class Iterator>`
  `using value_type = iterator_traits<Iterator>::value_type;`   // 仅表达式

### 22.3.2 头文件 `<compare>` 概要

```cpp
#include <compare>
#include <initializer_list>
// sec 17.11.1
```

```cpp
// sec 17.10.13
namespace std {
```

```cpp
// sec 17.11.1
template<class T, N>
  bool operator=(const T& a, const T& b);
```

```cpp
// sec 17.11.1
template<class T, N>
  auto _three_way_result<T> operator==(const T& a, const T& b);
```

```cpp
// sec 17.10.13
template<class T, N>
  void swap(T& a, T& b);
```

```cpp
// sec 17.10.13
template<class T, N>
  constexpr array_cv<T> to_array(const T a);
```

```cpp
// sec 17.11.1
template<class T, N>
  constexpr array_cv<T> to_array(T a);
```

## 22.3.5 Header `<list>` 概览

```cpp
#include <compare>                               //  17.11.1
#include <initializer_list>                               //  17.10.2
```

```cpp
namespace std {
    // 22.3.10, 类模板列表 list
    template<class T, class Allocator = allocator<T>> class list;
    template<class T, class Allocator>
        bool operator=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template<class T, class Allocator>
        std::three_way_comparison_result operator<=>(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template<class T, class Allocator>
        void swap(list<T, Allocator>& x, list<T, Allocator>& y)
        noexcept(x.swap(y));
    template<class T, class Allocator, class U>
        typename list<T, Allocator>::size_type
        erase(list<T, Allocator>& c, const U& value);
    template<class T, class Allocator, class Predicate>
        typename list<T, Allocator>::size_type
        erase_if(list<T, Allocator>& c, Predicate pred);
namespace pmr {
    template<class T>
        using list = std::list<T, polymorphic_allocator<T>>;
}
}
```

## 22.3.6 Header `<vector>` 概览

```cpp
#include <compare>                               //  17.11.1
#include <initializer_list>                               // 17.10.2
```

```cpp
namespace std {
    // 22.3.11, 类模板 vector
    template<class T, class Allocator = allocator<T>> class vector;
    template<class T, class Allocator>
        const bool operator=(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template<class T, class Allocator>
        std::three_way_comparison_result operator<=>(const vector<T, Allocator>& x, const vector<T, Allocator>& y);
    template<class T, class Allocator>
        void swap(vector<T, Allocator>& x, vector<T, Allocator>& y)
        noexcept(x.swap(y));
    template<class T, class Allocator, class U>
        typename vector<T, Allocator>::size_type
        erase(vector<T, Allocator>& c, const U& value);
    template<class T, class Allocator, class Predicate>
        typename vector<T, Allocator>::size_type
        erase_if(vector<T, Allocator>& c, Predicate pred);
    // 22.3.12, 类 vector<bool>
    template<class Allocator> class vector<bool, Allocator>;
    // 哈希支持
    template<class T> struct hash;
    template<class Allocator> struct hash<vector<bool, Allocator>>;
```

```cpp
namespace pmr {
    template<class T>
        using vector = std::vector<T, polymorphic_allocator<T>>;
}
}
```

## 22.3 类模板 array

### 22.3.1 概述

`array` 头文件定义了一个用于固定大小对象序列的类模板。`array` 是连续容器 `22.2.1`。`array<T, N>` 实例存储类型为 `T` 的元素，使得 `size() == N` 是不变的。一个 `9.4.2` 数组可以用最多 `N` 个元素初始化，这些元素的类型可以转换为 `T`。`array` 满足容器和可反转容器 `22.2` 的所有要求，但默认构造的 `array` 是空的且 `swap` 不具有常数复杂度。这里提供了关于序列容器 `22.2.3` 的部分描述，用于未在表格中描述的 `array` 操作。当且仅当每对元素 `a1` 和 `a2` 都相等时，`array<T, N>` 是结构等价 `3.6`。

```cpp
namespace std {
    template<class T, size_t N>
    struct array {
        // ...
        using value = T;
        using pointer = T*;
        using const_pointer = T*;
        using reference = T&;
        using const_reference = T&;
        using size_type = size_t;
        using difference_type = std::ptrdiff_t;
        using iterator = implementation_defined; // 见 22.2
        using const_iterator = implementation_defined; // 见 22.2
        using reverse_iterator = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const iterator>;
        // 默认构造/拷贝/析构
        array() noexcept(is_swapable<T>);
        // 迭代器
        iterator begin() noexcept;
        const_iterator begin() const;
        iterator end() noexcept;
        const_iterator end() const;
        reverse_iterator rbegin() noexcept;
        const_reverse_iterator rbegin() const;
        reverse_iterator rend() noexcept;
        const_reverse_iterator rend() const;
        const_iterator cbegin() noexcept;
        const_iterator cend() const;
        const_reverse_iterator crbegin() const noexcept;
        const_reverse_iterator cre() const noexcept;
        // 容量
        [[nodiscard]] constexpr empty() const noexcept;
        constexpr size_type size() const noexcept;
        constexpr size_type max_size() const noexcept;
        // 元素访问
        constexpr reference operator[](size_type n);
        constexpr const_reference operator[](size_type n) const;
        constexpr const_reference at(size_type n);
        constexpr const_reference at(size_type n) const;
        constexpr reference front();
        constexpr const_reference front() const;
        constexpr reference back();
        constexpr const_reference back() const;
        constexpr T* data() const noexcept;
        constexpr const T* data() const noexcept;
    };
template<class T, class... U>
array(T, U...) -> array<T, 1 + sizeof...(U)>;
```

### 22.3.7.2 构造、拷贝与赋值

必须满足聚合 `9.4.2` 的条件。类 `array` 依赖隐式声明的成员函数 `11.4.5.2, 11.4.5.7, 11.4.5.3` 来符合 `22.2` 中的容器要求。除了容器要求外，`array` 的隐式移动构造函数和移动赋值运算符分别要求 `C++1MoveConstructible` 和 `C++1Assignable`。

```cpp
template<class T, class... U>
array(T, U...) -> array<T, 1 + sizeof...(U)>;
```

- 2 强制：`is_same_v<T, U> && ...`

### 22.3.7.3 成员函数

```cpp
constexpr size_type size() const noexcept
```

- 1 返回：`N`。

```cpp
constexpr T* data() const noexcept;
constexpr const T* data() const noexcept;
```

- 2 返回：一个指针，使得 `data(), data() + size()` 是有效范围。对于非空 `array`，`data() == offset(front())`。

```cpp
constexpr void fill(const T& u)
```

- 3 效果：等同于 `fill(begin(), end(), u)`。

```cpp
constexpr void swap(array& x, array& y) noexcept(is_swapable_v<T>);
```

- 4 效果：等同于 `swap_ranges(begin(), end(), y.begin())`。`array::swap` 线性时间，可以通过异常退出，且不使用迭代器与另一个容器通信。
- 5 [注：与其它容器的 `swap` 函数不同，`array::swap` 线性时间，可以通过异常退出，且不使用迭代器与另一个容器通信。]

### 22.3.7.4 特化算法

```cpp
template<class T, size_t N>
void swap(array<T, N>& x, array<T, N>& y) noexcept(is_swapable_v<T>);
```

- 1 约束：`N > 0`。
- 2 效果：相对于 `N` 线性。
- 3 复杂度：`O(N)`。

### 22.3.7.5 零大小数组

1 如果 `N == 0`，`data()` 是未定义的。
2. 在 `N == 0` 的情况下，`begin()` 和 `end()` 返回相同。
3. 调用 `front()` 或 `back()` 的效果是未定义的。
4. 成员函数 `swap()` 应当具有不抛异常规范。

### 22.3.7.6 Array 函数

```cpp
template<class T, size_t N>
const array<remove_cv<T>, N>& array(T const)[N]);
```

- 1 强制：`is_copy_v<T>` 为真。
- 2 前提：`T` 满足 `C++1Copyable` 要求。
- 3 返回：`{ a[0], ..., a[N-1] }`。

```cpp
template<class T, size_t N>
const array<remove_cv<T>, N>& array(T&&)[N]);
```

- 4 强制：`is_moveable_v<T>` 为真。
- 5 前提：`T` 满足 `C++1Moveable` 要求。
- 6 返回：`{ std::move(a[0]), ..., std::move(a[N-1]) }`。

### 22.3.7.7 Tuple 接口

```cpp
template<class T, size_t N>
struct tuple<array<T, N>> : integral_constant<size_t, N> {
```

```cpp
template<class I, class T, size_t N>
struct tuple_element<I, array<T, N>> {
  using type = T;
};
```

- 1 强制：`I < N` 为真。

```cpp
template<size_t I, class T, size_t N>
const T& get(array<T, N>& a) noexcept;
template<size_t I, class T, size_t N>
const T&& get(array<T, N>&& a) noexcept;
template<size_t I, class T, size_t N>
const T& get(const array<T, N>& a) noexcept;
template<size_t I, class T, size_t N>
const T&& get(const array<T, N>&& a) noexcept;
```

- 2 返回：`a` 中第 `<I>` 个元素的引用，索引从 0 开始。

public:
// types
  using value_type = T;
  using allocator_type = Allocator;
