
`bool operator+=(const list<T, Allocator>& x, const list<T, Allocator>& y);`

`template <class T, class Allocator>`

`bool operator<(const list<T, Allocator>& x, const list<T, Allocator>& y);`

`template <class T, class Allocator>`

`bool operator!=(const list<T, Allocator>& x, const list<T, Allocator>& y);`

`template <class T, class Allocator>`

`bool operator==(const list<T, Allocator>& x, const list<T, Allocator>& y);`

`template <class T, class Allocator>`

`bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);`

`template <class T, class Allocator>`

`bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);`

```
// 特殊化算法：
template <class T, class Allocator>
void swap(list<T, Allocator>& x, list<T, Allocator>& y)
noexcept(swap(y));
```

# 23.3.5.5 列表操作

1 由于列表允许在中间进行插入和删除，因此某些操作是为它们专门定义的。

2 列表提供了三种 `splice` 操作，可以将元素从一个列表移动到另一个列表。如果 `get_allocator() != x.get_allocator()`，则 `splice` 操作是未定义的。

```cpp
void splice(const_iterator position, list& x);
void splice(const_iterator position, list&& x);
```

3 要求：`x != this`。

4 影响：将 `x` 插入该位置且 `x` 变为空。移动元素的指针和引用现在指向 `*this` 的成员。指向移动元素的迭代器将继续指向这些元素，但它们的行为是 `*this` 的迭代器，而不是 `x` 的迭代器。

5 如 17.6.3.5 所述，本节的要求适用于分配器相等的列表。

```cpp
void splice(const_iterator position, list& x, const_iterator i);
void splice(const_iterator position, list& x, const_iterator i);
void splice(const_iterator position, list& x, const_iterator first, const_iterator iterator);
```

```cpp
void merge(list& x);
void merge(list& x);
template <class Compare> void merge(list& x, Compare comp);
template <class Compare> void merge(list& x, Compare comp);
```

22 要求 `comp` 定义了一个严格排序 (25.4)，且两个参数列表都应按照此排序排序。

23 影响：如果 `(kx == this)` 则不执行任何操作；两个已排序范围 `[begin(), end())` 和 `[x.begin(), x.end())` 结果产生一个范围，其中的元素根据 `comp` 定义的排序按降序排列；也就是说，对于每一个迭代器 `i`，除第一个之外，条件 `*(i-1)` 将为假。指向 `x` 中被移动元素的指针和引用现在将这些元素引用为 `*this*` 的成员。指向被移动元素的迭代器继续指向这些元素，但行为上表现为指向 `*this*` 的迭代器，而不是 `x`。

24 备注：稳定的 (17.6.7)。如果 `(kx != this)`，则合并后范围 `[x.begin(), x.end())` 为空。完全没有元素被复制。如果 `this->get_allocator() != x.get_allocator()`，行为是未定义的。

25 复杂度：如果 `(kx != this)`，最多执行 `size() + x.size() - 1` 次 `comp`；否则，不执行任何 `comp` 的调用。如果抛出除比较以外的异常，则没有影响。

```cpp
void reverse() noexcept;
```

26 影响：反转列表中元素的顺序。不影响迭代器和引用的有效性。

27 复杂度：线性时间。

```cpp
void sort();
template <class Compare> void sort(Compare comp);
```

28 要求 `operator<`（对于第一个版本）或 `comp`（对于第二个版本）应定义一个严格排序 (25.4)。

29 影响：根据 `operator<` 或 `Compare` 函数对象排序列表。不影响迭代器和引用的有效性。

30 备注：稳定的 (17.6.5.7)。

31 复杂度：大约 `log(N)` 次比较，其中 `N == size()`。

## 23.3.5.6 list 特殊化算法

```cpp
template <class T, class Allocator>
void swap(list<T, Allocator>& x, list<T, Allocator>& y)
noexcept(noexcept(x.swap(y)));
```

影响：
`x.swap(y);`

## 23.3.6 类模板 vector

### 23.3.6.1 类模板 vector 概述

`vector` 是一种序列容器，支持在末尾进行（摊销）常数时间的插入和删除操作；在中间进行线性时间的插入和删除。存储管理自动处理，尽管可以提供提示来提高效率。

`Vector` 满足容器和可逆容器的所有要求（在两个表格 (23.2) 中给出）、序列容器（包括大部分可选序列容器要求 (23.2.3)、分配器感知容器的要求（表 99），以及对于除 `bool` 以外的元素，满足连续容器的要求 (23.2.1)。异常是 `push_front`、`pop_front` 和 `emplace` 成员函数，这些函数未被提供。此处仅对未在这些表格中描述的 `vector` 操作，或对默认值为语义信息的操作提供描述。

