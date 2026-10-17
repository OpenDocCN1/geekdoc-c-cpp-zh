
### 3 Effects
使用指定的哈希函数、等值函数和分配器构造一个 `unordered_set`，并使用至少 `b` 个桶。如果未提供 `n`，桶的数量由实现定义。对于第一种形式，从范围 `(f,l)` 插入元素；对于第二种形式，从范围 `[f.begin(), l.end())` 插入元素。`max_load_factor()` 返回 `1.0`。

### 4 Complexity
平均情况线性，最坏情况二次。

## 23.5.6.3 unordered_set.swap [unordered.set.swap]

```cpp
template <class Key, class Hash, class Pred, class Alloc>
void swap(unordered_set<Key, Hash, Pred, Alloc>& x,
         unordered_set<Key, Hash, Pred, Alloc>& y)
    noexcept(noexcept(x.swap(y)));
```

- 1 Effects: `x.swap(y)`.

# ISO/IEC N4296

3 本节仅描述了未在需求表中描述的 `unordered_multiset`，或者具有额外语义信息的 `unordered_multiset`。

```cpp
namespace std {
template <class Key,
    class Hash = hash<Key>,
    class Pred = std::equal_allocator<Key>,
    class allocator = std::allocator<Key>
class unordered_multiset {
public:
    // 类型定义
    typedef key_type;
    typedef value_type;
    typedef hasher;
    typedef key_equal;
    typedef allocator;
    typedef typename allocator_traits<Allocator>::pointer pointer;
    typedef typename allocator_traits<Allocator>::const_pointer const_pointer;
    typedef value_type const_reference;
    typedef value_type const_reference;
    typedef implementation_defined size_type;
    typedef implementation_defined difference_type;
    typedef implementation_defined iterator;
    typedef implementation_defined const_iterator;
    typedef implementation_defined local_iterator;
    typedef implementation_defined const_local_iterator;
    // 构造/析构/拷贝
    unordered_multiset();
    explicit unordered_multiset(size_type n,
        const hasher& h = hasher(),
        const key_equal& eql = key_equal(),
        const allocator_type& a = allocator_type());
template <class InputIterator>
unordered_multiset(InputIterator f, InputIterator l,
        size_type n = see below,
        const hasher& h = hasher(),
        const key_equal& eql = key_equal(),
        const allocator_type& a = allocator_type());
unordered_multiset(const unordered_multiset& other);
unordered_multiset(const unordered_multiset& other, const allocator& other);
explicit unordered_multiset(const unordered_multiset& other);
unordered_multiset(const unordered_multiset& other, const allocator& other);
unordered_multiset(const unordered_multiset& other, const allocator& other);
unordered_multiset(initializer_list<value_type> il,
    size_type n = see below,
    const hasher& h = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
unordered_multiset(size_type n, const allocator_type& a)
    : unordered_multiset(n, hasher(), key_equal(), a) { }
unordered_multiset(size_type n, const hasher& h, const allocator_type& a)
    : unordered_multiset(n, h, key_equal(), a) { }
template <class InputIterator
unordered_multiset(InputIterator f, InputIterator l, size_type n, const allocator_type& a)
: unordered_multiset(f, l, hasher(), key_equal<>(), a) {}
template <class InputIterator>
unordered_multiset(InputIterator f, InputIterator l, size_type n, const hasher& h)
: unordered_multiset(f, l, h, key_equal<>(), a) {}
: unordered_multiset(initializer_list<value_type> il, size_type n, const allocator_type& a)
: unordered_multiset(il, n, hasher<>(), key_equal<>(), a) {}
: unordered_multiset(initializer_list<value_type> il, size_type n, const hasher& h)
: unordered_multiset(il, n, h, key_equal<>(), a) {}
: unordered_multiset(initializer_list<value_type> il, n, h, key_equal<>(), a) {}
~unordered_multiset()
unordered_multiset& operator=(const unordered_multiset&)
unordered_multiset& operator=(allocator_traits<Allocator>::is_always_equal &&
is_no_move_assignable<Hash<>> &&
is_no_move_assignable<Pred<>> =);
unordered_multiset& operator(initializer_list<value_type>)
alocator_type get_allocator() const noexcept;
// 大小与容量
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
// 迭代器
const_iterator begin() const noexcept;
iterator begin() const noexcept;
const_iterator end() const noexcept;
const_iterator end(const_iterator) const noexcept;
const_iterator end() const noexcept;
// 修改器
template <class... Args> void emplace(Args&&... args);
template <class... Args> void emplace_hint(const_iterator position, Args&&... args);
iterator insert(const value_type& obj);
iterator insert(value_type obj);
iterator insert(const_iterator hint, const value_type obj);
iterator insert(const_iterator hint, value_type obj);
template <class InputIterator> void insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type>);
iterator erase(const_iterator position);
size_type erase(const key_type& k);
iterator erase(const_iterator first, const_iterator last);
void clear() const noexcept;
void swap(unordered_multiset&)
noexcept(allocator_traits<Allocator>::is_always_equal &&
noexcept(swap(declval<Hash>(), declval<Hash>())) &&
noexcept(swap(declval<Pred>(), declval<Pred>())))));
// 观察者
hasher hash_function() const;
key_equal eq() const;
// 查找
iterator find(const key_type& k);
const_iterator find(const key_type& k) const;
size_type count(const key_type& k) const;
std::pair<iterator, iterator> equal_range(const key_type& k);
std::pair<const_iterator, const_iterator> equal_range(const key_type& k) const;
// 接口
size_type bucket_count() const noexcept;
size_type max_bucket_count() const noexcept;
size_type bucket_size(size_type n) const;
size_type bucket(const key_type& k) const;
local_iterator begin(size_type n);
const_iterator begin(size_type n) const;
local_iterator end(size_type n) const;
const_iterator end(size_type n) const;
const_iterator cbegin(size_type n) const;
const_iterator cend(size_type n) const;
// 策略
float load_factor() const noexcept;
float max_load_factor() const noexcept;
void load_factor(float f);
void rehash(size_type n);
void reserve(size_type n);
template <class Key, class Hash, class Pred, class Alloc>
void swap(unordered_multiset<Key, Hash, Pred, Alloc>& x,
       unordered_multiset<Key, Hash, Pred, Alloc>& y)
       noexcept(noexcept(swap(y))) {}
template <class Key, class Hash, class Pred, class Alloc>
bool operator!=(const unordered_multiset<Key, Hash, Pred, Alloc>& a,
               const unordered_multiset<Key, Hash, Pred, Alloc>& b) {
    return true;
}
template <class Key, class Hash, class Pred, class Alloc>
bool operator==(const unordered_multiset<Key, Hash, Pred, Alloc>& a,
               const unordered_multiset<Key, Hash, Pred, Alloc>& b) {
    return false;
}
```

