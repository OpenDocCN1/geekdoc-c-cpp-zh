

# ISO/IEC 14882:2017(E)

```cpp
template <class T, class Container>
void swap(queue<T, Container&>& x, queue<T, Container&>& y) noexcept(noexcept(x.swap(y)));
```

```cpp
template <class T, class Container, class Alloc>
struct uses_allocator<queue<T, Container>, Alloc>
: :uses_allocator<Container, Alloc>::type { };
```

# 26.6.4.2 queue 构造函数

```
[queue.cons]
```

explicit queue(const Container& cont);

- 1 效果：用 cont 初始化 c。

explicit queue(const Container& cont = Container());

- 2 效果：用 std::move(cont) 初始化 c。

# 26.6.4.3 带有分配器的 queue 构造函数

```
[queue.cons]
```

- 1 如果 uses_allocator_v<queue_type, Alloc> 为 false，则此子句中的构造函数不参与重载解析。

```cpp
template <class Alloc> explicit queue(const Alloc a);
```

- 2 效果：用 a 初始化 c。

```cpp
template <class Alloc> queue(const Container_type& cont, const Alloc a);
```

- 3 效果：用 cont 作为第一个参数并作为第二个参数初始化 c。

```cpp
template <class Alloc> queue(const Container_type&& cont, const Alloc a);
```

- 4 效果：用 std::move(cont) 作为第一个参数并作为第二个参数初始化 c。

```cpp
template <class Alloc> queue(const queue_type& q, const Alloc a);
```

- 5 效果：用 q.c 作为第一个参数并作为第二个参数初始化 c。

```cpp
template <class Alloc> queue(queue&& q, const Alloc a);
```

- 6 效果：用 std::move(q.c) 作为第一个参数并作为第二个参数初始化 c。

# 26.6.4.4 queue 运算符

```
[queue.ops]
```

```cpp
template <class T, class Container>
bool operator==(const queue<T, Container>& x, const queue<T, Container>& y);
```

- 1 返回结果：x.c == y.c。

```cpp
template <class T, class Container>
bool operator!=(const queue<T, Container>& x, const queue<T, Container>& y);
```

- 2 返回结果：x.c != y.c。

```cpp
template <class T, class Container>
bool operator<(const queue<T, Container>& x, const queue<T, Container>& y);
```

- 3 返回结果：x.c < y.c。

```cpp
template <class T, class Container>
bool operator<=(const queue<T, Container>& x, const queue<T, Container>& y);
```
- 4 返回结果：x.c <= y.c。

```cpp
template <class T, class Container>
bool operator>(const queue<T, Container>& x, const queue<T, Container>& y);
```

- 5 返回结果：x.c > y.c。

```cpp
template <class T, class Container>
bool operator==(const queue<T, Container>& x, const queue<T, Container>& y);
```

- 6 返回结果：x.c == y.c。

# 26.6.4 queue 特殊化算法 [queue.special]

```cpp
template <class T, class Container>
void swap(queue<T, Container>& x, queue<T, Container>& y) noexcept(noexcept(x.swap(y)));
```

- 1 备注：除非 is_swappable_v<Container> 为 true，否则此函数不参与重载解析。

- 2 效果：等同于 x.swap(y)。

# 26.6.5 类模板 priority_queue [priority.queue]

任何具有随机迭代器并支持 front()、push_back() 和 pop_back() 操作的序列容器都可以使用。实例化 priority_queue 时，特别是 vector (20.3.11) 和 deque (20.3.8) 是适用的。比较使用算法，使得函数或函数对象定义了严格排序（28.7）。

```cpp
namespace std {
template <class T, class Container = vector<T>>
class Compare = typename Container::value_type>
class priority_queue {
public:
    using value_type = typename Container::value_type;
    using reference = typename Container::reference;
    using const_reference = typename Container::const_reference;
    using size_type = typename Container::size_type;
    using container_type = Container;
    using value_compare = Compare;

protected:
    Container c;
    Compare comp;

public:
    priority_queue(const Compare& x, const Container&);
    explicit priority_queue(const Compare& x = Compare(), const Container& k = Container());
template <class InputIterator>
    priority_queue(InputIterator first, InputIterator last,
                   const Compare& x, const Container& k);
template <class InputIterator>
    priority_queue(InputIterator first, InputIterator last,
                   const Compare& x = Compare(), const Container& k = Container());

template <class Alloc> explicit priority_queue(const Alloc&);
template <class Alloc> priority_queue(const Compare&, const Alloc&);
template <class Alloc> priority_queue(const Compare&, const Container&, const Alloc&);
template <class Alloc> priority_queue(const Compare&, const Container&&, const Alloc&);

bool empty() const;
    size_type size() const;
    const reference& top() const;
    void push(const value_type& x);
    void push(value_type&& x);
    template <class... Args> void emplace(Args&&... args);
    void pop();
    void swap(priority_queue& q) noexcept(noexcept(c.swap(q.c)));
    friend void swap(priority_queue&, priority_queue&) noexcept(using ::swap::swap);
};
```
