
```cpp
template<class Iterator>
unordered_map(Iterator f, Iterator l,
  size_type n = see below,
  const hasher& hf = hasher(),
  const key_eq& eql = key_eq(),
  const allocator& alloc = allocator_type());
unordered_map(initializer_list<value_type> l,
  size_type n = see below,
  const hasher& hf = hasher(),
  const key_eq& eql = key_eq(),
  const allocator& alloc = allocator_type());
```

- 3 使用指定的哈希函数、键等性谓词和分配器构造一个空的 `unordered_map`，并至少使用 `buckets`。如果未提供 `n`，桶的数量由实现定义。对于第一种形式，从范围 `[f, l)` 插入元素；对于第二种形式，从范围 `[il.begin(), il.end())` 插入元素。`max_load_factor()` 返回 1。

- 4 复杂度：平均情况线性，最坏情况二次二次。

# 22.5.4.3 元素访问 [unordered.map.elem]

- `mapped_type operator()(const key_type& k);`

  1 等于：`return this->at(k).first->second;`

- `mapped_type operator[](const key_type& k);`

  2 等于：`return this->at(move(k)).first->second;`

- `mapped_type& at(const key_type& k);`

  `const mapped_type& at(const key_type& k) const;`

- 3 返回对 `x.second` 的引用，其中 `x` 是与 `k` 等效的（唯一）元素。

- 4 如果不存在元素，则抛出一个类型为 `out_of_range` 的异常对象。

# 22.5.4.4 修改器 [unordered.map.modifiers]

```cpp
template<class P>
p<iterator, bool> insert(P& obj);
```

- 1 约束：`is_constructible<value_type, P&>` 为 `true`。

影响：等于：`return element(std::forward<P>(obj));`

```cpp
template<class P>
iterator insert(const iterator_hint hint, P& obj);
```

约束：`is_constructible_v<value_type, P&>` 为 `true`。

影响：等于：`return element(std::forward<P>(obj));`

```cpp
template<class... Args>
pair<iterator, bool> try_replace(const key_type& k, Args&... args);
template<class... Args>
iterator try_replace(const iterator_hint hint, const key_type& k, Args&... args...);
```

前置条件：`value_type` 可以通过 `piecewise_construct`、`forward_tuple(k)`、`forward_tuple(std::forward<Args>(args)...)` 构造进 `unordered_map`。

影响：如果 map 中已经包含与 `k` 等效的元素，则没有影响。否则，插入一个类型为 `value_type` 的对象，该对象通过 `piecewise_construct`、`forward_tuple(k)`、`forward_tuple(std::forward<Args>(args)...)` 构造。

返回：在第一个重载中，返回对的 `bool` 部分当且仅当插入发生时为 `true`。返回的迭代器指向与 `k` 等效的 map 元素。

复杂度：与 `emplace` 和 `insert_hint` 相同。

# ISO/IEC 14882:2020(E)

`using local_iterator = implementation-defined;` // 查看 22.2

`using const_local_iterator = implementation-defined;` // 查看 22.2

`using node_type = unspecified;`

```cpp
// 22.5.5.3, 拷贝/析
unordered_map() = default;
explicit unordered_map(size_type n, 
    const hasher& h = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());

template<class Iterator>
unordered_map(Iterator f, Iterator l,
    size_type n = see下方,
    const hasher& h = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());

unordered_multimap(const unordered_multimap&);
unordered_multimap(const unordered_multimap&);
explicit unordered_multimap(const Allocator&);
unordered_multimap(const unordered_multimap&, const Allocator&);
unordered_multimap(initializer_list<value_type> il,
    size_type n = see下方,
    const hasher& h = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());

unordered_multimap(size_type n, const allocator_type& a)
    : unordered_multimap(n, hasher(), key_equal(), a) {}

unordered_multimap(size_type n, const hasher& h, const allocator_type& a)
    : unordered_multimap(n, hasher(), key_equal(), a) {}

template<class Iterator>
unordered_multimap(Iterator f, Iterator l, size_type n, const allocator_type& a)
    : unordered_multimap(f, l, n, hasher(), key_equal());

template<class Iterator>
unordered_multimap(Iterator f, Iterator l, size_type n, const hasher& h,
    const allocator_type& a = allocator_type())
    : unordered_multimap(f, l, n, hasher(), key_equal()) {}

unordered_multimap(initializer_list<value_type> il, size_type n, const allocator_type& a)
    : unordered_multimap(il, n, hasher(), key_equal(), a) {}

unordered_multimap(initializer_list<value_type> il, size_type n, const hasher& h,
    const allocator_type& a = allocator_type())
    : unordered_multimap(il, n, hasher(), key_equal(), a) {}

unordered_multimap& operator=(const unordered_multimap&);
unordered_multimap& operator=(const unordered_multimap&);

noexcept(allocator_traits<Allocator>::is_always_equal &&
    is_nothmove_assignable<v_Hash> &&
    is_nothrow_assignable<value_type>)
unordered_multimap& operator=(initializer_list<value_type>);

allocator_type get_allocator() const noexcept;
```

