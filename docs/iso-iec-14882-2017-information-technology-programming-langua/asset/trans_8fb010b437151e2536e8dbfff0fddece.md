

# ISO/IEC 14882:2017(E)

```cpp
template<class K>
pair<const_iterator, const_iterator> equal_range(const K& x) const;
```

```cpp
template<class InputIterator,
    class Compare = less<typename iterator_traits<InputIterator>::value_type>,
    class Allocator = Allocator<typename iterator_traits<InputIterator>::value_type>>
    set(InputIterator it, Allocator alloc)
    Compare(const Compare = Compare(), Allocator alloc = Allocator())
    : set(typename iterator_traits<InputIterator>::value_type, it, alloc);
```

```cpp
template<class Key, class Compare = less<Key>, class Allocator = allocator<Key>>
    set(initializer_list<Key> init, const Compare& cmp = Compare(), const Allocator& alloc = Allocator())
    : set(init, cmp, alloc);
```

```cpp
template<class InputIterator, class Compare, class Allocator>
    set(InputIterator it, Allocator alloc)
    : set(typename iterator_traits<InputIterator>::value_type,
          typename iterator_traits<InputIterator>::value_type, it, alloc),
          alloc);
```

```cpp
template<class Key, class Compare = less<Key>, class Allocator = allocator<Key>>
    set(initializer_list<Key> init, Allocator alloc = Allocator())
    : set(init, less<Key>(), alloc);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator=(const Key& x, const Allocator& y) const
    : insertKey(x, Compare & y);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator<(const Key& x, const Allocator& y) const
    : insertKey(x, Compare & y);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator>(const Key& x, const Allocator& y) const
    : insertKey(x, Compare & y);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator==(const Key& x, const Allocator& y) const
    : insertKey(x, Compare & y);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator!=(const Key& x, const Allocator& y) const
    : insertKey(x, Compare & y);
```

```cpp
template<class Key, class Compare, class Allocator>
    bool operator<=(const Key& x, const Allocator& y) const
    : insertKey(x, Compare & y);
```

## 2.6.4.5. 特化算法

```cpp
template<class Key, class Compare, class Allocator>
    void swap(set<Key, Compare, Allocator>& x,
             set<Key, Compare, Allocator>& y)
    noexcept(x.swap(y));
```

## 2.6.4.2. set 构造函数、拷贝与赋值 [cons]

```cpp
explicit set(const Compare& cmp, const Allocator& alloc);
```

- 效果：使用指定的比较对象和分配器构造一个空 set。
- 复杂度：常时间级。

```cpp
template <class InputIterator>
set(InputIterator first, InputIterator last,
 const Compare& comp = Compare(), const Allocator& alloc = Allocator());
```

- 效果：使用指定的比较对象和分配器创建一个空 set，并插入范围 [first, last) 中的的元素。
- 复杂度：如果范围 [first, last] 已经使用 comp 排序，则复杂度为 N 的线性时间；否则为 log N 时间，其中 N 为 last - first。

## 2.6.4.3. set 特化算法 [set.special]

```cpp
template<class Key, class Compare, class Allocator>
void swap(set<Key, Compare, Allocator>& x, set<Key, Compare, Allocator>& y)
 noexcept(noexcept(x.swap(y)));
```

- 效果：类似于 x.swap(y)。

## 2.4.7. multiset 类 [multiset.overload]

### 2.4.7.1. multiset 迭代器

- multiset 是一种支持键（可能包含多个相同的值）并提供元素检索关联容器。multiset 支持双向迭代器。
- multiset 满足可逆容器 (2.2)、关联容器 (2.6) 以及分配器容器 (8) 的要求。multiset 还提供了 2.6 中的大多数操作，以支持重复键。对于 multiset<Key>，key_type 和 value_type 的描述仅在这些表中描述的操作中提供。

