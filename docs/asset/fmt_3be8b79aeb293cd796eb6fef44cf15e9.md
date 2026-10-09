
### 数据访问

```cpp
const reference& at(size_type n) const;
reference& at(size_type n);
const reference front() const;
reference& front();
const reference back() const;
reference& back();
```

### 数据访问

```cpp
// 22.3.11.4, data access
const T* data() const noexcept;
// 22.3.11.5, modifiers
template<class... Args>
void replace_back(Args&&... args);
void push_back(const T& x);
void push_back(T&& x);
template<class... Args>
const_iterator emplace(const_iterator position, Args&&... args);
const_iterator insert(const_iterator position, const T& x);
const_iterator insert(const_iterator position, T&& x);
const_iterator insert(const_iterator position, size_type n, const T& x);
template<class InputIterator>
const_iterator insert(const_iterator position, InputIterator first, InputIterator last);
const_iterator insert(const_iterator position, initializer_list<T> il);
const_iterator erase(const_iterator position);
void swap(const_iterator first, const_iterator last)
noexcept(allocator_traits<Allocator>::propagate_on_container_swap::value ||
allocator_traits<Allocator>::is_always_equal::value);
void clear() noexcept;
```

```cpp
template<class InputIterator, class Allocator = allocator<typename InputIterator::value_type>>
vector(InputIterator first, InputIterator last, const Allocator& alloc = Allocator())
vector(typename InputIterator::value_type, const Allocator& alloc);
```

```cpp
// swap
template<class T, class Allocator>
void swap(vector<T, Allocator>& x, vector<T, Allocator>& y)
noexcept(noexcept(swap(x, y)));
```

### 22.3.11.2 构造函数 [vector.cons]

```cpp
vector(const Allocator& alloc) noexcept;
```
- 1 影响：使用指定的分配器构造一个空 `vector`。
- 2 复杂度：常数。

```cpp
vector(size_type n, const Allocator& alloc = Allocator());
```
- 3 前提：`*this` 符合 `C17Defaultable`。
- 4 影响：使用指定的分配器构造包含 `n` 个默认插入元素的 `vector`。
- 5 复杂度：`n` 的线性。

```cpp
vector(size_type n, const T& value, const Allocator& alloc = Allocator());
```
- 6 前提：`*this` 符合 `C17CopyInsertable`。
- 7 影响：使用指定的分配器构造包含 `n` 个 `value` 拷贝的 `vector`。
- 8 复杂度：`n` 的线性。

```cpp
template<class InputIterator>
vector(InputIterator first, InputIterator last, const Allocator& alloc = Allocator());
```
- 9 影响：使用指定的分配器构造一个等于 `[first, last)` 范围的 `vector`。
复杂度：如果 `first` 和 `last` 是前向、双向或随机访问分类，则仅调用 `N` 次 `T` 的拷贝构造函数（`N` 为 `first` `last` 之间的距离）且不进行重新分配。如果它们只是输入分类，则调用 `N` 次拷贝构造函数并进行 `N` 次重新分配。

## 22.3.11.3 容量

```cpp
size_type capacity() const noexcept;
```
返回：`vector` 不需要重新分配就可以容容的元素总数。

复杂度：常量时间。

```cpp
void reserve(size_type n);
```
前提：`*this` 符合 `C17Insertable`。

影响：使所有指向计划更改大小的引用失效，以便相应管理存储分配。在 `reserve()` 之后，如果发生了重新分配，`capacity()` 大于或等于 `reserve` 的参数；重新分配发生在此时，且仅当当前容量小于 `reserve` 的参数时。如果非 `C17Insertable` 类型的构造函数抛出异常，则没有影响。

复杂度：它不改变序列的大小，在序列的大小范围内最多需要线性时间。

抛出：`length_error`（如果 `n > max_size()`）。

备注：重新分配使序列中所有元素的引用、指针和迭代器失效，就像传入的结束迭代器失效一样。

> 注 1：如果没有发生重新分配，它们保持有效。

在调用 `reserve()` 之后的插入期间或当插入会导致 `vector` 的大小大于 `capacity()` 的值时，不发生重新分配。

```cpp
void shrink_to_fit();
```
前提：`*this` 符合 `C17Insertable`。

影响：`shrink_to_fit` 是将容量减少到 `size()` 的非绑定请求。

> 注 2：该请求是非绑定的，以便为实现优化留出余地。

它不会增加容量，但可能通过引起重新分配来减少容量。如果非 `C17Insertable` `T` 的移动构造函数抛出异常，则没有影响。

复杂度：如果发生了重新分配，是序列大小的线性。

备注：它使序列中所有元素的引用、指针和迭代器失效，就像传入的结束迭代器失效一样。

> 注 3：如果没有发生交换，它们保持有效。

```cpp
void swap(vector& x)
noexcept(allocator_traits<Allocator>::propagate_on_container_swap::value ||
allocator_traits<Allocator>::is_always_equal::value);
```
影响：交换 `*this` 与 `x` 的内容和 `capacity()`。

复杂度：常数时间。

```cpp
void resize(size_type n);
```
前提：`*this` 符合 `C17Insertable` 和 `C17Defaultable`。

影响：如果 `size < n`，则从序列中删除最后的 `size()` 个元素。否则，在序列末尾追加 `sz = size()` 个默认插入元素。

备注：如果抛出除非 `C17CopyInsertable` `T` 的移动构造函数以外的异常，则没有影响。

# ISO/IEC 14882:2020(E)