// 迭代器

```cpp
iterator;
const_iterator begin() const noexcept;
iterator;
const_iterator end() const noexcept;
const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
```

// 容量

```cpp
[[nodiscard]] bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
```

```cpp
// 22.5.5.3, 修改器
template<class... Args> iterator emplace(Args&&... args);
template<class... Args> iterator emplace(const iterator_hint& hint, Args&&... args);

iterator insert(const value_type& obj);
iterator insert(value_type& obj);
iterator insert(const P& obj);
iterator insert(const iterator_hint& hint, const value_type& obj);
iterator insert(const iterator_hint& hint, value_type& obj);

template<class P> P insert(const iterator_hint& hint, P&& obj, InputIterator last);
template<class InputIterator> Iterator insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type> init);

node_type extract(const iterator_pos& pos);
node_type extract(const key_type& k);
iterator insert(const node_type& nh);
iterator insert(const iterator_hint& hint, const node_type& nh);

iterator erase(const iterator_pos& pos);
iterator erase(const key_type& k);
size_type erase(const iterator_first& first, const iterator_last);

void swap(unordered_map& other) noexcept(allocator_traits<Allocator>::is_default_constructed() && 
    is_not_swappable_v<Hash> &&
    is_n_swappable_v<Pred>);

void clear() noexcept;

template<class H2, class T, class P2>
void merge(unordered_multimap<Key, T, H2, P2, Allocator<>>& source);
template<class H2, class P2>
void merge(unordered_multimap<Key, T, H2, P2, Allocator<>>& source);
void merge(unordered_map<Key, T, P2, Allocator<>>& source);
template<class H2, class P2>
void merge(unordered_multimap<Key, T, H2, P2, Allocator<>>& source);
// 观察者
hash function();
key_equal eq() const;

// 操作
iterator find(const key_type&);
const_iterator find(const key_type&);
template<class K> iterator find(const K&);
template<class K> const_iterator find(const K&);

size_type count(const key_type&);
template<class K> size_type count(const K&);

bool contains(const key_type&);
template<class K> bool contains(const K&);

pair<iterator, iterator> equal_range(const key_type&);
template<class K> pair<iterator, iterator> equal_range(const K&);
size_type> equal_range(const K&);

// 桶接口
size_type bucket_count() const noexcept;
size_type max_bucket_count() const noexcept;
size_type bucket(size_type) const;
iterator begin(size_type) const;
iterator end(size_type) const;
void begin(size_type, iterator);
void end(size_type, iterator&);

// 哈希策略
float load_factor() const noexcept;
float max_load_factor() const noexcept;
void load_factor(float);
void reserve(size_type);
```

```cpp
} } else {
    ++i;
}
    return original_size - c.size();
```

## 22.5.6 类模板 unordered_set

### 22.5.6.1 概述

- `unordered_set` 是一种关联容器，它支持键（`unordered_set` 最多包含一个键值，且其中键即为元素）。`unordered_set` 支持前向迭代器。

- `unordered_set` 满足容器、关联容器以及感知分配器的容器的所有要求（表 76）。它提供了前述要求中描述的、针对唯一键的操作；即，`unordered_set` 支持该表中的 `a_uniq` 操作，但不支持 `a_eq` 操作。对于 `unordered_set<Key>`，键类型和值类型均为 `Key`。`iterator` 和 `const_iterator` 类型均属于迭代器类型。它们是否为同一种类型是未确定的。

### 22.5.6.2 unordered_set 中未在任何一个要求表中描述的成员操作，或具有额外语义信息的成员操作。
