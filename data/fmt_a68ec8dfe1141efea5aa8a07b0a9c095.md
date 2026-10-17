
## 22.5.4 类 `unordered_map` [unord.map]

### 22.5.4.1 概述 [unord.map.overview]

`unordered_map` 是一种无序关联容器，它支持唯一键（一个 `unordered_map` 容器中每个键最多包含一个）以及与这些键映射的另一种类型 `mapped_type` 的值。`unordered_map` 类支持前向迭代器。

`unordered_map` 满足容器、无序关联容器以及感知分配器的容器的所有要求（见表 76）。它提供了前述要求中描述的、针对唯一键的各种操作；即，`unordered_map` 支持该表中的 `a_uniq` 操作，而不支持 `a_eq`。对于 `unordered_map<Key, T>`，键类型为 `Key`，映射类型为 `T`，值类型为 `pair-const<Key, T>`。

- 22.5.4 仅描述了 `unordered_map` 上那些未在要求列表中被描述的操作，或者具有额外语义信息的操作。

```cpp
namespace std {

  template<class Key,

            class T,

            class Hash = hash<Key>,

            class Pred = equal_to<Key>,

            class Allocator = allocator<pair<const Key, T>>>

class unordered_map {

:

    using key_type = Key;

    using mapped_type = T;

    using value_type = pair-const<Key, T>;

    using hasher_type = Hash;

    using pred_type = Pred;

    using allocator_type = Allocator;

    using pointer = typename allocator_traits<Allocator>::pointer;

    using const_pointer = typename allocator_traits<Allocator>::const_pointer;

    using reference = value_type&;

    using const_reference = const_type&; // 22.9

    using size_type = implementation-defined; // 22.9

    using difference_type = implementation-defined; // 22.9

    using iterator = implementation-defined; // 22.9

    using const_iterator = implementation-defined; // 22.9

    using local_iterator = implementation-defined; // 22.9

    using insert_local_iterator = implementation-defined; // 22.9

    using node_type = unspecified;

    using insert_return_type = insert-type<iterator, node_type>;

}
```

```cpp
// 22.5.4.2 构造/拷贝/析构
unordered_map();
explicit unordered_map(size_type n,
                       const hash& h = hash(),
                       const key_equal& eql = key_equal(),
                       const allocator_type& a = allocator_type());
```

```cpp
template<class Iterator, Iterator L1>
  unordered_map(size_type n =
                const                & h = h =
(),
                const key_equal =_ = key_equal(),
                type_type = a_type_
```

```cpp
unordered_map(const unordered_map& map);
unordered_map(unordered_map& map);
explicit unordered_map(const Allocator& alloc);
unordered_map(const unordered_map& map, const Allocator& alloc);
unordered_map(unordered_map& map, const Allocator& alloc,
    initializer_list<value_type> il,
    size_type n =
    const hasher& hf = hasher(),
    const key_equal& eq = key_eq(),
    const allocator_type& a = allocator_type());
unordered_map(size_type n, const allocator_type& a)
    unordered_map(n, const hasher& hf, const allocator_type& a)
    unordered_map(n, const key_equal& eq, a);
template<class InputIterator>
unordered_map(InputIterator it1, InputIterator it2, size_type n, const allocator_type& a)
    unordered_map(it1, it2, n, hasher(), key_eq());
template<class InputIterator>
unordered_map(InputIterator it1, InputIterator it2, size_type n, const hasher& hf,
    const allocator_type& a)
    unordered_map(it1, it2, n, hf, a);
unordered_map(initializer_list<value_type> il, size_type n, const allocator_type& a)
    unordered_map(il, n, hasher(), key_eq());
unordered_map(initializer_list<value_type> il, size_type n, const hasher& hf,
    const allocator_type& a)
    unordered_map(il, n, hf, a);
unordered_map::operator=(const unordered_map& map);
unordered_map::operator=(unordered_map& map);
noexcept(allocator_traits<Allocator>::is_always_equal<value_type> &&
    is_swappable<HashPred>>)
unordered_map::operator=(initializer_list<value_type>&&);
allocator_type get_allocator() const noexcept;
```

```cpp
// 迭代器
iterator begin() noexcept;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator end() const noexcept;
const_iterator c() const noexcept;
```

```cpp
// 容量
[[nodiscard]] bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
```

