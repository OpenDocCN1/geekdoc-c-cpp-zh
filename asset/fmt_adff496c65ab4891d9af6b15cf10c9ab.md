
## 2 影响：使用指定的分配器构造一个空列表。

## 3 复杂度：常数级。

- 4 `explicit list(size_type n, const Allocator = Allocator());`

  5 前提条件：`T` 是可插入的。

  6 影响：使用指定的分配器构造包含 `n` 个默认插入元素的列表。

  7 复杂度：线性级。

- 8 `list(size_type n, const T& value, const Allocator = Allocator());`

  9 前提条件：`T` 是可拷贝的。

  10 影响：使用指定的分配器构造包含 `n` 个 `value` 拷贝的列表。

  11 复杂度：线性级。

```cpp
template<class InputIterator>
list(InputIterator first, InputIterator last, const Allocator& alloc = Allocator());
```

影响：构造范围 `[first, last]` 内的列表。

复杂度：线性级，`distance(first, last)`。

## 22.3.10.3 容量

`[list.capacity]`

- 1 `void resize(size_type sz);`

  2 前提条件：`T` 是可默认插入的。

  3 影响：如果 `size() < sz`，则向序列追加 `sz - size()` 个默认插入元素。等同于

```cpp
list<T>::iterator it = begin();
advance(it, sz);
erase(it, end());
```

- 4 `void resize(size_type sz, const T& c);`

  5 前提条件：`T` 是可拷贝的。

  6 影响：如下所示：

  if (sz > size()) {

    insert(end(), sz-size(), c);

  } else if (sz < size()) {

    iterator i = begin();

    advance(i, sz);

    erase(i, end());

  }

  else {

    // 无操作

  }

