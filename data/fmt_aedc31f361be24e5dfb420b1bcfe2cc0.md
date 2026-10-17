
# ISO/IEC 14882:2017(E)

## 26.5.6.2 无序集合构造函数 `unordered_set` [unord.set.constr]

```cpp
unordered_set() : unordered_set(size_type(see below)) {
explicit unordered_set(size_type n,
    const hasher& h = hasher(),
    const key_eql eql = key_equal(),
    const allocator_type& a = allocator_type());
```

- 1 效果：使用指定的哈希函数、键谓词和分配器构造一个 `unordered_set`，并至少包含 `n` 个桶。对于默认构造函数，桶的数量由实现定义。`max_load_factor()` 返回 1.0。
- 2 复杂度：常数级。

```cpp
template <class InputIterator>
unordered_set(InputIterator first,
    size_type n = see below,
    const hasher& h = hasher(),
    const key_eql eql = key_equal(),
    const allocator_type& a = allocator_type());
unordered_set(initializer_list<value_type> il,
    size_type n = see below,
    const hasher& h = hasher(),
    const key_eql eql = key_equal(),
    const allocator_type& a = allocator_type());
```

- 3 效果：使用指定的哈希函数、键谓词和分配器构造一个 `unordered_set`，并至少包含 `n` 个桶。如果未指定 `n`，桶的数量由实现定义。然后从第一种形式的范围 `[first, last)` 或从第二种形式的范围 `[il.begin(), il.end())` 中插入元素，`max_load_factor()` 返回 1.0。
- 4 复杂度：平均线性级，最坏情况二次级。

## 26.5.6.3 无序集合交换 `unordered_set` swap [ord.set.swap]

```cpp
template <class Key, class Hash, class Pred, class Alloc>
void swap(unordered_set<Key, Hash, Pred, Alloc>& x, unordered_set<Key, Hash, Pred, Alloc>& y) noexcept(x.swap(y));
```

- 1 效果：通过 `x.swap(y)` 执行。

## 26.5.7 类模板无序多集合 `unordered_multiset` [ord.multiset.overview]

### 26.5.7.1 类 `unordered_multiset`

`unordered_multiset` 是一种关联容器，支持等价键（`unordered_multiset` 的实例可能包含多个相同值的副本），并且每个元素本身就是该元素。`unordered_multiset` 支持前向迭代器。`unordered_multiset` 满足容器、关联容器和感知分配器的容器的所有要求。它提供了前述表中描述针对等价键的操作：对于 `Key` 类型，`iterator` 和 `const_iterator` 类型是否为同一种类型未指定。本节仅描述了 `unordered_multiset` 上未在表中描述的操作，或者对于有额外信息的 `unordered_multiset` 操作。

```cpp
namespace std {
    template <class Key,
    class Hash = hash<Key>,
    class Pred = equal_to<Key>,
    class Alloc = allocator<Key>>
    class unordered_multiset {
    public:
        // types:
        using key_type = Key;
        using value_type = Key;
        using hasher = Hash;
```

