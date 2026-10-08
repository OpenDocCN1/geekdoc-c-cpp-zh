
```cpp
#include <initializer_list>
namespace std {
    template <class T, class Container = deque<T>> class queue;
    template <class T, class Container = vector<T>>
    class Compare = less<typename T>::value_type>
    class priority_queue;

    template <class T, class Container>
    bool operator==(const queue<T, Container>& x, const queue<T, Container>& y);
    template <class T, class Container>
    bool operator<(const queue<T, Container>& x, const queue<T, Container>& y);
    template <class T, class Container>
    bool operator!=(const queue<T, Container>& x, const queue<T, Container>& y);
```

# ISO/IEC

# N4296

```cpp
template <class T, Container>
bool operator=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, Container>
bool operator=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, Container>
bool operator<(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, Container>
void swap(queue<T, Container>& x, queue<T, Container>& y) noexcept(noexcept(x.swap(y)));
template <class T, Container, Compare>
void swap(priority_queue<T, Container, Compare>& x,
           priority_queue<T, Container, Compare>& y) noexcept(noexcept(x.swap(y)));
```

## 23.6.3 类模板 queue

### 23.6.1 queue 定义

任何支持 `front()`、`back()`、`push_back()` 和 `pop_front()` 操作的序列都可以用于实例化 `queue`。特别是，`list` (23.3.5) 和 (23.3.3) 可以使用。

```cpp
namespace std {
template <class T, Container = deque<T>>
class queue {
public:
    typedef Container::value_type value_type;
    typedef Container::reference reference;
    typedef Container::const_reference const_reference;
    typedef Container::size_type size_type;
    typedef Container::container_type container_type;
protected:
    Container c;
public:
    explicit queue(const Container&);
    explicit queue(const Alloc& Alloc);
    template <class Alloc> explicit queue(const Container&, const Alloc&);
    template <class Alloc> queue(const Container&, const Alloc&);
    template <class Alloc> queue(const Container& q, const Alloc&);
    template <class Alloc> queue(const queue& q, const Alloc&);
    bool empty() { return c.empty(); }
    size_type size() { return c.size(); }
    reference front() { return c.front(); }
    const_reference front() { return c.front(); }
    reference back() { return c.back(); }
    const_reference back() { return c.back(); }
    void push(const value_type& x) { c.push_back(x); }
    void push(value_type&& x) { c.push_back(std::move(x)); }
    template <class... Args> void emplace(Args&&... args) { c.emplace_back(std::forward<Args>(args)...); }
    void pop() { c.pop_front(); }
    void swap(queue& q) noexcept(noexcept(swap(c, q))) { using std::swap; swap(c, q); }
};
```

### 23.6.3.1

```cpp
template <class T, class Container>
bool operator*=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator*=(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator>(const queue<T, Container>& x, const queue<T, Container>& y);
template <class T, class Container>
bool operator=(const queue<T, Container>& x, const queue<T, Container>& y);
```

## 23.6.2 queue 构造函数

`explicit queue(const Container& cont);`

- 1 效果：用 `cont` 初始化 `c`。

```cpp
explicit queue(const Container& cont = Container());
```

- 2 效果：用 `std::move(cont)` 初始化 `c`。

### 23.6.3.3 带分配器的 queue 构造函数

`[queue.cons.alloc]`

- 1 如果 `uses_allocator<container_type, Alloc>::value` 为 false，则此子句中的构造函数不参与重载解析。

```cpp
template <class Alloc>
explicit queue(const Alloc& a);
```

- 2 效果：用 `a` 初始化 `c`。

```cpp
template <class Alloc>
queue(const container_type& cont, const Alloc& a);
```

- 3 效果：用 const 作为第一个参数和作为第二个参数初始化 `c`。

```cpp
template <class Alloc>
queue(container_type&& cont, const Alloc& a);
```

