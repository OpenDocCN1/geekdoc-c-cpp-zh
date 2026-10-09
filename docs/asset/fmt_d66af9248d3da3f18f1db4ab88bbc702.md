
### `vector<bool>` 成员

```cpp
const_iterator cbegin() noexcept;
const_iterator const() noexcept;
const_reverse_iterator crbegin() noexcept;
const_reverse_iterator cred() noexcept;
```

#### 容量

```cpp
[[nodiscard]] bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
size_type capacity() const noexcept;
void resize(size_type sz, bool c = false);
void reserve(size_type n);
void shrink_to_fit();
```

#### 元素访问

```cpp
reference operator[](size_type n);
const_reference operator[](size_type n) const;
[[nodiscard]] const_reference at(size_type n) const;
[[nodiscard]] reference at(size_type n);
reference front();
const_reference front() const;
reference back();
const_reference back() const;
```

#### 修改器

```cpp
template<class Args...>
reference emplace_back(Args&&... args);
void push_back(const bool x);
void pop_back();
template<class Args...>
iterator emplace_insert(const_iterator position, Args&&... args);
iterator insert(const_iterator position, const bool x);
iterator insert(const_iterator position, size_type n, const bool x);
template<class Class>
iterator insert(const_iterator position, initializer_list<bool> il);
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);
void flip(reference& x, reference& y) noexcept;
void flip() noexcept; // 翻转所有位
void clear() noexcept;
allocator_type get_allocator() const noexcept;
```;
// namespace std

- 2 除非满足以下操作，否则所有操作与主 `vector` 模板具有相同的语义和性能，即处理 `bool` 值类型的操作映射到容器存储中的位值，且 `allocator_traits::construct` 不用于构造这些值。
- 3 不要求数据必须存储为连续的 `bool` 值分配。建议使用空间优化的 `bool` 表示，除非

`reference` 是一个模拟 `vector<bool>` 中单比特行为的类。转换函数在位被设置时返回 `true`，否则返回 `false`。赋值运算符在参数 `convert(to)` 为 `true` 时设置该位，否则清除它。`flip` 反转位的状态。

```cpp
constexpr flip() noexcept;
```

5 效果：将容器中的每个元素替换为其补码。

```cpp
constexpr static void swap(reference x, reference y) noexcept;
```

6 效果：交换 `x` 和 `y` 的内容，如下：

```cpp
bool b = x;
x = y;
y = b;
```

```cpp
template<class Allocator> struct hash<vector<bool, Allocator>>;
```

7 该特化已启用（20.14.9）。

## 22.4 关联容器

### 22.4.1 通用说明

1 头文件 `<map>` 定义了类 `map` 和 `multimap`；头文件 `<set>` 定义了类 `set` 和 `multiset`。

2 以下仅用于说明的迭代器可能出现在关联容器的文档指南中：

```cpp
template<class Iterator>
using value_type = 
  typename iterator_traits<Iterator>::value_type; // 仅说明

template<class Iterator>
using key_type = 
  typename remove_const_t<typename iterator_traits<Iterator>::value_type>::first_type; // 仅说明

template<class Iterator>
using mapped_type = 
  typename iterator_traits<Iterator>::value_type>::second_type; // 仅说明

template<class Iterator>
using iter_to_allocator = pair<
  typename iterator_traits<Iterator>::value_type>::first_type,
  add_const_t<typename iterator_traits<Iterator>::value_type>::first_type>
  typename iterator_traits<Iterator>::value_type>::second_type>; // 仅说明
```

### 22.4.2 `<map>` 特化

```cpp
#include <compare> // 17.11.1
#include <initial_list> // 17.10.2
```

```cpp
namespace std {
  // 22.14. 类模板 map
  template<class Key, class T, class Compare = less<Key>
  class Allocator = allocator<pair<const Key, T>>
  class map {
    template<class Key, class T, class Compare, class Allocator = Allocator>
    bool operator=(const map<Key, T, Compare, Allocator>& x,
                   const map<Key, T, Compare, Allocator>& y);
    template<class Key, class T, class Compare, class Allocator = Allocator>
    synth_three_way_result<pair<const Key, T>>
    operator<=>(const map<Key, T, Compare, Allocator>& x,
               const map<Key, T, Compare, Allocator>& y);
    template<class Key, class T, class Compare, class Allocator = Allocator>
    void swap(map<Key, T, Compare, Allocator>& x,
             map<Key, T, Compare, Allocator>& y)
    noexcept(noexcept(x.swap(y)));
```