```cpp
explicit multiset(const Compare& comp, const Allocator& alloc);
template <class Iterator>
multiset(InputIterator first, InputIterator last,
    const Compare& comp = Compare(),
    const Allocator& alloc = Allocator());
multiset(const Compare& comp);
multiset(multiset& x);
explicit multiset(const Allocator& alloc);
multiset(const multiset& x, const Allocator& alloc);
multiset(const multiset& x, const Allocator& alloc);
multiset(initializer_list<value_type> it, const Compare& comp = Compare(),
    const Allocator& alloc = Allocator());
template <class Iterator>
multiset(InputIterator first, InputIterator last, const Allocator& alloc)
    : multiset(first, last, Compare(), alloc)
multiset(initializer_list<value_type> il, const Allocator& alloc)
    : multiset(il, Compare(), alloc)
multiset& operator=(const Compare& x);
multiset& operator=(const multiset& x)
noexcept(allocator_traits<Allocator>::is_always_equal::value &&
    is_move_assignable<Compare>);
multiset& operator=(initializer_list<value_type>);
allocator_type get_allocator() const noexcept;
```

// 迭代器：

```cpp
const_iterator begin() const noexcept;
const_iterator begin() const noexcept;
const_iterator end() const noexcept;
const_iterator end() const noexcept;
```

// 反向迭代器：

```cpp
reverse_iterator begin() const noexcept;
const_reverse_iterator begin() const noexcept;
reverse_iterator end() const noexcept;
const_reverse_iterator end() const noexcept;
```

// 容量：

```cpp
const_iterator begin() const noexcept;
const_iterator end() const noexcept;
const_reverse_iterator begin() const noexcept;
const_reverse_iterator end() const noexcept;
```

// 修改器：

```cpp
bool empty() const noexcept;
size_type size(size_type) const noexcept;
size_type max_size(size_type) const noexcept;
```

```cpp
template <class... Args> iterator emplace(Args& args, Args&&... args);
template <class... Args> iterator emplace(const_iterator position, Args&&... args);
iterator insert(const multiset& x);
iterator insert(value_type&& x);
iterator insert(const_iterator position, const value_type& x);
iterator insert(const_iterator position, value_type&& x);
template <class Iterator>
void insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type> value_type);
```

```cpp
node_type extract(const_iterator position);
node_type extract(const key_type&& x);
iterator insert(const_iterator hint, node_type&& nh);
```

```cpp
iterator erase(iterator position);
iterator erase(const_iterator position);
size_type erase(const key_type& x);
iterator erase(const_iterator first, const_iterator last);
void
noexcept(allocator_traits<Allocator>::is_always_equal::value &&
is_nothrow_isswappable<Compare>);
void
clear() noexcept;
```

```cpp
template<class C2>
void merge(multiset<Key, C2, Allocator>&& source);
template<class C2>
void merge(multiset<Key, C2, Allocator>&& source);
template<class C2>
void merge(set<Key, C2, Allocator>&& source);
template<class C2>
void merge(set<Key, C2, Allocator>&& source);
```

```cpp
// 观察者
key_type key_comp() const;
compare value_comp() const;
```

```cpp
// set 操作：
iterator find(const key_type& x);
const_iterator find(const key_type& x) const;
template<class K> iterator find(const K& x);
template<class K> const_iterator find(const K& x) const;
```

```cpp
size_type count(const key_type& x) const;
template<class K> size_type count(const K& x) const;
```

```cpp
iterator lower_bound(const key_type& x);
const_iterator lower_bound(const key_type& x) const;
template<class K> iterator lower_bound(const K& x) const;
template<class K> const_iterator lower_bound(const K& x) const;
```

```cpp
iterator upper_bound(const key_type& x);
const_iterator upper_bound(const key_type& x) const;
template<class K> iterator upper_bound(const K& x) const;
template<class K> const_iterator upper_bound(const K& x) const;
```

```cpp
pair<iterator, iterator> equal_range(const key_type& x);
pair<const_iterator, const_iterator> equal_range(const key_type& x) const;
```

