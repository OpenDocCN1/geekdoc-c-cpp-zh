

# ISO/IEC 14882:2017(E)

```cpp
template<class Iterator,
    class Compare = less<typename iterator_traits<Iterator>::value_type>,
    class Allocator = allocator<typename iterator_traits<Iterator>::value_type>>
multiset(Iterator, Iterator,
    Compare cmp = Compare(), Allocator alloc = Allocator())
    -> multiset<typename iterator_traits<Iterator>::value_type, Compare, Allocator>;
```

```cpp
template<class Key, class Compare = less<Key>, class Allocator = allocator<Key>>
multiset(initializer_list<Key> list, Compare cmp = Compare(), Allocator alloc = Allocator())
    -> multiset<Key, Compare, Allocator>;
```

```cpp
template<class Iterator, class Allocator>
multiset(Iterator, Iterator, Allocator)
    -> multiset<typename iterator_traits<Iterator>::value_type,
        less<typename iterator_traits<Iterator>::value_type>, Allocator>;
```

## 26.4.7.3 特殊化算法

```cpp
template<class Key, class Compare, class Allocator>
    void swap(multiset<Key, Compare, Allocator>& x,
        multiset<Key, Compare, Allocator>& y) noexcept(x.swap(y));
```

## 26.4.7.2 multiset 构造函数

[multiset.cons]

```cpp
explicit multiset(const Compare& comp, const Allocator& alloc = Allocator());
```

- **效果**：使用指定的比较对象和分配器构造一个空的 multiset。
- **复杂度**：常数级。

```cpp
template <class InputIterator>
multiset(InputIterator first, InputIterator last,
const Compare& comp = Compare(), const Allocator& alloc = Allocator());
```

- **效果**：使用指定的比较对象创建一个空的 multiset，并插入范围 [first, last) 范围元素。
- **复杂度**：如果范围 [first, last] 已经使用 comp 排序，则复杂度为相对于 N 的线性级；否则为 O(log N)，其中 N 为 last - first。

## 26.4.7 multiset 排序算法 [multiset.special]

```cpp
template <class Key, class Compare, class Allocator>
void swap(multiset<Key, Compare, Allocator>& x,
multiset<Key, Compare, Allocator>& y)
noexcept(noexcept(x.swap(y)));
```

- **效果**：等同于 x.swap(y)。

## 26.5 无序关联容器 [unordered.general]

### 26.5.1 通用

- 头文件 <unordered_map> 定义了类 unordered_map 和 unordered_multimap；头文件 <unordered_set> 定义了类 unordered_set 和 unordered_multiset。
- 在 26.4.1 中定义的、仅用于说明的别名模板 iter_key_t、iter_val_t 和 iter_alloc_t 可能会出现在无序容器的推导指南中。

### 26.5.2 头文件 <unordered_map> 概要 [unordered.map.syn]

```cpp
#include <initializer_list>
namespace std {
// 26.5.1. 类模板 unordered_map
template <class Key, class T,
class Hash = hash<Key>,
class Pred = equal_to<Key>,
class Alloc = allocator<pair<const Key, T>>
class unordered_map;
```

```cpp
// 26.5.5. 类模板 unordered_multimap
template <class Key, class T,
class Hash = hash<Key>,
class Pred = equal_to<Key>,
class Alloc = allocator<pair<const Key, T>>>
class unordered_multimap;
```

```cpp
template <class Key, class T, class Hash, class Pred, class Alloc>
void swap(unordered_map<Key, T, Hash, Pred, Alloc>& x,
unordered_map<Key, T, Hash, Pred, Alloc>& y)
noexcept(noexcept(x.swap(y)));
```

```cpp
template <class Key, class T, class Hash, class Pred, class Alloc>
void swap(unordered_multimap<Key, T, Hash, Pred, Alloc>& x,
unordered_multimap<Key, T, Hash, Pred, Alloc>& y)
noexcept(noexcept(x.swap(y)));
```

```cpp
template <class Key, class T, class Hash, class Pred, class Alloc>
bool operator=(const unordered_map<Key, T, Hash, Pred, Alloc>&& a,
                    const unordered_map<Key, T, Hash, Pred, Alloc>&& b);

template <class Key, class T, class Hash, class Pred, class Alloc>
bool operator!=(const unordered_map<Key, T, Hash, Pred, Alloc>&& a,
                    const unordered_map<Key, T, Hash, Pred, Alloc>&& b);

template <class Key, class T, class Hash, class Pred, class Alloc>
bool operator=(const unordered_multimap<Key, T, Hash, Pred, Alloc>&& a,
                    const unordered_multimap<Key, T, Hash, Pred, Alloc>&& b);

template <class Key, class T, class Hash, class Pred, class Alloc>
bool operator!=(const unordered_multimap<Key, T, Hash, Pred, Alloc>&& a,
                    const unordered_multimap<Key, T, Hash, Pred, Alloc>&& b);
```

```cpp
namespace pm {
    template <class Key, class T,
    class Hash = hash<Key>,
    class Pred = equal_to<Key>,
    class Alloc = allocator<pair<const Key, T>>>
    using unordered_map = std::unordered_map<Key, T, Hash, Pred, Alloc>;

    template <class Key, class T,
    class Hash = hash<Key>,
    class Pred = equal_to<Key>,
    class Alloc = allocator<pair<const Key, T>>>
    using unordered_multimap = std::unordered_multimap<Key, T, Hash, Pred, Alloc>;
}
```