```cpp
template<class Key, class T, class Compare, class Allocator, class Predicate>
typename map<Key, T, Compare, Allocator>::size_type
erase_if(map<Key, T, Compare, Allocator>& c, Predicate pred);
```

```cpp
// 22.4.5, 类模板
template<class Key, class T, class Compare = less<Key>
class Allocator = allocator<pair<const Key, T>>>
class map:
    template<class Key, class T, class Compare, class Allocator>
    bool operator=(const map<Key, T, Compare, Allocator>& x,
                   const map<Key, T, Compare, Allocator>& y);
    synth_three_way_result<iterator<const Key&>>
    operator<==(const map<Key, T, Compare, Allocator>& x,
                const map<Key, T, Compare, Allocator>& y);
```

```cpp
template<class Key, class T, class Compare, class Allocator>
void swap(map<Key, T, Compare, Allocator>& x,
         map<Key, T, Compare, Allocator>& y)
noexcept(noexcept(x.swap(y)));
```

```cpp
template<class Key, class T, class Compare, class Allocator>
typename map<Key, T, Compare, Allocator>::size_type
erase_if(map<Key, T, Compare, Allocator>& c, Predicate pred);
```

```cpp
namespace pmr {
    template<class Key, class T, class Compare = less<Key>>
    using map = std::map<Key, T, Compare,
                polymorphic_allocator<pair<const Key, T>>>;
```

```cpp
template<class Key, class T, class Compare = less<Key>>
using map = std::map<Key, T, Compare,
            polymorphic_allocator<pair<const Key, T>>>;
```

### 22.4.3 头文件 `<compare>` 概要

```cpp
#include <compare>    // 21.17.1
#include <initializer_list>  // 21.10.2
```

```cpp
namespace std {
    // 22.1.6, 类模板
template<class Key, class T, class Compare = less<Key>, class Allocator = allocator<Key>>
class set:
    template<class Key, class Compare, class Allocator>
    bool operator=(const set<Key, Compare, Allocator>& x,
                   const set<Key, Compare, Allocator>& y);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator=(const set<Key, Compare, Allocator>& x,
                   const set<Key, Compare, Allocator>& y);
    template<class Key, class Compare, class Allocator>
    synth_three_way_result<iterator<const Key&>>
    operator<==(const set<Key, Compare, Allocator>& x,
                const set<Key, Compare, Allocator>& y);
```

```cpp
template<class Key, class Compare, class Allocator>
void swap(set<Key, Compare, Allocator>& x,
noexcept(noexcept(x.swap(y)));
```

```cpp
template<class Key, class Compare, class Allocator, class Predicate>
typename set<Key, Compare, Allocator>::size_type
erase_if(set<Key, Compare, Allocator>& c, Predicate pred);
```

```cpp
// 22.4.7. 类 multiset
template<class Key, class Compare = less<Key>, class Allocator = allocator<Key>>
class multiset;
template<class Key, class Compare, class Allocator>
bool operator==(multiset<Key, Compare, Allocator>& x,
                const multiset<Key, Compare, Allocator>& y);
template<class Key, class Compare, class Allocator>
synth_three_way_result<iterator<const Key&>>
operator<==(multiset<Key, Compare, Allocator>& x,
            const multiset<Key, Compare, Allocator>& y);
template<class Key, class Compare, class Allocator>
void swap(multiset<Key, Compare, Allocator>& x,
           multiset<Key, Compare, Allocator>& y)
noexcept(noexcept(x.swap(y)));
template<class Key, class Compare, class Allocator, class Predicate>
typename multiset<Key, Compare, Allocator>::size_type
erase_if(multiset<Key, Compare, Allocator>& c, Predicate pred);
namespace pmr {
    template<class Key, class Compare = less<Key>>
    using set = std::set<Key, Compare, polymorphic_allocator<pair<const Key, typename T>>>;
    template<class Key, class Compare = less<Key>>
    using multiset = std::multiset<Key, Compare, polymorphic_allocator<pair<const Key, typename T>>>;
}
```

## 22.4.4 类模板

### 1 概述

`map` 是一种支持唯一键（每个键最多一个）并根据键快速检索值 `T` 的关联容器。`map` 支持双向迭代器。它满足容器、可逆容器（22.2）、关联容器（22.6）以及感知分配器的容器（7）的要求。`map` 还提供了 22.2 中描述的方法。这意味着 `map` 满足 22.6 中的唯一操作，但不满足相等操作。对于 `map<Key, T>`，`key_type` 和 `value_type` 是 `pair<const Key, T>`。此处描述仅针对这些表中未定义的操作或额外的语义信息提供。
