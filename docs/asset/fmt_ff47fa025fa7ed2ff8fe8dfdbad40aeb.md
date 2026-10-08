
- 要求：`x` 定义了一个严格弱序 (25.4)。

- 效果：用 `x` 初始化 `comp`，用 `y` 初始化 `c`（拷贝构造或移动构造视情况而定）；

调用 `make_heap(c.begin(), c.end(), comp)`。

```cpp
template <class Iterator>
    priority_queue(InputIterator first, InputIterator last,
    const Compare& x,
    const Container& y);
template <class Iterator>
    priority_queue(InputIterator first, InputIterator last,
    const Compare& x = Compare(),
    Container& y = Container());
```

### 3 要求：`x` 应当定义一个严格序 (25.4)。

### 4 效果：用 `x` 和 `c` 初始化 `c`（根据情况使用拷贝构造或移动构造）；
调用 `c.insert(c.end(), first, last)`; 并调用 `make_heap(c.begin(), c.end(), comp)`。

## 23.6.4.2 带有分配器的 priority_queue 构造函数 [priorityqueue.cons.alloc]

+ 1 如果 `uses_allocator<container_type, Alloc>` 为 `false`，则此子句中的构造函数不应参与重载解析。

```cpp
template <class Alloc>
    explicit priority_queue(const Alloc a);
```

2 效果：用 `a` 初始化 `c` 并对 `comp` 进行值初始化。

```cpp
template <class Alloc>
    priority_queue(const Compare& compare, const Alloc& a);
```

3 效果：用 `compare` 初始化 `c`，并用 `compare` 初始化 `comp`。

```cpp
template <class Alloc>
    priority_queue(const Compare& compare, const Container& cont, const Alloc& a);
```

4 效果：用 `cont` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `compare` 初始化 `comp`。

```cpp
template <class Alloc>
    priority_queue(const Compare& compare, const Container& cont, const Alloc& a);
```

5 效果：用 `std::move(cont)` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `compare` 初始化 `comp`。

```cpp
template <class Alloc>
    priority_queue(const priority_queue& q, const Alloc& a);
```

6 效果：用 `q.c` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `q.comp` 初始化 `comp`。

```cpp
template <class Alloc>
    priority_queue(priority_queue& q, const Alloc& a);
```

7 效果：用 `std::move(q.c)` 作为第一个参数、`a` 作为第二个参数初始化 `c`，并用 `std::move(q.comp)` 初始化 `comp`。

## 23.6.4.3 priority_queue 成员

```cpp
void push(const value_type& x);
```

效果：
+ `c.push_back(x);`
`push_heap(c.begin(), c.end(), comp);`

```cpp
void push(value_type&& x);
```

效果：
+ `c.push_back(std::move(x));`
`push_heap(c.begin(), c.end(), comp);`

```cpp
template <class... Args> void emplace(Args&& args);
```

效果：
+ `c.emplace_back(std::forward<Args>(args)...);`
`push_heap(c.begin(), c.end(), comp);`

```cpp
void pop()();
```

效果：
+ `pop_heap(c.begin(), c.end(), comp);`
`c.pop_back();`

## 23.6.4.4 priority_queue 特化算法

```cpp
template <class T, class Container, Compare>
void swp(priority_queue<T, Container, Compare>& x, noexcept(noexcept(x.swap(y)))
priority_queue<T, Container, Compare>& y);
```

效果：`x.swap(y);`

## 23.6.5 类模板 stack

任何支持 `back()`、`push_back()` 和 `pop_back()` 操作的序列都可以用于实例化 `stack`。特别是 `vector` (23.3.6)、`list` (23.3.5) 和 `deque` (23.3.3) 可以使用。

## 23.6.5.1 头文件 <stack> 概要

```cpp
#include <initializer_list>
namespace stack {
template <class T, class Container = deque<T>> class stack {
template <class T, class Container>
bool operator===(const stack<T, Container>& x, const stack<T, Container>& y);
template <class T, class Container>
bool operator<(const stack<T, Container>& x, const stack<T, Container>& y);
template <class T, class Container>
bool operator!=(const stack<T, Container>& x, const stack<T, Container>& y);
template <class T, class Container>
bool operator>=(const stack<T, Container>& x, const stack<T, Container>& y);
template <class T, class Container>
bool operator<=(const stack<T, Container>& x, const stack<T, Container>& y);
template <class T, class Container>
bool operator>=(const stack<T, Container>& x, const stack<T, Container>& y);
```

```cpp
template<class T, class Container>
bool operator<<(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
void swap(stack<T, Container>& x, stack<T, Container>& y) noexcept(x.swap(y));
}
```

## 23.6.5.2 stack 定义 [stack.defn]

