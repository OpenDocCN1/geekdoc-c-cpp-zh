

## 22.5.4.2 构造器 [unord.map.cnstr]

```
template<class Key, class T, class Hash, class Allocator>
    unordered_map(initializer_list<pair<Key, T>>, typename see below::size_type, Hash, Allocator)
        -> unordered_map<Key, T, Hash, equal_to<Key>, Allocator>;

// swap
template<class Key, class T, class Hash, class Pred, class Alloc>
    void swap(unordered_map<Key, T, Hash, Pred, Alloc>& x,
              unordered_map<Key, T, Hash, Pred, Alloc>& y)
        noexcept(noexcept(x.swap(y)));
}
```

4 在 unordered_map 推导指引中，size_type 参数类型指的是由该推导指引推导出的类型的 size_type 成员类型。

```
unordered_map() : unordered_map(size_type(see below)) { }
explicit unordered_map(size_type n,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
```

1 效果：使用指定的哈希函数、键相等谓词和分配器构造一个空的 unordered_map，并使用至少 n 个桶。对于默认构造函数，桶的数量由实现定义。max_load_factor() 返回 1.0。

2 复杂度：常数。

```
template<class InputIterator>
    unordered_map(InputIterator f, InputIterator l,
        size_type n = see below,
        const hasher& hf = hasher(),
        const key_equal& eql = key_equal(),
        const allocator_type& a = allocator_type());
unordered_map(initializer_list<value_type> il,
    size_type n = see below,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
```

3 效果：使用指定的哈希函数、键相等谓词和分配器构造一个空的 unordered_map，并使用至少 n 个桶。如果未提供 n，则桶的数量由实现定义。然后从范围 [f, l) 中插入元素，针对第一种形式，或从范围 [il.begin(), il.end()] 中插入元素，针对第二种形式。max_load_factor() 返回 1.0。

4 复杂度：平均情况线性，最坏情况二次。

## 22.5.4.3 元素访问 [unord.map.elem]

```
mapped_type& operator[](const key_type& k);
```

1 效果：等价于：return try_emplace(k).first->second;

```
mapped_type& operator[](key_type&& k);
```

2 效果：等价于：return try_emplace(move(k)).first->second;

```
mapped_type& at(const key_type& k);
const mapped_type& at(const key_type& k) const;
```

3 返回：对 x.second 的引用，其中 x 是键等价于 k 的（唯一）元素。

4 抛出：如果不存在此类元素，则抛出类型为 out_of_range 的异常对象。

## 22.5.4.4 修改器 [unord.map.modifiers]

```
template<class P>
    pair<iterator, bool> insert(P&& obj);
```

1 约束：is_constructible_v<value_type, P&&> 为 true。

效果：如果映射已包含键等价于 k 的元素 e，则将 std::forward<M>(obj) 赋给 e.second。否则插入一个使用 std::move(k)、std::forward<M>(obj) 构造的 value_type 类型的对象。

返回：在第一个重载中，返回的 pair 的 bool 分量当且仅当插入发生时为 true。返回的迭代器指向键等价于 k 的映射元素。

复杂度：与 emplace 和 emplace_hint 分别相同。

## 22.5.4.5 删除 [unord.map.erasure]

```
template<class K, class T, class H, class P, class A, class Predicate>
typename unordered_map<K, T, H, P, A>::size_type
erase_if(unordered_map<K, T, H, P, A>& c, Predicate pred);
```

效果：等价于：

```
auto original_size = c.size();
for (auto i = c.begin(), last = c.end(); i != last; ) {
    if (pred(*i)) {
        i = c.erase(i);
    } else {
        ++i;
    }
}
return original_size - c.size();
```

## 22.5.5 类模板 unordered_multimap [unord.multimap]

## 22.5.5.1 概述 [unord.multimap.overview]

1 unordered_multimap 是一个无序关联容器，支持等价键（unordered_multimap 的实例可能包含每个键值的多个副本），并将另一个类型 mapped_type 的值与键关联。unordered_multimap 类支持前向迭代器。

2 unordered_multimap 满足容器、无序关联容器以及分配器感知容器（表 76）的所有要求。它为等价键提供了前述需求表中描述的操作；也就是说，unordered_multimap 支持该表中的 a_eq 操作，而非 a_uniq 操作。对于 unordered_multimap<Key, T>，键类型为 Key，映射类型为 T，值类型为 pair<const Key, T>。

