

# ISO/IEC 14882:2017(E)

```cpp
unordered_map(Iterator f, Iterator l, size_type n, const allocator_type& a) 
    : unordered_map(f, 1, n, hasher(), key_equal(a), a) { }
template<class Iterator>
unordered_map(Iterator f, Iterator l, size_type n, const hasher& hf,
    const allocator_type& a) 
    : unordered_map(f, 1, n, hf, key_equal(a), a) { }
template<class Value>
unordered_map(initializer_list<Value> n, hasher(), key_equal(a), a) 
    : unordered_map(initializer_list<Value>(n), hasher(), key_equal(a)) {}
unordered_map(initializer_list<Value> l, size_type n, const hasher& hf,
    const allocator_type& a) 
    : unordered_map(initializer_list<Value>(l), n, hf, key_equal(a), a) {}
unordered_map& operator=(const unordered_map&);
unordered_map& operator=(const unordered_map&&)
const allocator_traits<Allocator>::is_equal::value &&
    is_throw_move_assignable<VPred> &&
unordered_map& operator(initializer_list<Value> type);
allocator_type get_allocator() const noexcept;

// 迭代器：
```

```cpp
iterator;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator begin() const noexcept;
const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
```

附录:

```cpp
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
```

```cpp
// 26.5.5.3,
template<class... Args>
iterator& insert(Args&&... args);
template<class... Args>
iterator insert_hint(const iterator_position, Args&&... args);
iterator insert(const value_type& obj);
template<class P>
iterator insert(P&& obj);
iterator insert(const iterator_hint, const value_type& obj);
template<class P>
iterator insert(const iterator_hint, P&& obj);
template<class Iterator>
iterator insert(Iterator first, Iterator last);
iterator insert(initializer_list<Value> l, size_type n);
```

```cpp
node_type extract(const iterator_position);
node_type extract(const key_type& x);
iterator extract(node_type&& nh);
iterator extract(const iterator_hint, node_type&& nh);

iterator erase(iterator_position position);
iterator erase(const iterator_position position);
size_type erase(const key_type& k);
iterator erase(const iterator_first first, const iterator_iterator last);
void swap(unordered_map& other);
```

§ 26.5.5.1

©ISO/IEC 2017 - 版留权利

```cpp
noexcept(allocator_traits<Allocator>::is_always_equal<value_type> &&
    is_not_swappable_v<Hash> &&
    is_not_swappable_v<Pred>) noexcept
void clear();
```

```cpp
template<class H2, class P2>
void merge(unordered_map<Key, T, H2, P2, Allocator>& source);
template<class H2, class P2>
void merge(unordered_map<Key, T, H2, P2, Allocator>&& source);
template<class H2, class P2>
void merge(unordered_map<Key, T, H2, P2, Allocator>* source);
template<class H2, class P2>
void merge(unordered_map<Key, T, H2, P2, Allocator>&& source);
```

```cpp
// 者
hasher hash_function() const;
key_equal key_equal() const;
```

```cpp
// map 操作
iterator find(const key_type& k);
const_iterator find(const key_type& k);
size_type count(const key_type& k) const;
const_iterator count(const key_type& k) const;
pair<iterator, iterator> range(const key_type& k);
pair<const_iterator, const_iterator> range(const key_type& k) const;
```

```cpp
// 桶策略
size_type bucket_count() const noexcept;
size_type max_bucket_count(size_type n) const noexcept;
size_type bucket_count(size_type n) const;
size_type bucket_count(const key_type& k) const;
local_iterator begin(size_type n);
const_iterator begin(size_type n) const;
local_iterator end(size_type n);
const_iterator end(size_type n) const;
local_iterator cbegin(size_type n) const;
const_iterator cend(size_type n) const;
```

```cpp
// 哈希策略
float load_factor() const noexcept;
float max_load_factor(float z) const noexcept;
void rehash(size_type n);
void reserve(size_type n);
```

```cpp
template<class InputIterator,
class Hash = hash<key_type<InputIterator>>,
class Pred = equal_to<key_type<InputIterator>>,
class Allocator = allocator<pair<const key_type<InputIterator>, value_type>>>
unordered_map(InputIterator first, InputIterator last, size_type n,
    Hash h = Hash(), Pred = Pred(), Allocator a = Allocator())
: unordered_map<key_type<InputIterator>, value_type<InputIterator>, Hash, Pred, Allocator>;
```