```cpp
using const_pointer = allocator_traits<Allocator>::const_pointer;

using reference = value_type&;

using const_reference = const value_type&;

using size_type = implementation-defined; // see 26.2

using difference_type = implementation-defined; // see 26.2

using iterator = implementation-defined; // see 26.2

using const_iterator = implementation-defined; // see 26.2

using local_iterator = implementation-defined; // see 26.2

using const_local_iterator = implementation-defined; // see 26.2

using node_type = unspecified;

using insert_return_type = INSERT_RETURN_iterator<node_type>;

// 26.5.6.2. construct(copy/destroy)

unordered_set();

explicit unordered_set(size_type n) {
    const hasher hf = hasher(n);
    const key_equal& eql = key_equal();
    const allocator_type& a = allocator_type();
}

template<class Iterator1, class Iterator1>
unordered_set(Iterator1 first, Iterator1 last,
    size_type n = 0) // see below,
    const hasher hf = hasher(n);
    const key_equal& eql = key_equal();
    const allocator_type& a = allocator_type())
{}

unordered_set(const unordered_set& s);
unordered_set(const unordered_set& other);
explicit unordered_set(const Allocator&, const Allocator&);
unordered_set(const unordered_set&, const Allocator&);
unordered_set(initializer_list<value_type> i,
    size_type n = 0, // see below,
    const hasher h = hasher<Key>(),
    const key_eq eq = key_equal<Key>(),
    const allocator_type a = allocator<Key>());

unordered_set(size_type n, const allocator_type a)
    : unordered_set(n, h(), eq(), a) {}

unordered_set(size_type n, const hasher h, const allocator_type a)
    : unordered_set(n, h, key_equal(), a) {}

template<class InputIterator>
unordered_set(InputIterator f, InputIterator i, size_type n, const allocator_type a)
    : unordered_set(f, i, n, key_equal(), a) {}

template<class InputIterator>
unordered_set(InputIterator f, InputIterator i, size_type n, const hasher h,
    const allocator_type a)
    : unordered_set(f, i, n, h, key_equal(), a) {}

unordered_set(initializer_list<value_type> i, size_type n, const allocator_type a)
    : unordered_set(i, n, h(), a) {}

unordered_set(initializer_list<value_type> i, size_type n, const hasher h,
    const allocator_type a)
    : unordered_set(i, n, h, key_equal(), a) {}

unordered_set();
unordered_set& operator=(const unordered_set&)
noexcept(allocator_traits<Allocator>::is_always_equal);
unordered_set& operator=(initializer_list<value_type> i)
noexcept(allocator_traits<Allocator>::is_move_assignable);
allocator_type get_allocator() const noexcept;

// iterators:
iterator begin() const noexcept;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator end() const noexcept;
const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;

// capacity:
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;

// bucket:
template<class Args...> pair<iterator, bool> emplace(Args...);
template<class Args...> pair<iterator, bool> emplace(const_iterator, Args...);
pair<iterator, bool> emplace(const value_type&);
pair<iterator, bool> emplace(value_type&&);
pair<iterator, bool> emplace(const_iterator hint, value_type&);
pair<iterator, bool> emplace(value_type&&);
template<class InputIterator> void emplace(InputIterator first, InputIterator last);
void emplace(initializer_list<value_type> i);
node_type extract(const_iterator pos);
node_type extract(const key_type&);
insert_return_type extract(node_type&&);
void extract(const_iterator hint, node_type&&);
iterator erase(const_iterator pos);
iterator erase(const_iterator hint);
size_type erase(const key_type&);
size_type erase(iterator first, iteratorator last);
void swap(unordered_set& other) noexcept(allocator_traits<Allocator>::is_always_equal);
void clear();
template<class H2, class P2> void merge(unordered_set<H2, P2>&&);
template<class H2, class P2> void merge(unordered_set<H2, P2>&&);
template<class H2, class P2> void merge(unordered_mult<H2, P2>&&);
template<class H2, class P2> void merge(unordered_mult<H2, P2>&&);

// observers:
hash_function() const;
key_eq() const;

// set operations:
iterator find(const key_type&);
const_iterator find(const key_type&) const;
size_type count(const key_type&) const;
pair<iterator, iterator> equal_range(const key_type&) const;
pair<const_iterator, const_iterator> equal_range(const key_type&) const;

// bucket interface:
size_type bucket_count() const;
size_type bucket_count(size_type n) const;
size_type bucket(const key_type&) const;
local_iterator begin(size_type n) const;
const__iterator begin(size_type n) const;
local_iterator end(size_type n) const;
const_local_iterator cbegin(size_type n) const;
const_local_iterator cend(size_type n) const;

// hash policy:
float load_factor() const noexcept;
float max_load_factor() const noexcept;
void max_load_factor(float z);
void rehash(size_type n);
void reserve(size_type n);

template<class InputIterator, iterator_traits<InputIterator>::value_type,
    class Hash = equal_to<typename iterator_traits<InputIterator>::value_type>,
    class Pred = allocator<typename iterator_traits<InputIterator>::value_type>,
    class Allocator = allocator<typename iterator_traits<InputIterator>::value_type>>
    unordered_set(InputIterator, InputIterator, typename see = size_type = see below,
        Hash hash = Hash(), Pred pred = Pred(), Allocator alloc = Allocator())
    -> unordered_set<typename iterator_traits<InputIterator>::value_type,
        Hash, Allocator>;

template<class T, class Hash = hash<T>, class Allocator = allocator<T>>
    unordered_set(initializer_list<T> i, typename see = size_type = see below,
        Hash hash = Hash(), Pred pred = Pred(), Allocator alloc = Allocator())
    -> unordered_set<T, Hash, Allocator>;
};
```