```cpp
namespace std {
template<class T, class Container = deque<T>
class stack {
public:
typedef typename Container::value_type;
typedef typename Container::reference;
typedef typename Container::const_reference;
typedef typename Container::size_type;
typedef typename Container::container_type;
protected:
Container c;
public:
explicit stack(const Container&);
explicit stack();
template<class Alloc> explicit stack(const Alloc&);
template<class Alloc> stack(const Container&, const Alloc&);
template<class Alloc> stack(Container&&, const Alloc&);
template<class Alloc> stack(const stack&, const Alloc&);
template<class Alloc> stack(stack&&, const Alloc&);
bool empty() const { return c.empty(); }
size_type size() const { return c.size(); }
reference top() const { return c.back(); }
const_reference top() const { return c.back(); }
void push(value_type x) { c.push_back(x); }
void push(value_type&& x) { c.push_back(std::move(x)); }
template<class... Args> void emplace(Args&&... args) { c.emplace(std::forward<Args>(args)...); }
void pop() { c.pop_back(); }
void swap(stack& x, stack& y) noexcept(x.c.swap(y.c)) {
    x.c.swap(y.c);
}
}
}
template<class T, class Container>
bool operator==(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
bool operator<(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
bool operator!=(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
bool operator>(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
bool operator<=(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
bool operator>=(const stack<T, Container>& x, const stack<T, Container>& y);
template<class T, class Container>
void swap(stack<T, Container>& x, stack<T, Container>& y) noexcept(x.c.swap(y.c));
```

```cpp
template <class T, class Container, class Alloc>
struct uses_allocator<stack<T, Container>, Alloc>
  : uses_allocator<Container, Alloc>::type { };
```

## 23.6.5.3 stack 构造函数 [stack.cons]

+ `explicit stack(const Container& cont);`

效果：用 `cont` 初始化 `c`。

+ `explicit stack(Container&& cont = Container());`

效果：用 `std::move(cont)` 初始化 `c`。

## 23.6.5.4 带有分配器的 stack 构造函数 [stack.cons.alloc]

+ 如果 `uses_allocator<container_type, Alloc>::value` 为 `false`，则此子句不应参与重载解析。

+ `template <class Alloc>`

`explicit stack(const Alloc& a);`

效果：用 `a` 初始化 `c`。

+ `template <class Alloc>`

`stack(container_type&& const, const Alloc& a);`

效果：用 `const` 作为第一个参数、`a` 作为第二个参数初始化 `c`。

+ `template <class Alloc>`

`stack(container_type&& cont, const Alloc& a);`

效果：用 `std::move(cont)` 作为第一个参数、`a` 作为第二个参数初始化 `c`。

+ `template <class Alloc>`

`stack(const stack& s, const Alloc& a);`

效果：用 `s.c` 作为第一个参数、`a` 作为第二个参数初始化 `c`。

+ `template <class Alloc>`

`stack(stack&& s, const Alloc& a);`

效果：用 `std::move(s.c)` 作为第一个参数、`a` 作为第二个参数初始化 `c`。

# 24 迭代器库

## 24.1 通用

1 本节描述了 C++ 程序可能用于对容器进行迭代的组件（第 23 节、流 (27.7) 和流缓冲区 (27.6)）。

2 后子节描述了迭代器要求以及迭代器原语、预定义迭代器和流迭代器的组件，如表 104 所示。

表 104 — 迭代器库摘要

| 子节 | 头文件(s) | |
|---|---|---|
| 24.2 | 要求 | |
| 24.4 | 迭代器原语 | <iterator> |
| 24.5 | 预定义迭代器 | |
| 24.6 | 流迭代器 | |

## 2.2 迭代器要求

### 2.1 一般地

1 迭代器是指针的泛化，允许 C++ 程序以统一的方式处理不同的数据结构（容器）。为了能够构建在不同类型数据上正确且高效运行的模板算法，库不仅形式化了迭代器的接口，还形式化了其语义和复杂性假设。所有迭代器支持表达式 `*`，结果为 `a = o`，其中 `o` 是某种类型的值的迭代器的类型。所有输出迭代器支持表达式 `i = o`，其中 `o` 是某种类型的值的可写入 `i` 的特定迭代器类型。所有表达式 `(*i)==j` 定义良好的迭代器都支持表达式 `i!=j`。对于每个定义了相等性的迭代器类型 `i`，都有对应 `i` 的比较运算符。

2 由于迭代器是指针的抽象，它们的语义是 C++ 中大多数指针语义的泛化。这确保了每个接收迭代器的函数模板都能像普通指针一样工作。本国际标准根据在它们上定义的操作将迭代器分为五类：输入迭代器、前向迭代器、双向迭代器和随机访问迭代器，如表 105 所示。

表 105 — 迭代器类别之间的关系

| 随机访问 | 双向 | 前向 | 输入 |
|---|---|---|---|
| | | | 输出 |

3 前向迭代器满足输入迭代器的所有要求，并在指定输入迭代器时均可以使用；双向迭代器也满足前向迭代器的所有要求，并在指定前向迭代器时均可以使用；随机访问迭代器也满足双向迭代器的所有要求，并在指定双向迭代器时均可以使用。

4 进一步满足输出迭代器要求的迭代器称为可变迭代器（mutable iterators）。不可变迭代器称为常量迭代器（constant iterators）。

5 进一步满足以下要求的：对于整数值 `n` 和可解引用迭代器值 `a` 以及 `(a + n)`，`*(a + n)` 等于 `*address(*a + n)` 的迭代器被称为连续迭代器（contiguous iterators）。[注：例如，类型为连续迭代器，使用 `reverse_iterator<int>`。对于具有可解引用 `a` 的有效范围 `[a,b]`，指针表示的相应范围 `*address(*a),*address(*a + (b - a))` 可能不可解引用。——结束]