```cpp
namespace std {
template <class T, class Allocator = allocator<T>>
class vector {
public:
    //
    typedef value_type type_k;
    typedef const value_type const_type;
    typedef implementation_defined implementation_defined;
    typedef implementation_defined implementation_defined;
    typedef implementation_defined implementation_defined;
    T value;
    Allocator allocator;
    typedef allocator_traits<Allocator>::pointer pointer;
    typedef allocator_traits<Allocator>::const_pointer const_pointer;
    std::reverse_iterator<Iterator> reverse_iterator;
    std::reverse_iterator<const Iterator> reverse_iterator;
    // 23.3.6. construct(copy/dest)
    vector(const Allocator& alloc = Allocator()) noexcept {}
    explicit vector(size_type n, const Allocator& alloc = Allocator()) noexcept;
    vector(size_type n, const T& value, const Allocator& alloc = Allocator()) noexcept;
    template <class InputIterator>
    vector(InputIterator first, InputIterator last,
           const Allocator& alloc = Allocator()) noexcept;
    vector(const T& x) noexcept;
    vector(T&& x) noexcept;
    vector(const T& x, const Allocator& alloc) noexcept;
    vector(std::initializer_list<T> list, const Allocator& alloc = Allocator()) noexcept;
    ~vector() noexcept;
    vector& operator=(const T& x);
    vector& operator=(T&& x) noexcept
        (allocator_traits<Allocator>::propagate_on_container_move_assignment() == value ||
        allocator_traits<Allocator>::is_equal);
    vector& operator=(const std::initializer_list<T>& list);
    template <class InputIterator>
    void assign(InputIterator first, InputIterator last);
    void assign(size_type n, const T& u);
    void assign(std::initializer_list<T> list);
    allocator_type get_allocator() const noexcept;
    // iterators:
    iterator begin() noexcept;
    const_iterator begin() const;
    iterator end() noexcept;
    const_iterator end() const;
    reverse_iterator begin() noexcept;
    reverse_iterator begin() const;
    reverse_iterator end() noexcept;
    reverse_iterator end() const;
    const_iterator cbegin() noexcept;
    const_iterator cbegin() const;
    const_iterator const() noexcept;
    const_iterator const() const;
    reverse_iterator crbegin() noexcept;
    reverse_iterator crbegin() const;
    reverse_iterator cend() noexcept;
    reverse_iterator cend() const;
    const_iterator cbegin() noexcept;
    const_iterator cbegin() const;
    const_iterator const() noexcept;
    const_iterator const() const;
    reverse_iterator crbegin() noexcept;
    reverse_iterator crbegin() const;
    reverse_iterator cend() noexcept;
    reverse_iterator cend() const;
    const_iterator cbegin() noexcept;
    const_iterator cbegin() const;
    const_iterator const() noexcept;
    const_iterator const() const;
    reverse_iterator crbegin() noexcept;
    reverse_iterator crbegin() const;
    reverse_iterator cend() noexcept;
    reverse_iterator cend() const;
    const_iterator cbegin() noexcept;
    const_iterator cbegin() const;
    const_iterator const() noexcept;
    const_iterator const() const;
    reverse_iterator crbegin() noexcept;
    reverse_iterator crbegin() const;
    reverse_iterator cend() noexcept;
    reverse_iterator cend() const;
    const_iterator cbegin() noexcept;
    const_iterator cbegin() const;
    const_iterator const() noexcept;
    const_iterator const() const;
    reverse_iterator crbegin() noexcept;
    reverse_iterator crbegin() const;
    reverse_iterator cend() noexcept;
    reverse_iterator cend() const;
    type_type size() const noexcept;
    type_type capacity() const;
    void resize(size_type n);
    void resize(size_type n, const T& v);
    void reserve(size_type n);
    bool empty() const noexcept;
    T& operator[](size_type n);
    const T& operator[](size_type n) const;
    T& at(size_type n);
    const T& at(size_type n) const;
    T& front() noexcept;
    const T& front() const noexcept;
    T& back() noexcept;
    const T& back() const noexcept;
    T* data() noexcept;
    const T* data() const noexcept;
    void push_back(const T& x);
    void push_back(T&& x);
    template <class... Args>
    void emplace_back(Args&&... args);
    void insert(size_type pos, const T& x);
    void insert(size_type pos, T&& x);
    template <class... Args>
    void emplace(size_type pos, Args&&... args);
    iterator insert(const iterator& pos, const T& x);
    iterator insert(const iterator& pos, T&& x);
    template <class... Args>
    iterator emplace(const iterator& pos, Args&&... args);
```
