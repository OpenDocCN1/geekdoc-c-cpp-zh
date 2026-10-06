

# ISO/IEC 14882:2017(E)

## 26.3.10.6 特殊化算法 [list.special]

```cpp
template <class T, class Allocator>
void swap(list<T, Allocator>& x, list<T, Allocator>& y)
noexcept(noexcept(x.swap(y)));
Effects: 相当于通过 x.swap(y) 执行；
```

## 26.3.11 类模板 vector [vector.overview]

### 26.3.11.1 类模板 vector 概述

- 1 一个 vector 是一种容器，支持在末尾处进行（摊销的）常数时间插入和删除操作；在中间的插入和删除为线性时间。存储管理由自动处理，尽管可以提供提示来提高效率。
- 2 一个 vector 满足容器的所有要求以及可逆容器的要求（在 26.2 的表格中给出）、序列容器的要求（包括大多数优化序列容器的要求 (26.2.3)）、分配器感知容器的要求（表 80），并且对于除 bool 以外的元素类型，满足连续容器（26.2.1）。push_front 和 pop_front 是成员函数，但未提供。此处仅对未在这些表格中描述的 vector 操作，或对具有额外语义信息的操作提供描述。

```cpp
namespace std {
template <class T, class Allocator = allocator<T>>
class vector {
  // types:
  using value_type = T;
  using allocator_type = Allocator;
  using pointer = typename allocator_traits<Allocator>::pointer;
  using const_pointer = typename allocator_traits<Allocator>::const_pointer;
  using reference = value_type&;
  using const_reference = const value_type&;
  using difference_type = implementation_defined; // 见 36.2
  using implementation_defined = implementation_defined; // 见 36.2
  using iterator = implementation_defined; // 见 36.2
  using const_iterator = implementation_defined; // 见 36.2
  using reverse_iterator = std::reverse_iterator<iterator>;
  using const_reverse_iterator = std::reverse_iterator<const_iterator>;
```

### 26.3.11.2 构造函数(拷贝/移动)

```cpp
vector() noexcept(noexcept(allocator())) : vector(allocator())
explicit vector(size_type n, const Allocator& alloc = Allocator()) : vector(n, alloc)
explicit vector(size_type n, const T& n, const Allocator& alloc = Allocator()) : vector(n, n, alloc)
template <class Input>
vector(Input first, Input last, const Allocator& alloc = Allocator()) : vector(first, last, alloc)
vector(const T& x) : vector(1, x)
vector(vector&& x) noexcept()
vector(vector&& x, const Allocator& alloc) : vector(std::move(x), alloc)
vector(initializer_list<T> l, const Allocator& alloc = Allocator()) : vector(l, alloc)
-vector();
vector& operator=(const T& x)
vector& operator=(vector&& x) noexcept(allocator_traits<Allocator>::propagate_on_move_assignment::value || allocator_traits<Allocator>::is_always_equal::value);
vector& operator=(initializer_list<T>);
template <class InputIterator>
void assign(InputIterator first, InputIterator last);
void assign(size_type n, const T & u);
void assign(initializer_list<T>);
allocator_type get_allocator() const noexcept;
```

```cpp
// iterators:
iterator begin() noexcept;
const_iterator begin() noexcept;
iterator end() noexcept;
const_iterator end() noexcept;
reverse_iterator rbegin() noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() noexcept;
const_reverse_iterator rend() const noexcept;
```

```cpp
const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
const_reverse_iterator crbeg() const noexcept;
const_reverse_iterator crend() const noexcept;
```

```cpp
// 26.3.11.3, capacity
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
size_type capacity() const noexcept;
void resize(size_type sz);
void resize(size_type sz, const T & c);
void resize(size_type n);
void shrink_to_fit();
```

```cpp
// 26.3.11.4, access
reference operator[](size_type n);
const_reference operator[](size_type n) const;
const_reference at(size_type n) const;
reference front();
reference back();
const_reference front() const;
const_reference back() const;

``` 
// 26.1.5, modifiers
template <class... Args> emplace_back(Args&& args);
void push_back(const T& x);
void push_back(T&& x);
template <class... Args> Args(const_iterator position, Args&&,);
iterator insert(const_iterator position, T& x);
iterator insert(const_iterator position,__type);
template <class InputIterator>
iterator insert(InputIterator first, InputIterator last);
iterator insert(const_iterator position, initializer_list<T> il);
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);
void clear();

```cpp
template <class... Args>
vector(Args&&... args);
template <class InputIterator>
vector(InputIterator first, InputIterator last,
       typename allocator_traits<Allocator>::size_type n = allocator_traits<Allocator>::size_type(),
       const Allocator& alloc = Allocator());
```

