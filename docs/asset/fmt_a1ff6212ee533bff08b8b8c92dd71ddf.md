
```cpp
#include <initializer_list>

namespace std {

template <class T, class Container = deque<T>> class queue;
template <class T, class Container = vector<T>,
 class Compare = typename Container::value_type>
 class priority_queue;

template <class T, class Container>
bool operator<=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator<>(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator!=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator>(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator>=(const queue<T, Container>& x, const queue<T, Container>& y);

template <class T, class Container>
void swap(queue<T, Container>& x, queue<T, Container>& y) noexcept(noexcept(x.swap(y)));
template <class T, class Container, class Compare>
 priority_queue<T, Container, Compare>
void swap(priority_queue<T, Container, Compare>& x, priority_queue<T, Container, Compare>& y) noexcept(noexcept(x.swap(y)));

```

## 23.6.3 类模板 queue [queue]

### 23.6.3.1 queue 定义 [queue.def]

1 任何支持 `front()`、`back()`、`push_back()` 和 `pop_front()` 操作的序列容器都可以用于实例化 `queue`。特别是 `list` (23.3.5) 和 `deque` (23.3.6) 可以被使用。

```cpp
namespace std {
template <class T, class Container = deque<T>>
 class queue {
 public:
    typedef	 typename Container::value_type value_type;
    typedef	 typename Container::reference reference;
    typedef	 typename Container::const_reference const_reference;
    typedef	 typename Container::size_type size_type;
    typedef	 Container container_type;
 protected:
    Container c;
 public:
    explicit queue(const Container&);
    explicit queue(Container&& = Container());

template <class Alloc> explicit queue(const Alloc&, const Alloc);
template <class Alloc> queue(Container&, const Alloc&);
template <class Alloc> queue(Container&&, const Alloc&);
template <class Alloc> queue(const queue&, const Alloc);
template <class Alloc> queue(queue&&, const Alloc);

```
```cpp
bool

    empty() { return c.empty(); }

size_type

    size() { return c.size(); }

reference

    front() { return c.front(); }

const_reference

    front() { return c.front(); }

reference

    back() { return c.back(); }

void push(const value_type& x)

    { c.push_back(x); }

void push(value_type&& x)

    { c.push_back(std::move(x)); }

template <class... Args>

void emplace(Args&&... args)

    { c.emplace(std::forward<Args>(args)...); }

void pop()

    { c.pop_front(); }

void swap(queue&& q) noexcept(noexcept(c.swap(q.c)))

    { using std::swap(c, q.c); }

};
```

template <class T, class Container>
bool operator=(const queue<T>& x, const queue<T>& y);
template <class T, class Container>
bool operator<(const queue<T>& x, const queue<T>& y);
template <class T, class Container>
bool operator>(const queue<T>& x, const queue<T>& y);
template <class T, class Container>
bool operator==(const queue<T>& x, const queue<T>& y);
template <class T, class Container>
bool operator<=(const queue<T>& x, const queue<T>& y);
template <class T, class Container>
bool operator>=(const queue<T>& x, const queue<T>& y);

template <class T, class Container>
void swap(queue<T, Container>& x, queue<T, Container>& y) noexcept(noexcept(x.swap(y)));

template <class T, class Container, class Alloc>
struct uses_allocator<queue<T, Container>, Alloc>
    { type uses_allocator<Container, Alloc>::type; };

## 23.6.3.2 queue 构造函数

explicit queue(const Container& cont);
- 1 效果：用 `cont` 初始化 `c`。
explicit queue(Container&& cont);
- 2 效果：用 `std::move(cont)` 初始化 `c`。

## 23.6.3.3 带分配器的 queue 构造函数

- 1 如果 `uses_allocator<alloc_type, Alloc>::value` 为 `false`，则该子类中的构造函数不应参与重载解析。

§ 23.6

© ISO/IEC 2011 - All rights reserved 823

# ISO/IEC 14882:2011(E)

```cpp
void pop();

void swap(priority_queue& q, priority_queue& q) noexcept(

noexcept(swap(c, q)) && noexcept(swap(comp, q.comp))

{

    std::swap(c, q); swap(comp, q.comp);

}

// 未提供相等运算符

template <class T, class Container, class Compare>

void swap(priority_queue<T, Container, Compare&>& x,

         priority_queue<T, Container, Compare&>& y) noexcept(x.swap(y));

template <class T, class Container, class Compare, class Alloc>

struct uses_allocator<priority_queue<T, Container, Compare>, Alloc>

  : uses_allocator<Container, Alloc>::type { };

```

