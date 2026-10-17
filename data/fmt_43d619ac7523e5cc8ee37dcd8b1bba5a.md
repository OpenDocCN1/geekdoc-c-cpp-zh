
```cpp
bool operator>=(const mapKey<T,Compare,Allocator>& x,
           const mapKey<T,Compare,Allocator>& y);

template <class Key, class T, class Compare, class Allocator>
void swap(mapKey<T,Compare,Allocator>& x)
           noexcept(noexcept(x.swap(y)));
```

### 23.4.3 Header <set> 摘要 [associative.set.syn]

```cpp
#include <initializer_list>

namespace std {

template <class Key, class Compare = less<Key>,
class Allocator = allocator<Key>
class set:

  template <class Key, class Compare, class Allocator>
    bool operator+=(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator<(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator>=(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator<=(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator>(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator<=(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator>=(const set<Key,Compare,Allocator>& x,
           const set<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    void swap(set<Key,Compare,Allocator>& x,
           set<Key,Compare,Allocator>& y)
    noexcept(noexcept(x.swap(y)));

template <class Key, class Compare = less<Key>>
class multiset:

  template <class Key, class Compare, class Allocator>
    bool operator<=(multiset<Key,Compare,Allocator>& x,
           const multiset<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator>(multiset<Key,Compare,Allocator>& x,
           const multiset<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator!=(multiset<Key,Compare,Allocator>& x,
           const multiset<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator==(multiset<Key,Compare,Allocator>& x,
           const multiset<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
  template <class Key, class Compare, class Allocator>
    bool operator<=(multiset<Key,Compare,Allocator>& x,
           const multiset<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    bool operator>=(multiset<Key,Compare,Allocator>& x,
           const multiset<Key,Compare,Allocator>& y);

  template <class Key, class Compare, class Allocator>
    void swap(multiset<Key,Compare,Allocator>& x,
           multiset<Key,Compare,Allocator>& y)
    noexcept(noexcept(x.swap(y)));
```

## 23.4.4 类模板 map

### 23.4.1 类 map 概述

- `[map]` `map` 是一种关联容器，支持唯一键（每个值对应一个键），并根据键快速检索任何类型 `T` 的值。`map` 支持双向迭代器。
- `map` 满足可逆容器 (23.2)、关联容器 (23.4) 以及感知分配器的容器 (表 99) 的所有要求。`map` 还提供了针对唯一键的操作 (23.2.4)。此 `map` 支持唯一键 (23.2.4)，不支持相等操作。对于 `map<Key,T>`，`key_type` 是 `Key`，`value_type` 是 `pair<Key,T>`。此处提供了未在表中描述的 `map` 操作，或具有额外语义信息的操作。

```cpp
namespace std {

template<class Key, class T, class Compare = less<Key>,
class Allocator = allocator<pair<const Key, T>>>
class map {
public:
// types:
  typedef Key key_type;
  typedef T mapped_type;
  typedef pair<const Key, T> value_type;
  typedef Compare key_compare;
  typedef Allocator allocator_type;
  typedef value_type& reference;
  typedef const value_type& const_reference;
  typedef implementation-defined iterator; // sec 23.2
  typedef implementation-defined const_iterator; // sec 23.2
  typedef implementation-defined size_type; // sec 23.2
  typedef difference_type; // sec 23.2
  typedef allocator_traits<Allocator>::pointer pointer;
  typedef allocator_traits<Allocator>::const_pointer const_pointer;
  typedef std::reverse_iterator<iterator> reverse_iterator;
  typedef std::reverse_iterator<iterator> const_iterator;

class value_compare {
    friend class compare;
protected:
    Compare comp;
    value_compare(Compare c) : comp(c) {}
public:
    typedef bool result_type;
    typedef value_type first_argument;
    typedef value_type second_argument;
    bool operator()(const value_type& x, const value_type& y) const {
        return comp(x.first(), y.first());
    }
};
```

```cpp
// 23.4.4.2. construct() from/copy:
map() : map(Compare())
    explicit map(const Compare& comp,
             const Allocator& alloc = Allocator());
template<class InputIterator>
    map(InputIterator first, InputIterator last,
        const Compare& comp = Compare(), const Allocator& alloc = Allocator());
    map(const map& x);
    map(map& x);
    explicit map(const map& map, const Allocator& alloc);
    map(const map& map, const Allocator& alloc);
    map(initializer_list<pair<const Key, value_type>> init,
        const Compare& comp = Compare(),
        const Allocator& alloc = Allocator());
template<class InputIterator>
    map(InputIterator first, InputIterator last, const Allocator& a)
        : map(first, last, Compare(), a) {}
    map(initializer_list<value_type> il, const Allocator& a)
        : map(il, Compare(), a);
    ~map();
    map operator=(const map& x);
    map operator=(map& x)
        noexcept(allocator_traits<Allocator>::is_always_equal::value &&
```

is_nothrow_move_assignable<Compare>::value;
map& operator=(initializer_list<value_type>);
allocator_type get_allocator() const noexcept;
```

```cpp
// 迭代器:
iterator begin() noexcept;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator end() const noexcept;
```

```cpp
reverse_iterator rbegin() const noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() const noexcept;
const_reverse_iterator rend() const noexcept;
```

```cpp
const_iterator begin() const noexcept;
const_iterator end() const noexcept;
const_reverse_iterator crbegin() const noexcept;
const_reverse_iterator crend() const noexcept;
```

```cpp
// 容量:
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
```

### 23.4.3. 访问:

```cpp
T& operator[](const key_type& x);
T& operator*(const key_type& x);
T& at(const key_type& x);
```

### 23.4.4. 修改器:

```cpp
template<class... Args> pair_iterator(Args&... args);
template<class... Args> iterator insert_hint(const_iterator position, Args&... args);
pair_iterator, bool insert(const value_type& x);
pair_iterator, bool insert(value_type& x);
template<class P>
pair_iterator, bool insert(const P& x);
iterator insert(const_iterator position, const value_type& x);
iterator insert(const_iterator position, value_type& x);
template<class P>
iterator insert(const_iterator position, const P& x);
template<class InputIterator>
void insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type>);
```

```cpp
template<class... Args>
pair_iterator, bool try_emplace(const key_type& x, Args&... args);
template<class... Args>
iterator try_emplace(const_iterator hint, const key_type& x, Args&... args);
template<class M>
pair_iterator, bool insert_or_assign(const key_type& x, M& obj);
```

```cpp
template <class M>
pair<iterator, bool> insert_or_assign(key_type&& k, M& obj);
template <class M>
iterator insert_or_assign(const_iterator hint, const key_type& k, M& obj);
iterator erase(const_iterator position);
size_type erase(const key_type&& x);
iterator erase(const_iterator first, const_iterator last);
void swap(swap);
noexcept(allocator_traits<Allocator>::is_always_equal &&
```
