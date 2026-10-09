
- 1 Effects: 构建一个空的 `unordered_set`，使用指定的哈希函数、键相等谓词和分配器，并使用 `n` 个桶。默认构造函数中，桶的数量由实现定义。`max_load_factor()` 返回 `1.0`。

## 22.5.6 构造函数

[unordered.set.cnstr]

```cpp
unordered_set() : unordered_set(size_type(see below)) {}
explicit unordered_set(size_t n,
const hasher& h = hasher(),
const key_eq& eq = key_equal(),
const allocator_type& a = allocator_type());
```

- 2 Complexity: `InputIterator()`

```cpp
template<class InputIterator>
unordered_set(InputIterator f, InputIterator l,
size_type n = see below,
const hasher& h = hasher(),
const key_eq& eq = key_equal(),
const allocator_type& a = allocator_type());
```

```cpp
unordered_set<initializer_list<value_type>> il,
    size_type n = see below;
    const hasher hf = hasher();
    const key_equal eql = key_equal();
    const allocator_type alloc = allocator_type();
```

影响：使用指定的哈希函数、等值谓词和分配器构造一个空的 `unordered_set`，并至少使用 `b` 个桶。如果没有提供，则桶的数量由实现定义。对于第一种形式，它从范围 `[first, last)` 插入元素；对于第二种形式，它从范围 `[il.begin(), il.end())` 插入元素。`max_load_factor()` 返回 `1.0`。

复杂度：平均情况为线性级，最坏情况为二次级。

## 22.5.6.3 删除 [unordered.set.erase]

```cpp
template<class K, class H, class P, class A, class Pred>
typename unordered_set<K, H, P, A>::size_type
erase(unordered_set<K, H, P, A>& c, Pred& pred);
```

影响：等价于：

```cpp
auto original_size = c.size();
for (auto i = c.begin(), last = c.end(); i != last; ) {
    if (pred(*i)) {
        i = c.erase(i);
    } else {
        i++;
    }
}
return original_size - c.size();
```

## 22.5.7 类模板 unordered_multiset [unordered.multiset]

### 22.5.7.1 概述

`unordered_multiset` 是一种关联容器，它支持元素（`unordered_set` 的实例）可能包含多个相同的键值副本，并且每个元素本身就是该键。`unordered_multiset` 支持前向迭代器。

`unordered_multiset` 满足容器、关联容器以及感知分配器容器的所有要求（表 76）。它提供了提供了上述要求中关于等值键的操作：即 `unordered_multiset` 在支持 `a_cmp` 操作外，还支持 `a_eq` 操作。对于 `unordered_multiset<Key>`，键值和类型都是 `Key`。迭代器和 `const_iterator` 类型都是常量迭代器。不确定它们是否为同一种类型。

22.5.7 仅描述了 `unordered_multiset` 上未在某个要求表中描述的操作，或者具有额外语义信息的操作。

```cpp
namespace std {
template<class Key,
    class Hash = hash<Key>,
    class Pred = equal_to<Key>,
    class Allocator = allocator<Key>>
class unordered_multiset {
public:
    // types
    using key_type = Key;
    using value_type = Key;
    using hasher = Hash;
    using key_equal = Pred;
    using allocator = Allocator;
    using allocator_type = typename allocator_traits<Allocator>::pointer;
    using pointer = typename allocator_traits<Allocator>::pointer;
    using const_pointer = typename allocator_traits<Allocator>::const_pointer;
    using reference = value_type&;
    using const_reference = const value_type&;
    using size_type = size_type;
    using difference_type = difference_type;
    implementation-defined; // see 22.9
    implementation-defined; // see 22.9
```

```cpp
using iterator = implementation-defined; // see 22.9
using const_iterator = implementation-defined; // see 22.9
using local_iterator = implementation-defined; // see 22.9
using const_local_iterator = implementation-defined; // see 22.9
using node_type = unspecified;
```

// 22.5.2, 构造/拷贝

```cpp
unordered_multiset();
explicit unordered_multiset(size_type n,
    const hasher& h = hasher(),
    const key_equal& eq = key_equal(),
    const allocator_type& a = allocator_type());
```

```cpp
template<class Iterator>
unordered_multiset(Iterator first, Iterator last,
    size_type n = 0,
    const hasher& h = hasher(),
    const key_equal& eq = key_equal(),
    const allocator_type& a = allocator_type());
unordered_multiset(const unordered_multiset& other);
 unordered_multiset(unordered_multiset&& other);
unordered_multiset(const unordered_multiset& other, const allocator_type& a);
unordered_multiset(unordered_multiset&& other, const allocator_type& a);
```

