

# ISO/IEC 14882:2017(E)

```cpp
void swap(vector& x)
noexcept(allocator_traits<Allocator>::propagate_on_container_swap::value ||
    allocator_traits<Allocator>::is_always_equal);
```

影响：交换 *this* 与 *x* 的内容和 `capacity()`。

复杂度：常数时间。

```cpp
void resize(size_type sz);
```

影响：如果 `sz < size()`，则从序列中删除最后的 `(size() - sz)` 个元素。否则，在序列末尾追加 `sz - size() - inserted elements` 个元素。

要求：*this* 必须是 `MoveInsertable` 且 `DefaultInsertable`。

备注：如果抛出了非 `CopyInsertable T` 类型的移动构造函数以外的异常，则没有影响。

```cpp
void resize(size_type sz, const T& c);
```

影响：如果 `sz < size()`，则从序列中删除最后的 `(size() - sz)` 个元素。否则，在序列末尾追加 `sz` 个 `c` 的拷贝。

要求：*this* 必须是可 `CopyInsertable` 的。

备注：如果抛出了异常，则没有影响。

## 26.3.11.4 vector 数据 [vector.data]

```cpp
T* data() noexcept;
const T* data() noexcept;
```

返回：一个指向 `data()` 的指针，`data + size()` 是一个有效范围。对于非空 vector，`data() == addressof(front())`。

复杂度：常数时间。

## 26.3.11.5 vector 修饰符 [vector.modifiers]

```cpp
iterator insert(const_iterator position, const T& x);
iterator insert(const_iterator position, T&& x);
iterator insert(const_iterator position, size_type n, const T& x);
template <class InputIterator>
iterator insert(const_iterator position, InputIterator last);
iterator insert(const_iterator position, initializer_list<InputIterator> last);
```

```cpp
template <class... Args> Args& emplace_back(Args&... args);
template <class... Args> Args& emplace(const_iterator position, Args&&... args);
push_back(const T& x);
push_back(T&& x);
```

备注：如果新大小大于当前数据大小，重新分配将使引用序列的引用、指针和迭代器失效。如果没有发生重新分配，则插入之前的所有迭代器和引用均保持有效。如果抛出了除 `T` 的移动构造函数、赋值运算符或移动赋值运算符以外的异常，或由任何 `InputIterator` 抛出的异常，则没有影响。如果在在该位置插入单个元素时，该元素是 `CopyInsertable` 或 `is_nothrow_move_constructible-T` 为真抛出了异常，则没有影响。否则，异常由非 `CopyInsertable T` 的移动构造函数抛出，影响是未定义的。

复杂度：复杂度与插入元素的数量加上到 vector 末尾的距离呈线性。

```cpp
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);
pop_back();
```

- 影响：使删除点或其之后的迭代器和引用失效。
- 复杂度：`T` 的析构函数调用次数等于删除元素的数量，但 `T` 的赋值运算符的调用次数等于删除元素后 vector 中剩余元素的数量。
- 抛出：除非由 `T` 的赋值运算符或移动赋值运算符抛出了异常。

## 26.3.11.6 vector 特殊化算法 [vector.special]

```cpp
template<class T, class Allocator>
void swap(vector<T, Allocator>& x, vector<T, Allocator>& y)
noexcept(x.swap(y));
```

- 影响：等同于通过 `x.swap(y)`。

## 26.3.12 class vector<bool> [vector.bool]

- 1 为了优化空间分配，提供了针对 `bool` 元素的特化版本：

```cpp
namespace std {
template <class Allocator>
class vector<bool, Allocator> {
public:
  // 类型定义:
  using value_type = bool;
  using allocator_type = Allocator;
  using pointer = implementation-defined;
  using const_pointer = implementation-defined;
  using const_reference = bool;
  using reference_type = implementation-defined; // own 26.2
  using difference_type = implementation-defined; //  26.2
  using iterator = implementation-defined; //  26.2
  using const_iterator = implementation-defined; //  26.2
  using reverse_iterator = std::reverse_iterator<iterator>;
  using const_reverse_iterator = std::reverse_iterator<const_iterator>;

  // 位引用
  class reference {
    friend class vector;
    friend class const_vector;
public:
    reference(const bool) noexcept;
    operator bool() const noexcept;
    reference& operator=(const bool x) noexcept;
    reference& operator=(const reference& x) noexcept;
    void flip() noexcept; // 翻转比特位
  };

  // 构造函数/拷贝/析构
  vector() : vector(Allocator()) {}
  explicit vector(const Allocator& alloc);
  explicit vector(size_type n, const Allocator& alloc);
  vector(size_type n, const Allocator& alloc);
```cpp
  template<class InputIterator>
  vector(InputIterator first, InputIterator last);
  template<class InputIterator>
  vector(const_iterator first, InputIterator last);
  template<class InputIterator>
  vector(initializer_list<InputIterator> last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator<,Input_> last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_
 last

templatetemplate<

>
  vectorvectorvector,,ator> last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<

vector>
  vector(___,,








);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last

vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, last_
 last);
  template<class
Iterator  
  vector_iterator_iterator_iterator last);
  template<class InputIterator>
  vector(initializer_list<InputIterator> last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  template<class InputIterator>
  vector(initializer_list<InputIterator> last);
  template<class InputIterator>
  vector(const_iterator first, const_
template<class InputIterator>
  vector(const_iterator first, const_iterator last);
  push_back(const T& x);
  push_back(T&& x);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
  reference reference;
  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x) noexcept;
  flip() noexcept;
  empty() const;
  size_type size() const;
  size_type max_size() const;
  reserve(size_type n);
  resize(size_type n, bool);
  shrink_to_fit();
  operator[](size_type n);
  const reference operator[](size_type n) const;
  at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;
  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator rend();
  const_reverse_iterator rend();
  emplace_back(Args&... args);
  emplace(const_iterator position, Args&&... args);
  push_back(const T& x);
  push_back(T&& x);
  push_back(size_type n);
  pop_back();
  erase(const_iterator position);
  erase(const_iterator first, const_iterator last);
  swap(vector& x);
  swap(vector<T, Allocator>& x, vector<T, Allocator>& y);
