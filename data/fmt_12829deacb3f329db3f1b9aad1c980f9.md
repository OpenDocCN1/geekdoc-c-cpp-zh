
```cpp
namespace std {
template<class T, class Container = vector<T>>
class priority_queue {
public:
    using value_type = typename Container::value_type;
    using reference = typename Container::reference;
    using const_reference = typename Container::const_reference;
    using size_type = typename Container::size_type;
    using container_type = Container;
    using value_compare = Container::value_compare;

protected:
    Container C;
    Compare comp;

public:
    priority_queue() : priority_queue(Compare()) {}
    explicit priority_queue(const queue<T, Container>& x) : priority_queue(x, Compare()) {}
    explicit priority_queue(const queue<T, Container>& x, const Compare& x) : priority_queue()
    template<class Iterator>
    priority_queue(Iterator first, Iterator last, const Compare& x) : priority_queue(first, last, x) {}
    template<class Iterator>
    priority_queue(Iterator first, Iterator last) { 
    template<class Container, class Alloc = Allocator<typename Container::value_type>>
    priority_queue(const Container& x, const Compare& comp, const Alloc& alloc) { 
    template<class Container, class Alloc = Allocator<typename Container::value_type>>
    priority_queue(const Container& x, const Alloc& alloc) :
    template<class Container, class Alloc = Allocator<typename Container::value_type>>
    priority_queue(const Container& x, const Compare& comp, const Alloc& alloc) : 
    template<class Container, class Alloc = Allocator<typename Container::value_type>>
    priority_queue(const Container& x, const Compare& comp, const Alloc& alloc)
    [[nodiscard]] bool empty() const { return C.empty(); }
    size_type size() const { return C.size(); }
    const_reference top() const { return C.front(); }
    void push(const value_type x) { C.push_back(x); }
    void push(value_type x) { C.push_back(std::move(x)); }
    void pop() { C.pop_front(); }
```

### 22.6.5.2 构造函数

```cpp
priority_queue(const Compare& x, const Container& y);
priority_queue(const Compare& x, const&& y);
```

- 1 前提条件：`x` 定义了严格排序 (25.8)。
- 2 效果：使用 `x` 和 `y` 初始化堆（拷贝或移动），调用 `make_heap(C.begin(), C.end(), comp);`

```cpp
template<class Iterator>
priority_queue(Iterator first, Iterator last, const Compare& x, const Container& y)
    : Container(y), comp(x);
```

- 3 前提条件：`x` 定义了严格排序 (25.8)。
- 4 效果：使用 `x` 和 `y` 初始化堆（拷贝或移动），调用 `insert(C.end(), first, last);` 并最后调用 `make_heap(C.begin(), C.end(), comp);`

### 22.6.5.3 带分配器的构造函数

- 1 如果 `uses_allocator<value_type, Alloc>` 为 false，则此子类中的构造函数不参与重载解析。

```cpp
template<class Alloc> priority_queue(const Compare& compare, const Alloc& a);
template<class Alloc> priority_queue(const Compare& compare, const Alloc& a) noexcept();
```

- 2 效果：使用 `a` 初始化 `C`，并值初始化 `comp`。
- 3 效果：使用 `a` 初始化 `C`，并使用 `compare` 初始化 `comp`。

```cpp
template<class Alloc>
```

```cpp
priority_queue(const Compare& compare, const Container& cont, const Alloc& alloc = Alloc());
```

影响：使用 `compare` 作为第一个参数和第二个参数初始化 `c`，并用 `compare` 初始化 `comp`；调用 `make_heap(c.begin(), c.end(), comp)`。

```cpp
template<class Alloc>
```

```cpp
priority_queue(const Compare& compare, const Container& cont, const Alloc& alloc = Alloc());
```

影响：使用 `std::move(cont)` 作为第一个参数和第二个参数初始化 `c`，并用 `compare` 初始化 `comp`；调用 `make_heap(c.begin(), c.end(), comp)`。

```cpp
template<class Alloc>
priority_queue(const priority_queue& q, const Alloc& alloc = Alloc());
```

影响：使用 `std::move(q)` 作为第一个参数初始化 `c`，并用 `q` 初始化 `comp`；调用 `make_heap(c.begin(), c.end(), q)`。

```cpp
template<class Alloc>
```

`priority_queue(priority_queue& q, const Alloc& alloc = Alloc());`

影响：使用 `std::move(q)` 作为第一个参数和第二个参数初始化 `c`，并用 `std::move(q.comp)` 初始化 `comp`。

## 22.6.5.4 成员 [priority_queue.members]

```cpp
void push(const value_type& x);
```

影响：等同：
```cpp
c.push_back(); push_heap(c.begin(), c.end(), comp);
```

```cpp
void push(value_type&& x);
```

影响：等同于：
```cpp
c.push_back(std::move(x)); push_heap(c.begin(), c.end(), comp);
```