- 4 效果：用 `std::move(cont)` 作为第一个参数，`a` 作为第二个参数初始化 `c`。

```cpp
template <class Alloc>
queue(const_type& q, const Alloc& a);
```

- 5 效果：用 `q` 作为第一个参数，`a` 作为第二个参数初始化 `c`。

```cpp
template <class Alloc>
queue(queue&& q, const Alloc& a);
```

- 6 效果：用 `std::move(q.c)` 作为第一个参数，`a` 作为第二个参数初始化 `c`。

## 23.6.3.4 queue 运算符

```cpp
template <class T, class Container>
bool operator==(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, class Container>
bool operator!==(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, class Container>
bool operator<(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, class Container>
bool operator>(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, class Container>
bool operator<=(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, class Container>
bool operator>=(const queue<T, Container>& x, const queue<T, Container>& y);
```

```cpp
template <class T, class Container>
void swap(queue<T, Container>& x, queue<T, Container>& y);
```

## 23.6.4 类模板 priority_queue

任何具有随机访问迭代器和排序操作（`push_back`）的容器都可以用于实例化 `priority_queue`。特别是 `vector` (23.3.6) 和 `deque` (23.3.3) 可以使用。实例化 `priority_queue` 涉及到提供一个函数或对象 (25.4)。

```cpp
namespace std {
template <class T, Container = deque<T>, Compare = less<T>>
class priority_queue {
public:
    typedef Container::value_type value_type;
    typedef Container::reference reference;
    typedef Container::const_reference const_reference;
    typedef Container::size_type size_type;
    typedef Container::container_type container_type;
protected:
    Container c;
    Compare comp;
public:
    priority_queue(const Compare& x, Container&& y);
    explicit priority_queue(const Compare& x = Compare(), Container&& y = Container());
    template<class InputIterator>
    priority_queue(InputIterator first, InputIterator last, const Compare& x, Container& y);
    template<class InputIterator>
    priority_queue(InputIterator first, InputIterator last, const Compare& x = Compare(), Container&& y = Container());
    template<class Alloc>
    explicit priority_queue(const Alloc& a);
    template<class Alloc>
    priority_queue(const Compare&, Container&& y, const Alloc& a);
    template<class Alloc>
    priority_queue(const Compare&, Container&& y, const Alloc& a);
    template<class Alloc>
    priority_queue(const container_type& y, const Alloc& a);
    template<class Alloc>
    priority_queue(container_type&& y, const Alloc& a);
    template<class Alloc>
    priority_queue(const priority_queue& q, const Alloc& a);
    template<class Alloc>
    priority_queue(const priority_queue&& q, const Alloc& a);
    bool empty() const { return c.empty(); }
    size_type size() const { return c.size(); }
    const T& top() const { return c.front(); }
    T& top() { return c.front(); }
    void push(const T& x) { c.push_back(x); }
    void push(T&& x) { c.push_back(std::move(x)); }
    template<class... Args>
    void emplace(Args&&... args) { c.emplace_back(std::forward<Args>(args)...); }
    void pop() { c.pop_back(); }
    void swap(priority_queue& q) noexcept(noexcept(swap(c, q.c)) && noexcept(swap(comp, q.comp))) {
        using std::swap; swap(c, q.c); swap(comp, q.comp);
    }
};
```

```cpp
template <class T, class Container, class Compare, class Alloc>
void swap(priority_queue<T, Container, Compare>& x, priority_queue<T, Container, Compare>& y) noexcept(noexcept(x.swap(y)));
```

```cpp
template<class T, class Container, class Compare, class Alloc>
struct uses_allocator<priority_queue<T, Container, Compare>, Alloc>
    : uses_allocator<Container, Alloc>::type { };
```

### 23.6.4.1 priority_queue 构造函数

```cpp
priority_queue(const Compare& x, Container&& y);
explicit priority_queue(const Compare& x = Compare(), Container&& y = Container());
```