## 23.6.4.1 priority_queue 构造函数

```cpp
priority_queue(const Compare& x, const Compare& y);

explicit priority_queue(const Compare& x = Compare(),

                         Container&& y = Container());
```

- 1 要求：`x` 应当定义一个严格弱序 (25.4)。
- 2 效果：使用 `x` 和 `y` 初始化 `c`（根据需要进行拷贝或移动）；
  调用 `make_heap(c.begin(), c.end(), comp)`。

```cpp
template <class InputIterator>

priority_queue(InputIterator first, InputIterator last,

               const Compare& x,

               const Compare& y);
```

```cpp
template <class InputIterator>

template <class Container, class Compare>

priority_queue(InputIterator first, InputIterator last,

               const Compare& x = Compare(),

               Container&& y = Container());
```

- 3 要求：`x` 应当定义一个严格弱序 (25.4)。
- 4 效果：使用 `x` 和 `y` 初始化 `c`（根据需要进行拷贝或移动）；
  调用 `c.insert(c.begin(), first, last)`；最后调用 `make_heap(c.begin(), c.end(), comp)`。

## 23.6.4.2 带有分配器的 priority_queue 构造函数

- 1 如果 `uses_allocator<container_type, Alloc>::value` 为 `false`，则此条款中的构造函数不应参与重载解析。

```cpp
template <class Alloc>

explicit priority_queue(const Alloc& a);
```

- 2 效果：使用 `a` 初始化 `c` 并对 `comp` 进行值初始化。

```cpp
template <class Alloc>

priority_queue(const Compare& compare, const Alloc& a);
```

- 3 效果：使用 `a` 初始化 `c`，并用 `compare` 初始化 `comp`。

```cpp
template <class Alloc>

priority_queue(const Compare& compare, const Container& cont, const Alloc& a);
```

效果：使用第一个参数和参数、 `a` 作为第二个参数初始化 `c`，并用 `compare` 初始化 `comp`。

```cpp
template <class Alloc>

priority_queue(const Compare& compare, Container&& cont, const Alloc& a);
```

效果：使用 `std::move(cont)` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `compare` 初始化 `comp`。

```cpp
template <class Alloc>

priority_queue(const priority_queue& q, const Alloc& a);
```

效果：使用 `q.c` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `q.comp` 初始化 `comp`。

```cpp
template <class Alloc>

priority_queue(priority_queue& q, const Alloc& a);
```

效果：使用 `std::move(q.c)` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `std::move(q.comp)` 初始化 `comp`。

## 23.6.4.3 priority_queue 成员

```cpp
void push(const value_type& x);
```

效果：
- `c.push_back(x)`
- `push_heap(c.begin(), c.end(), comp);`

```cpp
void push(value_type&& x);
```

效果：
- `c.push_back(std::move(x))`
- `push_heap(c.begin(), c.end(), comp);`

```cpp
template <class... Args>

void emplace(Args&&...);
```

效果：
- `c.emplace(std::forward<Args>(args)...)`
- `push_heap(c.begin(), c.end(), comp);`

```cpp
void pop();
```
效果：
- `c.pop_back()`
- `pop_heap(c.begin(), c.end(), comp);`

```cpp
const value_type& top() const;
```
效果：
- `return c.back();`

```cpp
bool empty() const;
```
效果：
- `return c.empty();`

```cpp
size_type size() const;
```
效果：
- `return c.size();`

## 23.6.4.4 priority_queue 算法

```cpp
template <class T, class Container, class Compare>
void swap(priority_queue<T, Container, Compare&>& x,
         priority_queue<T, Container, Compare&>& y) noexcept(x.swap(y));
```

效果：
- `x.swap(y);`

## 23.6.4.5 Stack 类

支持 `back()`、`push_back()` 的容器都可以用于实例化 `stack`。特别是 `vector` (23.6)、`list` (23.5) 和 `deque` (23.3) 可以用于。

### 23.6.5.1 Header 概述