```
size_type bucket(const key_type& k) const;
local_iterator begin(size_type n);
const_local_iterator begin(size_type n) const;
local_iterator end(size_type n);
const_local_iterator end(size_type n) const;
const_local_iterator begin(size_type n) const;
const_local_iterator end(size_type n) const;

// hash 策略
float load_factor() const noexcept;
float max_load_factor() const noexcept;
void max_load_factor(float z);
void rehash(size_type n);
void reserve(size_type n);
template<class InputIterator>
    class Hash = hash<iter_value_type<InputIterator>>;
    class Pred = equal_to<iter_value_type<InputIterator>>;
    class Allocator = allocator<iter_value_type<InputIterator>>;
unordered_multiset(InputIterator, InputIterator, typename size_type = see_below,
    typename Hash = Hash(), Pred = Pred(), Allocator = Allocator())
    -> unordered_multiset<iter_value_type<InputIterator>>;
template<class T, class Hash = hash<T>>
    class Pred = equal_to<T>, Allocator = allocator<T>;
unordered_multiset(initializer_list<T>, typename size_type = see_below,
    typename Hash = Hash(), Pred = Pred(), Allocator = Allocator())
    -> unordered_multiset<T, Hash, Pred, Allocator>;
template<class InputIterator, class Allocator>
unordered_multiset(InputIterator, InputIterator, typename size_type = see_below, Allocator)
    -> unordered_multiset<iter_value_type<InputIterator>,
    hash<iter_value_type<InputIterator>>,
    equal_to<iter_value_type<InputIterator>>,
    Allocator>;
template<class InputIterator, class Hash, class Allocator>
unordered_multiset(InputIterator, InputIterator, typename size_type = see_below, Hash, Allocator)
    -> unordered_multiset<iter_value_type<InputIterator>, Hash,
    equal_to<iter_value_type<InputIterator>>,
    Allocator>;
template<class T, class Hash, class Allocator>
unordered_multiset(initializer_list<T>, typename size_type = size_type, Hash, Allocator)
    -> unordered_multiset<T, Hash, equal_to<T>, Allocator>;

// swap
template<class Key, class Hash, class Pred, class Alloc>
    void swap(unordered_multiset<Key, Hash, Pred, Alloc>& x,
    unordered_multiset<Key, Hash, Pred, Alloc>& y)
    noexcept(noexcept(x.swap(y)));
```

`unordered_multiset` 推导指南中使用的 `size_type` 参数指向推导指南所推导类型类型 `size_type` 成员。

## 22.5.7.2 构造函数

`unordered_multiset()` : `unordered_multiset(size_type see below)` {}

`explicit unordered_multiset(size_type n,`

```cpp
const hasher& h = hasher();
const key_eq eq = key_equal();
const allocator_type& a = allocator_type();
```

- 1 效果：使用指定的哈希函数、键相等谓词和分配器构造一个 `unordered_multiset`，并分配 `n` 个桶。对于默认构造函数，桶的数量由实现决定。`max_load_factor()` 返回 `1.0`。

- 2 复杂度：常数级。

```cpp
template<class Iterator>
unordered_multiset(Iterator f, Iterator l,
size_type n = see below,
const hasher& h = hasher();
const key_eq eq = key_equal();
const allocator_type& a = allocator_type();
unordered_multiset(iterator_list<value_type> it,
size_type n = see below,
const hasher& h = hasher();
const key_eq eq = key_equal();
const allocator_type& a = allocator_type());
```

- 3 效果：使用指定的哈希函数、键相等谓词和分配器并使用 `n` 个桶构造一个 `unordered_multiset`。如果 `n` 不是指定的，则桶的数量由实现决定。第一个从范围 `[f, l)` 复制元素，第二个则从范围 `[i.begin(), i.end())` 复制。`max_load_factor()` 返回 `1.0`。

- 4 复杂度：平均线性级，最坏情况二次方级。

## 22.5.7.3 删除

```cpp
template<class K, class H, class P, class A, class Predicate>
typename unordered_multiset<K, H, P, A>::size_type
erase(unordered_multiset<K, H, P, A>& e, const Predicate& pred);
```

- 1 效果：等同于：

```cpp
auto _original_size = c.size();
for (auto i = c.begin(); i != c.end(); ) {
  if (pred(*i)) {
    i = c.erase(i);
  } else {
    ++i;
  }
}
return _original_size;
```

## 22.6 容器适配器

头文件 `<queue>` 和 `<stack>` 定义了 `queue`、`priority_queue` 和 `stack`。

- 1 效果：`queue` 和 `priority_queue` 接受一个 `Container` 参数。

- 2 效果：`queue` 和 `priority_queue` 接受一个 `Container` 参数。

- 3 效果：`stack` 接受一个 `Container` 参数。

- 4 效果：除非满足任一条件，否则 `queue` 和 `priority_queue` 不参与重载：

### 22.6.1 <queue> 概要