3 子条款 22.5.5 仅描述 unordered_multimap 上的操作，这些操作未在需求表中描述，或存在额外的语义信息。

```
namespace std {
template<class Key,
         class T,
         class Hash = hash<Key>,
         class Pred = equal_to<Key>,
         class Allocator = allocator<pair<const Key, T>>>
class unordered_multimap {
public:
// types
using key_type = Key;
using mapped_type = T;
using value_type = pair<const Key, T>;
using hasher = Hash;
using key_equal = Pred;
using allocator_type = Allocator;
using pointer = typename allocator_traits<Allocator>::pointer;
using const_pointer = typename allocator_traits<Allocator>::const_pointer;
using reference = value_type&;
using const_reference = const value_type&;
using size_type = implementation-defined; // see 22.2
using difference_type = implementation-defined; // see 22.2
using iterator = implementation-defined; // see 22.2
using const_iterator = implementation-defined; // see 22.2
```

```
size_type bucket(const key_type& k) const;
local_iterator begin(size_type n);
const_local_iterator begin(size_type n) const;
local_iterator end(size_type n);
const_local_iterator end(size_type n) const;
const_local_iterator cbegin(size_type n) const;
const_local_iterator cend(size_type n) const;

// hash policy
float load_factor() const noexcept;
float max_load_factor() const noexcept;
void max_load_factor(float z);
void rehash(size_type n);
void reserve(size_type n);
};

template<class InputIterator,
    class Hash = hash<iter-key-type<InputIterator>>,
    class Pred = equal_to<iter-key-type<InputIterator>>,
    class Allocator = allocator<iter-to-alloc-type<InputIterator>>>
unordered_multimap(InputIterator, InputIterator,
    typename see below::size_type = see below,
    Hash = Hash(), Pred = Pred(), Allocator = Allocator())
-> unordered_multimap<iter-key-type<InputIterator>, iter-mapped-type<InputIterator>,
    Hash, Pred, Allocator>;

template<class Key, class T, class Hash = hash<Key>,
    class Pred = equal_to<Key>, class Allocator = allocator<pair<const Key, T>>>
unordered_multimap(initializer_list<pair<Key, T>>,
    typename see below::size_type = see below,
    Hash = Hash(), Pred = Pred(), Allocator = Allocator())
-> unordered_multimap<Key, T, Hash, Pred, Allocator>;

template<class InputIterator, class Allocator>
unordered_multimap(InputIterator, InputIterator, typename see below::size_type, Allocator)
-> unordered_multimap<iter-key-type<InputIterator>, iter-mapped-type<InputIterator>,
    hash<iter-key-type<InputIterator>>,
    equal_to<iter-key-type<InputIterator>>, Allocator>;

template<class InputIterator, class Allocator>
unordered_multimap(InputIterator, InputIterator, Allocator)
-> unordered_multimap<iter-key-type<InputIterator>, iter-mapped-type<InputIterator>,
    hash<iter-key-type<InputIterator>>,
    equal_to<iter-key-type<InputIterator>>, Allocator>;

template<class InputIterator, class Hash, class Allocator>
unordered_multimap(InputIterator, InputIterator, typename see below::size_type, Hash,
    Allocator)
-> unordered_multimap<iter-key-type<InputIterator>, iter-mapped-type<InputIterator>, Hash,
    equal_to<iter-key-type<InputIterator>>, Allocator>;

template<class Key, class T, class Allocator>
unordered_multimap(initializer_list<pair<Key, T>>, typename see below::size_type,
    Allocator)
-> unordered_multimap<Key, T, hash<Key>, equal_to<Key>, Allocator>;

template<class Key, class T, class Allocator>
unordered_multimap(initializer_list<pair<Key, T>>, Allocator)
-> unordered_multimap<Key, T, hash<Key>, equal_to<Key>, Allocator>;

template<class Key, class T, class Hash, class Allocator>
unordered_multimap(initializer_list<pair<Key, T>>, typename see below::size_type,
    Hash, Allocator)
-> unordered_multimap<Key, T, Hash, equal_to<Key>, Allocator>;
```

