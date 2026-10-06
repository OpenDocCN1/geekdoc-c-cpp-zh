

# ISO/IEC 14882:2017(E)

```cpp
template<class Iterator, class Allocator>
unordered_multiset(unordered_multiset<typename Iterator, typename see below::size_type, Allocator>
    -> unordered_multiset<typename iterator_traits<Iterator>::value_type,
	hash<typename iterator_traits<Iterator>::value_type>,
	equal<typename iterator_traits<Iterator>::value_type>,
	Allocator>
);
```

```cpp
template<class Iterator, class Hash, class Allocator>
unordered_multiset(InputIterator, InputIterator, typename see below::size_type,
	hash, Allocator)
    -> unordered_multiset<typename iterator_traits<Iterator>::value_type, Hash,
	equal<typename iterator_traits<Iterator>::value_type>,
	Allocator>
);
```

```cpp
template<class T, class Allocator>
unordered_multiset(unordered_multiset<T, typename see below::size_type, Allocator>
    -> unordered_multiset<T, Hash, equal<T>, Allocator>
```

```cpp
template<class T, class Hash, class Allocator>
unordered_multiset(unordered_multiset<T, typename see below::size_type, Hash, Allocator>
    -> unordered_multiset<T, Hash, equal<T>, Allocator>
```

```cpp
template<class Key, class Hash, class Pred, class Allocator>
bool operator=(const unordered_multiset<Key, Hash, Pred, Allocator>& a,
	const unordered_multiset<Key, Hash, Pred, Allocator>& b);
```

```cpp
// 26.5.7.3 swap
template<class Key, class Hash, class Pred, class Allocator>
void swap(unordered_multiset<Key, Hash, Pred, Allocator>& x,
	unordered_multiset<Key, Hash, Pred, Allocator>& y)
noexcept(noexcept(x.swap(y)));
```

- 4 `unordered_multiset` 推导中的 `size_type` 参数类型指的是主 `unordered_multiset` 模板的 `size_type` 成员类型。

- 26.5.7.2 `unordered_multiset()` 构造函数

```cpp
unordered_multiset() : unordered_multiset(size_type see below) { {}
explicit unordered_multiset(size_type n = 0,
	hash const hf = hasher();
	const key_equal eql = equal();
	const allocator_type& a = allocator_type(););
```

- 1 影响：使用指定的哈希函数、键等值谓词和分配器使用 `n` 个桶构造一个空的 `unordered_multiset`。对于默认构造函数，桶的数量由实现定义。`max_load_factor()` 返回 1。

- 2 复杂度：常数级。

```cpp
template <class InputIterator>
unordered_multiset(InputIterator f, InputIterator l,
    size_type n = see below,
    const hash& h = hasher(),
    const key_equal eq = key_equal(),
    const allocator& alloc = allocator<value_type>),
unordered_multiset(initializer_list<
    size_type n = see below,
    const hash& h = hasher(),
    const key_equal eq = key_equal(),
    const allocator& alloc = allocator<value_type>())
```

影响：使用指定的哈希函数、键等值谓词和分配器构造一个包含至少 `n` 个桶的 `unordered_multiset`。如果没有提供 `n`，则桶的数量由实现定义。第一形式从范围 `[f, l)` 插入元素，第二种形式从范围 `[il.begin(), il.end())` 插入元素。返回 `n`。

复杂度：平均线性，最坏情况二方级。

# 26.5.7.3 unordered_multiset

```cpp
[unord.multiset.swap]
template <class Key, class Hash, class Pred, class Alloc>
void swap(unordered_multiset<Key, Hash, Pred, Alloc>& x,
    unordered_multiset<Key, Hash, Pred, Alloc>& y) noexcept(x.swap(y));
```

影响：同于 `x.swap(y)`。

# 26.6 容器适配器中

```cpp
[container.adaptors]
```

头文件 `queue` 和 `stack` 包含了容器适配器 `queue`、`priority_queue` 和 `stack`。

容器适配器接受一个 `Container` 模板参数，每个构造函数都接受一个 `Container` 引用参数。该参数被拷贝到每个适配器的 `Container` 成员中。如果容器接受分配器，则可以在适配器的构造函数中传递一个兼容的分配器。否则，对容器参数使用普通类型或不进行构造。容器适配器的第一个模板参数 `T` 应当是与 `Container::value_type` 相同的类型。

对于容器适配器，没有一个 `swap` 函数会抛出异常，除非该异常是由适配器的 `Container` 或 `Object`（如果有的话）的 `swap` 抛出的。

如果满足以下任一条件，容器适配器的推导指南将不参与重载解析：

- (4.1) 它有一个 `InputIterator` 参数且该类型不符合迭代器限定。
- (4.2) 它有一个 `Compare` 参数且该类型符合分配器推导。
- (4.3) 它有一个 `Container` 参数且该类型符合分配器推导。
- (4.4) 它有一个 `Allocator` 参数且该类型不符合分配器推导。
- (4.5) 它同时拥有 `Container` 和 `Allocator` 参数，且分配器推导为假。

- 26.6.2 Header <queue>

```cpp
#include <initializer_list>
namespace std {
    template <class T, class Container = deque<T>>
    class queue;
    template <class T, class Compare = less<typename T>>
    class priority_queue;
...（此处省略重复内容以保持逻辑一致）...
```

- 26.6.3 Header <stack>

```cpp
#include <initializer_list>
namespace std {
    template <class T, class Container = deque<T>>
    class stack;
...（此处省略重复内容以保持逻辑一致）...
```

- 26.6.4 类模板 queue

# 26.6.4.1 序列容器操作 `front()`、`back()`、`push_back()` 和 `pop_front()` 都可以用于实例化 `queue`。特别是 `list` (26.3.10) 和 `deque` (26.3.8) 可以使用。

```cpp
namespace std {
template<class T, class Container = deque<T>>
class queue {
...（此处省略重复内容以保持逻辑一致）...
```