17 前置条件：`T` 是 `Cpp17CopyInsertable` 到 `*this*` 的。

18 影响：如果 `sz < size()`，则保留序列最后的 `size(sz) - sz` 个元素。否则，向序列末尾追加 `sz = size()` 个 `c` 的拷贝。

19 备注：如果抛出异常，则不产生影响。

## 22.3.11.4 数据 [vector.data]

```cpp
constexpr T data noexcept;
const T* data noexcept;
```
- 1 返回：指向此类(`data`) 的指针，`data() + size(sz)` 是一个有效范围。对于非空 `vector`，`data() == offset(front())`。
- 2 复杂度：常数时间。

## 22.3.11.5 修改器 [vector.modifiers]

```cpp
constexpr iterator insert(const_iterator_position, const T& x);
constexpr iterator insert(const_iterator_position, T& x);
constexpr iterator insert(const_iterator_position, size_type n, const T& x);
template<class InputIterator>
constexpr iterator insert(const_iterator_position, InputIterator first, InputIterator last, nIterator last);
constexpr iterator insert(const_iterator_position, initializer_list<T>);
```

```cpp
template<class Args> void push_back(Args&&... args);
template<class Args> void push_back(const_iterator_position, Args&&... args);
constexpr void push_back(const T& x);
```
如果新大小大于当前容量，则发生分配。重新分配会使所有指向序列中元素的引用、指针和迭代器，以及结束迭代器失效。如果没有发生重新分配，则插入点之前的引用、指针和迭代器将保持有效，直到插入点之后，包括过末尾迭代器（past-end iterator）失效。如果抛出的异常不是由 `T` 的拷贝构造函数、移动构造函数、赋值或移动赋值或任何 `InputIterator` 抛出的，则不产生影响。如果在构造期间抛出异常且 `T` 是 `CppCopyInsertable` 或不是 `not_move_constructible<T>`，则由非 `CppCopyInsertable` `T` 的构造函数抛出异常，影响是不确定的。

- 2 复杂度：如果发生重新分配，则与结果 `vector` 的元素数量线性相关；否则，与插入的元素数量加上到 `vector` 末尾的距离线性相关。

```cpp
constexpr iterator erase(const_iterator_position);
constexpr erase(const_iterator first, const_iterator last);
constexpr void pop_back();
```
- 3 影响：使删除点或其之后的迭代器和引用失效。
- 4 复杂度：`T` 的构造函数调用次数等于被删除元素的数量，但 `T` 的赋值运算符的调用次数等于删除元素后 `vector` 中的元素数量。
- 5 抛出：除非 `T` 的赋值运算符或移动赋值运算符抛出异常，否则不抛出异常。

## 22.3.11.6 删除 [vector.erase]

```cpp
template<class T, class Allocator, class U>
constexpr typename vector<T, Allocator>::size_type
erase(vector<T, Allocator>& c, const U& value);
```
- 1 影响：等效于

```cpp
auto it = remove(c.begin(), c.end(), value);
auto r = distance(it, c.end());
c.erase(it, c.end());
```

return r;

```cpp
template<class T, class Allocator, class Predicate>
constexpr vector<T, Allocator>::size_type
erase(vector<T, Allocator>& c, Predicate pred);
```
影响：等效于：

```cpp
auto it = remove_if(c.begin(), c.end());
auto r = distance(it, c.end());
erase(it, c.end());
return r;
```

## 22.3.1 类 `vector<bool>`

为了优化空间分配，提供了一个针对 `bool` 元素的 `vector` 特化化：

```cpp
namespace std {
template<class Allocator>
class vector<bool, Allocator> {
public:
  // 类型
  using value_type = bool;
  using allocator_type = implementation-defined;
  using pointer = implementation-defined;
  using const_pointer = implementation-defined;
  using reference = bool; // 22.9
  using size_type = implementation-defined; // 22.9
  using difference_type = implementation-defined; // 22.9
  using iterator = implementation-defined; // 22.9
  using const_iterator = implementation-defined;
  using reverse_iterator = std::reverse_iterator<iterator>;
  using const_reverse_iterator = std::reverse_iterator<const_iterator>;
  // 位引用
  class reference {
    friend class vector;
    constexpr reference reference() noexcept;
  public:
      constexpr reference(const reference&) = default;
      const reference reference();
      constexpr reference operator bool() const noexcept;
      constexpr reference operator=(const bool x) noexcept;
      constexpr reference& operator=(const reference& x) noexcept;
      constexpr reference void flip() noexcept; // 翻转位
  };
  // 构造/析毁
  constexpr vector(Allocator()) {}
  constexpr vector(size_type n, const Allocator&);
  template<class Iterator>
  constexpr vector(Iterator first, Iterator last, const Allocator&);
  template<class Iterator>
  constexpr vector(const Iterator first, const Iterator last, const Allocator&);
  constexpr vector(initializer_list<bool>, const Allocator&);
  constexpr vector(const Allocator&);
  constexpr vector(Allocator&&);
  constexpr vector(const vector&);
  constexpr vector(vector&&);
  ~vector();
  vector& operator=(const vector&);
  vector& operator=(vector&&);
  void swap(vector&) noexcept;
  // 迭代器
  iterator begin() noexcept;
  const_iterator begin() noexcept;
  iterator end() noexcept;
  const_iterator end() noexcept;
  reverse_iterator begin() noexcept;
  reverse_iterator begin() noexcept;
  reverse_iterator rend() noexcept;
  reverse_iterator rend() noexcept;
```