```cpp
template<class...> void emplace(Args&&..., Args&&... args);
```

影响：等同于：
```cpp
c.emplace(std::forward<Args>(args)...); push_heap(c.begin(), c.end(), comp);
```

```cpp
void pop();
```

影响：等同于：
```cpp
pop_heap(c.begin(), c.end(), comp); c.pop_back();
```

## 22.6.5.5 特殊化算法 [priority_queue.special]

```cpp
template<class T, class Container, class Compare>
void swap(priority_queue<T, Container, Compare>& x, priority_queue<T, Container, Compare>& y) noexcept(noexcept(x.swap(y)));
```

约束：`is_swappable_v<Container>` 为 `true` 且 `is_swappable_v<Compare>` 为 `true`。
影响：等同于 `x.swap(y)`。

## 22.6.6 类模板栈 [stack]

## 22.6.6.1 通用 [stack.general]

任何支持 `back()`、`push_back()` 和 `pop_back()` 操作的序列容器都可以用于实例化 `stack`。特别是 `vector` (22.3.11)、`list` (22.3.10) 和 `deque` (22.3.8) 可以被使用。

## 22.6.6.2 定义

```cpp
namespace std {
template<class T, class Container = deque<T>>
class stack {
public:
```

```cpp
using value_type             = typename Container::value_type;
using reference             = typename Container::reference;
using const_reference      = typename Container::const_reference;
using size_type             = typename Container::size_type;
using container_type        = Container;
```

protected:
Container c;

```cpp
public:
    stack() : stack(Alloc()) {}
    explicit stack(const Alloc& alloc);
    explicit stack(Alloc&& alloc);
    template<class Alloc> stack(const Container&, const Alloc& alloc);
    template<class Alloc> stack(Container&&, const Alloc& alloc);
    template<class Alloc> stack(const stack& s, const Alloc& alloc);
    template<class Alloc> stack(stack&& s, const Alloc& alloc);
```

```cpp
[nodiscard] bool empty() { return c.empty(); }
size_type size() const { return c.size(); }
reference& top() { return c.back(); }
const_reference top() const { return c.back(); }
void push(const value_type& x) { c.push_back(x); }
void push(value_type&& x) { c.push_back(std::move(x)); }
template<class... Args>
void emplace(Args&&... args) { return c.emplace_back(std::forward<Args>(args)...); }
void pop() { c.pop_back(); }
void swap(stack& s) noexcept(is_nothrow, is_swappable<Container>) {
    std::swap(c, s.c);
}
```

```cpp
template<class Alloc>
stack(Container) -> typename Container::value_type, Container>;
template<class Alloc>
stack(Container, Alloc) -> typename Container::value_type, Container>;
template<class T, class Container, class Alloc>
struct use_allocator<Container, Alloc>
    : ::alloc_allocator<Container, Alloc>::type { };
```

## 22.6.6.3 构造函数 [stack.cons]

```cpp
explicit stack(const Alloc& cont);
```
- 1 使用 `cont` 初始化 `c`。

```cpp
explicit stack(Alloc&& cont);
```
- 2 使用 `std::move(cont)` 初始化 `c`。

## 22.6.6.4 带有分配器的构造函数 [stack.alloc]

- 1 如果 `use_allocator_v<Container_type, Alloc>` 为 `false`，则不参与重载解析。

```cpp
template<class Alloc> stack(const Alloc& alloc);
```
- 2 使用 `a` 初始化 `c`。

```cpp
template<class Alloc> stack(const container_type& cont, const Alloc& alloc);
```
- 3 使用第一个参数和第二个参数初始化 `c`。

```cpp
template<class Alloc> stack(container_type&& c, const Alloc& alloc);
```
使用 `std::move(c)` 作为第一个参数和第二个参数初始化 `c`。

```cpp
template<class Alloc> stack(const stack& s, const Alloc& alloc);
```
使用 `std::move(s.c)` 作为第一个参数和第二个参数初始化 `c`。

```cpp
template<class Alloc> stack(stack&& s, const Alloc& alloc);
```
使用 `std::move(s.c)` 作为第一个参数和第二个参数初始化 `c`。

## 22.6.5 运算符 [stack.ops]

```cpp
template<class T, class Container>
bool operator=(const stack<T, Container>& x, const stack<T, Container>& y);
```
- 1 返回：`x.c = y`。

```cpp
template<class T, class Container>
bool operator!=(const stack<T, Container>& x, const stack<T, Container>& y);
```
- 2 返回：`x.c != y.c`。

```cpp
template<class T, class Container>
bool operator<(const stack<T, Container>& x, const stack<T, Container>& y);
```
- 3 返回：`x.c < y.c`。

```cpp
template<class T, class Container>
bool operator>(const stack<T, Container>& x, const stack<T, Container>& y);
```
- 4 返回：`x.c > y.c`。

```cpp
template<class T, class Container>