```cpp
// 22.5.4. 修改器
template<class... Args> pair<iterator, bool> emplace(const_iterator position, Args... args);
template<class... Args> Args insert(const_iterator position, Args... args);
pair<iterator, bool> insert(const_iterator hint, const value_type& obj);
template<class P> size_type insert(iterator hint, P&& obj);
iterator insert(const_iterator hint, const value_type& obj);
template<class P> size_type insert(const_iterator hint, P&& obj);
template<class InputIterator> void insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type> il);
```

```cpp
node_type extract(const_iterator position);
node_type extract(const key_type& k);
insert_return_type extract(node_type&& hf);
iterator insert(const_iterator hint, const node_type& hf);
```

```cpp
template<class... Args> pair<iterator, bool> try_emplace(const key_type& k, Args... args);
template<class... Args> pair<iterator, bool> try_emplace(const key_type&& k, Args... args);
template<class... Args> iterator try_emplace(const_iterator hint, const key_type& k, Args... args);
template<class... Args> iterator try_emplace(const_iterator hint, const key_type&& k, Args... args);
template<class M> pair<iterator, bool> insert_assign(const key_type& k, M& obj);
template<class M> pair<iterator, bool> insert_assign(const key_type&& k, M&& obj);
template<class M> iterator insert_assign(const_iterator hint, const key_type& k, M& obj);
template<class M> iterator insert_assign(const_iterator hint, const key_type&& k, M&& obj);
```

```cpp
iterator erase(const_iterator position);
iterator erase(const_iterator position);
size_type erase(const key_type& k);
iterator erase(const_iterator first, const_iterator last);
void swap(unordered_map&);
noexcept(allocator_traits<Allocator>::is_always_equal<value_type> &&
    is_swappable<HashPred>)
void clear() noexcept;
```

```cpp
template<class H2, class P2> void merge(unordered_map<Key, T, H2, P2>&& source);
template<class H2, class P2> merge(unordered_map<Key, T, H2, P2>&& source);
template<class H2, class P2> merge(unordered_multimap<Key, T, H2, P2, Allocator>&& source);
template<class H2, class P2> merge(unordered_multimap<Key, T, H2, P2, Allocator>&& source);
```

```cpp
// 观察器
size_type size() const;
size_type max_size() const;
bool empty() const noexcept;
```

```cpp
// map 操作
iterator find(const key_type& k);
const_iterator find(const key_type& k) const;
template<class K> iterator find(const K& k) const;
template<class K> const_iterator find(const K& k) const;
size_type count(const key_type& k);
template<class K> size_type count(const K& k) const;
bool contains(const key_type& k);
template<class K> bool contains(const K& k) const;
pair<iterator, iterator> equal_range(const key_type& k);
template<class K> pair<const_iterator, const_iterator> equal_range(const K_type k) const;
template<class K> pair<iterator, iterator> equal_range(const K& k);
template<class K> pair<const_iterator, const_iterator> equal_range(const K& k) const;
```

### 22.5.4.3 元素访问

```cpp
mapped_type& operator[](const key_type& k);
mapped_type& operator[](const key_type&& k);
```

# ISO/IEC 14882:2020(E)

```cpp
template<class Key, class T, class Allocator>
unordered_map(initializer_list<pair<Key, T>>, typename see::size_type, Hash,
  -> unordered_map<Key, T, Hash, equal_to<Key>, Allocator>;
```

```cpp
// swap
template<class Key, class T, class Hash, class Pred, class Allococ>
void swap(unordered_map<Key, T, Hash, Pred, Allococ>& x,
  unordered_map<Key, T, Hash, Pred, Allococ>& y)
  noexcept(noexcept(x.swap(y)));
```

4 `unordered_map` 导推指南中的 `size_type` 参数指向由导推指南推出的类型的 `size_type` 成员。

# 22.5.4.2 构造函数 [unordered.map.cnstr]

```cpp
unordered_map() : size_type(see below) {
  explicit unordered_map(size_type n,
    const hasher& hf = hasher(),
    const key_eq& eql = key_eq(),
    const allocator& alloc = allocator_type());
```

- 1 使用指定的哈希函数、键等性谓词和分配器构造一个空的 `unordered_map`，并至少使用 `buckets`。对于默认构造函数，桶的数量由定义。`max_load_factor()` 返回 1。

- 2 复杂度：`Input()`
