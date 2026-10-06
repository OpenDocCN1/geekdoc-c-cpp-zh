

# ISO/IEC 14882:2017(E)

## 26.3.7.8 零大小数组 [array.zero]

- 1 数组应该支持 N == 0 的特殊情况。
- 2 在 N == 0 的情况下，`begin() == end() == data()` 的唯一值是不确定的。
- 3 对于零大小数组，调用 `front()` 或 `back()` 的效果是未定义的。
- 4 成员函数 `swap()` 应该具有非抛出的异常规范。

## 26.3.7.9 元组到类模板数组 [array.tuple]

```cpp
template <class T, size_t N>
struct size_array<array<T, N>> : integral_constant<size_t, N> { };
tuple_element<I, array<T, N>>::type
```

- 需要 I：如果 I 越界，则程序为格式不正确。

```cpp
template <size_t I, class T, size_t N>
const T& get(array<T, N>& a) noexcept;
```

- 需要 I：如果 I 越界，则程序为格式不正确。
- 返回：a 的第 I 个元素，索引从 0 开始。

## 26.3.8 类模板 deque [deque.overview]

### 26.3.8.1 类模板 deque 概述

deque 满足可逆容器的所有要求（参见 27.2 中的表格）。此外，它支持在开头或末尾进行常数时间的插入和删除；在中间的插入和删除需要线性时间。deque 在开头和末尾推入和弹出元素进行了专门优化。存储管理由系统自动处理。

deque 满足可逆容器（参见 27.2 中的表格）、序列容器（包括可选的序列容器要求 (26.2.3)）以及分配器感知容器（表 86）的所有要求。此处仅对未在上述表格任一中描述的 deque 操作，或对具有额外语义信息的操作提供描述。

```cpp
namespace std {
template <class T, class Allocator = allocator<T>>
class deque {
public:
  //...
  using value_type = T;
  using allocator_type = Allocator;
  using pointer = typename allocator_traits<Allocator>::pointer;
  using const_pointer = typename allocator_traits<Allocator>::const_pointer;
  using reference = T&;
  using const_reference = const T&;
  using size_type = size_type;
  using difference_type = difference_type;
  using iterator = implementation-defined; // sec 26.2
  using reverse_iterator = implementation-defined; // sec 26.2
  using const_iterator = implementation-defined; // sec 26.2
```

```cpp
using const_iterator = implementation-defined; // see 26.2
using reverse_iterator = std::reverse_iterator<iterator>;
using const_reverse_iterator = std::reverse_iterator<const_iterator>;

// 26.3.8.2,构造/拷贝/析析
deque() : Allocator(Allocator()) {}
explicit deque(const Allocator&);
explicit deque(size_type n, const T& value, const Allocator& alloc = Allocator()) : Allocator(alloc) {}
template <class Iterator>
deque(InputIterator first, InputIterator last, const Allocator& alloc = Allocator());
deque(const deque& x);
deque(deque&& x);
deque(const Allocator&);
deque(initializer_list<T>, const Allocator& alloc = Allocator());

deque& operator=(const deque& x);
deque& operator=(deque&& x) noexcept(noexcept(std::allocator<T>::is_always_equal));
deque& operator=(initializer_list<T>) const noexcept;
template <class Iterator>
void assign(InputIterator first, InputIterator last);
void assign(size_type n, const T& value);
void assign(initializer_list<T>) const noexcept;
allocator_type get_allocator() const noexcept;
```

```cpp
// 迭代器:
iterator begin() const noexcept;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator end() const noexcept;
reverse_iterator begin() const noexcept;
const_reverse_iterator begin() const noexcept;
reverse_iterator rend() const noexcept;
const_reverse_iterator rend() const noexcept;
const_iterator begin() const noexcept;
const_iterator const() const noexcept;
const_reverse_iterator cregin() const noexcept;
const_reverse_iterator rend() const noexcept;
```

```cpp
// 26.3.8.3, 容量
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
void resize(size_type n);
void resize(size_type n, const T& c);
void shrink_to_fit();
```

```cpp
// 元素访问:
reference operator[](size_type n);
const_reference operator[](size_type n) const;
reference at(size_type n);
const_reference at(size_type n) const;
```

```cpp
reference front();
const_reference front() const;
reference back();
const_reference back() const;
```

```cpp
// 26.3.8.4. 修改符
template <class..., typename... Args> emplace_back(Args&& args);
template <class..., typename... Args> iterator emplace(const_iterator position, Args&&... args);
```

```cpp
void push_front(T& x);
void push_back(T& x);

iterator insert(const_iterator position, T& x);
iterator insert(const_iterator position, T&& x);
iterator insert(const_iterator position, size_type n, const T& c);
template <class Iterator>
iterator insert(InputIterator first, InputIterator last);
iterator insert(const_iterator position, initializer_list<T>);

void pop_front();
void pop_back();

erase(const_iterator position);
erase(InputIterator first, InputIterator last);
clear();

void swap(deque& y) noexcept(noexcept(this.swap(y)));
void swap(y);
```

### 26.3.8.1 deque 构造函数

### 26.3.8.2 deque 构造函数、拷贝与赋值

### 26.3.8.3 deque 容量

### 26.3.8.4 deque 修改符

### 26.3.8.5 deque 算法