```

## 22.3.10.4 修改器

`[list.modifiers]`

- 1 `iterator insert(const_iterator position, const T& x);`
  `iterator insert(const_iterator position, T&& x);`
  `iterator insert(const_iterator position, size_type n, const T& x);`

```cpp
template<class InputIterator>
iterator insert(const_iterator position, InputIterator first);
```
`iterator insert(const_iterator position, initializer_list<T>);`
`template<class Args...>`
`Args& element_front(Args&&... args);`
`template<class Args...>`
`Args& element_back(Args&&... args);`
`template<class Args...>`
`Args& element_place(const_iterator position, Args&&... args);`
`void push_front(const T& x);`
`void push_front(T&& x);`
`void push_back(const T& x);`

- 1 注意：不影响迭代器和引用的有效性。如果抛出异常，则没有影响。
  2 复杂度：向列表中插入单个元素需要常数时间，对 `T` 构造函数的调用次数与插入元素的数量线性相关，对 `T` 移动构造函数的调用次数正好等于元素数量。
```cpp
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);
void pop_front();
void pop_back();
clear() noexcept;
```

- 3 影响：仅使删除元素的迭代器和引用失效。
  4 抛出：无。
  5 复杂度：删除单个元素是常数级操作，调用一次 `T` 的析构函数。删除列表中的范围与范围的大小以及对 `T` 析构函数的调用次数线性相关。

## 22.3.10.5 操作

- 1 `list` 允许在列表中间快速插入和删除，专门为此提供了某些操作。在本子句中，模板参数 `BinaryPredicate` 的参数满足 25 中的相应要求。对于 `merge` 和 `sort`，定义和要求见 25.8。
  2 `list` 提供了三种操作，破坏性地将元素从一个列表移动到另一个。`splice` 操作的行为是未定义的。
```cpp
void splice(const_iterator position, list& x);
void splice(const_iterator position, list& x);
void address(x) != this is true.
```

- 3 前提条件：`all` 为真。
  4 影响：`x` 在 `position` 之前的内容变为空。指向移动元素的指针和引用将继续指向它们作为 `*this` 的成员。指向移动元素的迭代器将继续指向它们的元素，但它们现在作为指向 `*this` 的迭代器，而不是 `unto`。
  5 抛出：无。
  6 复杂度：常数级。
```cpp
void splice(const_iterator position, list& x, const_iterator i);
void splice(const_iterator position, list& x, const_iterator i);
```

- 7 前提条件：`i` 是有效的可解引用点
  8 影响：在 `list position` 之前插入 `i` 指向的元素并从 `x` 中移除元素。如果 `i == position` 或 `i == end()`，结果不变。继续作为 `*this` 的成员指向相同的元素。指向 `*i`（包括自身）的迭代器继续指向相同的元素，但现在作为指向 `*this` 的迭代器，而不是 `x` 中的。

抖动：无。
复杂度：常数级。

```cpp
void slice(const_iterator position, list& x, const_iterator first, const_iterator last);
void slice(const_iterator position, list& x, const_iterator first, const_iterator last);
```

前提条件：`[first, last)` 是 `x` 中的有效范围。`position` 不是 `[first, last)` 范围内的迭代器。
影响：在 `[first, last)` 范围之前插入 `position` 并从 `x` 中移除元素。移动元素的指针和引用现在指向这些元素作为 `*this` 的成员。指向 `x` 中移动元素的迭代器将继续指向它们，但它们是 `*this` 的迭代器，而不是 `x` 的。
抖动：无。
复杂度：如果 `address(x) == this` 为常数级；否则为线性级。

```cpp
size_type remove(const T& value);
template<class Predicate> size_type remove_if(Predicate pred);
```
影响：删除列表中所有由迭代器 `i` 指向的、满足条件的元素：`*i == pred(i) != false`。仅使删除元素的迭代器和引用失效。
返回：删除元素的数量。
抛出：除非抛出 `*i == this` 或 `pred(i) != false` 异常。
备注：稳定（16.4.6）。

```cpp
size_type unique();
template<class BinaryPredicate> size_type unique(BinaryPredicate binary_pred);
```
影响：删除范围 `[first, last)` 内每组连续相等元素中除第一个以外的所有元素，这些元素由迭代器 `i` 指向且 `i == *(i-1)`（无参数 `unique` 版本）或 `pred(*i, *(i-1))`（带谓词参数 `unique` 版本）。仅使删除元素的迭代器和引用失效。
返回：删除元素的数量。
抛出：除非抛出 `*i == *(i-1)` 或 `pred(*i, *(i-1))` 异常。
复杂度：如果范围 `[first, last)` 不为空，则执行 `(last - first) - 1` 次相应的成对应用，否则不应用谓词。

备注：稳定 (16.4.6.8)。如果 `addressof(x) != this`，则合并后范围 `[x.begin(), x.end())` 为空。此操作不拷贝元素。

复杂度：如果 `addressof(x) != this`，执行 `max size() + x.size() - 1` 次 `comp` 调用；否则不执行 `comp` 调用。如果比较时抛出异常，则没有影响。

```cpp
void reverse() noexcept;
```

影响：反转列表中元素的顺序。不影响迭代器和引用的有效性。

复杂度：线性时间。

```cpp
template<class Compare> void sort(Compare comp);
```

影响：根据运算符或 `Compare` 函数对象对列表进行排序。如果抛出异常，则 `*this` 中元素的顺序是不指定的。不影响迭代器和引用的有效性。

复杂度：稳定 (16.4.6.8)。`N log N` 次比较，其中 `N == size()`。

## 22.3.10. 擦除 (Erasure)

```cpp
template<class T, class Allocator, class U>
typename listT<T, Allocator>::size_type
erase(listT<T, Allocator>& c, const U& value = {});
```

影响：等价于 `erase_if(c, [value](auto elem) { return elem == value; });`

```cpp
template<class T, class Allocator, class Predicate>
typename listT<T, Allocator>::size_type
erase(listT<T, Allocator>& c, Predicate pred);
```

影响：等价于 `return c.remove_if(pred);`

## 22.3.11 Class vector 模板

### 22.3.11.1 概述

- `vector` 是一种支持在末尾进行（摊销）时间插入和删除操作的容器；在中间插入和删除需要线性时间。存储管理由自动处理，在需要时可能会重新分配。异常均为与 `std::allocator` 相关的 `std::bad_alloc`。

`vector` 满足序列容器和可逆序列容器（在 22.2 中的两个表中给出）的所有要求，包括所有感知分配器的容器（表 76），并且对于除 `bool` 以外的元素类型，提供了连续容器的 `push_front`、`pop_front` 和 `emplace_front` 成员函数（这些已提供，22.2.1）。此处提供了未未在这些表中描述的操作，或存在语义信息的操作的描述。

`iterator` 和 `const_iterator` 类型必须满足迭代器要求 (23.3.1)。

```cpp
namespace std {
template<class T, class Allocator = allocator<T>>
class vector {
public:
using value_type = T;
using allocator_type = Allocator;
using pointer = T*;
using reference = T&;
using const_pointer = const T*;
using const_reference = const T&;
using size_type = std::size_t; // 22.2
using difference_type = std::ptrdiff_t; // 22.2
using implementation_defined = std::allocator_traits<Allocator>::value_type; // 22.2
using iterator = ...;
using const_iterator = ...;
using reverse_iterator = std::reverse_iterator<iterator>;
using const_reverse_iterator = std::reverse_iterator<const_iterator>;
```

```cpp
// 22.3.11.2, constructor(Allocator())
const vector() noexcept(const Allocator&) : vector(Allocator()) {}
const vector explicit(const Allocator&) noexcept;
const vector explicit(size_type n, const Allocator& = Allocator());
const vector(size_type n, const T& v, const Allocator& = Allocator());
template<class InputIterator>
const vector(InputIterator first, InputIterator last, const Allocator& = Allocator());
const vector(const vector& x);
const vector(const vector& x, const Allocator& = Allocator());
const vector(initializer_list<T>, const Allocator& = Allocator());
const vector& operator=(const vector& x);
const vector& operator=(const vector& x) noexcept
allocator_traits<Allocator>::is_propagate_on_container_move_assign == value;
const vector& operator=(initializer_list<T>, const Allocator& = Allocator());
template<class InputIterator>
const void assign(InputIterator first, InputIterator last);
const void assign(size_type n, const T& v);
const void assign(initializer_list<T>);
const Allocator& get_allocator() const noexcept;
```

```cpp
// iterator
iterator begin() noexcept;
const const_iterator begin() const noexcept;
iterator end() noexcept;
const const_iterator end() const noexcept;
reverse_iterator begin() const noexcept;
const const_reverse_iterator begin() const noexcept;
reverse_iterator end() const noexcept;
const const_reverse_iterator end() const noexcept;
```

```cpp
const_iterator cbegin() const noexcept;
const const_iterator cend() const noexcept;
reverse_iterator crbegin() const noexcept;
const const_reverse_iterator crbegin() const noexcept;
reverse_iterator crest() const noexcept;
```

```cpp
// 22.3.11.3, capacity
[[nodiscard]] bool empty() const noexcept;
const size_type size() const noexcept;
const size_type max_size() const noexcept;
const size_type capacity() const noexcept;
void resize(size_type n);
void resize(size_type n, const T& c);
void reserve(size_type n);
void shrink_to_fit();
```

```cpp
// element access
const reference operator[](size_type n) const;
reference& operator[](size_type n);
```