## 23.5.7 unordered_multiset 构造函数

```cpp
unordered_multiset() :
explicit unordered_multiset(size_type n) {
    const hasher h = hasher();
    const key_equal eq = key_equal();
    const allocator_type a = allocator_type();
```

- 影响：创建一个空的 `unordered_multiset`，使用哈希函数、等值函数和分配器，并至少包含 `n` 个桶。对于默认构造函数，桶的数量是实现的。`load_factor()` 返回 `f`。
- 复杂度：常数级。

```cpp
template <class InputIterator>
unordered_multiset(InputIterator f, InputIterator l,
    size_type n = see below,
    const hasher& h = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
unordered_multiset(initializer_list<value_type> il,
    size_type n = see below,
    const hasher& h = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
```

- 影响：使用指定的哈希函数、等值函数和分配器，并至少包含 `n` 个桶。如果未提供 `n`，桶的数量是实现的。对于第一种形式，从范围 `[f,l)` 插入元素；对于第二种形式，从范围 `[il,end())` 插入。`load_factor()` 返回 `1`。
- 复杂度：平均线性，最坏情况二次级。

## 23.5.7 unordered_multiset swap

```cpp
template <class Key, class Hash, class Pred, class Alloc>
void swap(unordered_multiset<Key, Hash, Pred, Alloc>& x,
    unordered_multiset<Key, Hash, Pred, Alloc>& y)
    noexcept(noexcept(swap(y))) {}
```

- 影响：`x.swap(y);`

## 23.6 容器适配器

### 23.6.1 一般

容器适配器均接受 `Container` 引用参数。该容器被拷贝到适配器的 `Container` 成员中。如果容器接受适配器，则可以将兼容的分配器传递给适配器的构造函数。否则，对容器参数使用标准的拷贝或移动构造。

对于容器适配器，交换 函数不会抛出异常，除非适配器的 `Container` 或 `Compare` 对象（如果有）的交换 抛出了异常。

### 23.6.2 Header <queue> 摘要