```cpp
template<class Iterator, class Allocator = Allocator>
unordered_multimap(Iterator first, Iterator last, Allocator a)
  : unordered_multimap<key_type<Iterator>, value_type<Iterator>,
    hash<key_type<Iterator>>, equal<key_type<Iterator>>,
```

```cpp
template<class Iterator, class Allocator = Allocator>
unordered_multimap(Iterator first, Allocator a)
  : unordered_multimap<key_type<Iterator>, value_type<Iterator>,
    hash<key_type<Iterator>>, equal<key_type<Iterator>>,
```

```cpp
template<class Key, class Hash, class Allocator = Allocator>
unordered_multimap(initializer_list<pair<Key, T>> l, size_type n,
                   Hash h = Hash(), Allocator a = Allocator())
  : unordered_multimap<Key, T, Hash, equal_to<Key>, Allocator>;
```

```cpp
template<class Key, class Hash, class Allocator = Allocator>
unordered_multimap(initializer_list<pair<Key, T>> l, Allocator a)
  : unordered_multimap<Key, T, Hash, equal_to<Key>, Allocator>;
```

```cpp
template<class Key, class Hash, class Allocator = Allocator>
unordered_multimap(initializer_list<pair<Key, T>> l, size_type n,
                   Hash h = Hash(), Allocator a = Allocator())
  : unordered_multimap<Key, T, Hash, equal_to<Key>, Allocator>;
```

```cpp
template<class Key, class Hash, class Pred, class Allocator = Allocator>
bool operator=(const unordered_multimap<Key, T, Hash, Pred, Allocator>& a,
               const unordered_multimap<Key, T, Hash, Pred, Allocator>& b);
```

```cpp
template<class Key, class Hash, class Pred, class Allocator = Allocator>
bool operator=(unordered_multimap<Key, T, Hash, Pred, Allocator>&& a,
               const unordered_multimap<Key, T, Hash, Pred, Allocator>& b);
```

// 26.5.5.1 swap
template<class Key, class Hash, class Pred, class Allocator = Allocator>
void swap(unordered_multimap<Key, T, Hash, Pred, Allocator>& x,
         unordered_multimap<Key, T, Hash, Pred, Allocator>& y)
  noexcept(noexcept(x.swap(y)));
```

unordered_multimap 推导指南中的 size_type 参数指的是推导指南类型的 size_type 成员。

§ 26.5.5.1

©ISO/IEC 2017 - 版留权利

## 26.5.5.2 unordered_multimap 构造函数 [unordered.multimap.cnstr]

```cpp
unordered_multimap() : unordered_multimap(size_type(see below)) {}
explicit unordered_multimap(size_type n,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& alloc = allocator_type());
```

- 1 效果：使用指定的哈希函数、键相等谓词和分配器构造 unordered_multimap，并使用至少 n 个桶。对于默认构造函数，桶的数量由定义。max_load_factor() 返回 1.0。
- 2 复杂度：常数级。

```cpp
template<class Iterator>
unordered_multimap(Iterator f, Iterator l,
    size_type n = see below,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& alloc = allocator_type());
unordered_multimap(initializer_list<value_type> il,
    size_type n = see below,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& alloc = allocator_type());
```

- 3 效果：使用指定的哈希函数、键相等谓词和分配器构造 unordered_multimap，并使用至少 n 个桶。如果没有提供 n，桶的数量由定义。对于第一种形式，从范围 [f, l) 插入元素；对于第二种形式，从范围 [il.begin(), il.end()) 插入。max_load_factor() 返回 1.0。
- 4 复杂度：平均线性，最坏二次。

## 26.5.5.3 unordered_multimap 修改器 [unordered.multimap.modifiers]

```cpp
template <class P>
iterator insert(const P& obj);
```

- 1 效果：等同于返回 replace(std::forward<P>(obj))。
- 2 备注：除非 is_constructible<value_type, P> 为真，否则此签名不参与重载解析。

```cpp
template <class P>
iterator insert(const iterator_hint hint, const P& obj);
```

- 3 效果：等同于返回 place_hint(hint, std::forward<P>(obj))。
- 4 备注：除非 is_constructible<value_type, P> 为真，否则此签名不参与重载解析。

## 26.5.5.4 unordered_multimap swap [unordered.multimap.swap]

```cpp
template <class Key, class T, class Hash, class Pred, class Alloc>
void swap(unordered_multimap<Key, T, Hash, Pred, Allocator>& x,
    unordered_multimap<Key, T, Hash, Pred, Allocator>& y)
    except(noexcept(x.swap(y)));
```

