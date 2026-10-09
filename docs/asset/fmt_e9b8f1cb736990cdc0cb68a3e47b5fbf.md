
## 22.4.5 multimap 类 (`Class multimap`)

- `multimap` 是一种关联容器，它支持键（可能包含相同值的多个副本），并能根据键快速检索另一种类型的值。`multimap` 容器支持双向迭代器。

`multimap` 满足容器和可反转容器（22.2）、关联容器（22.6）以及感知分配器的容器（表 76）的所有要求。`multimap` 还提供了 22.2.6 中描述的相等键的大多数操作。这意味着 `multimap` 支持 22.2.6 中的 `a_eq` 操作，但不支持 `uniq` 操作。对于 `multimap<Key,T>`，键和 `value_type` 是 `pair<const Key, T>`。这里提供了 `multimap` 操作的描述，这些操作在上述内容中未描述，或者对于具有额外语义信息的操作。

```cpp
namespace std {
template<class Key, class T, class Compare = less<Key>>
class multipap {
    class Allocator = allocator<pair<const Key, T>>>
public:
    using key_type = Key;
    using mapped_type = T;
    using value_type = pair<const Key, T>;
    using compare_type = Compare;
    using allocator_type = typename allocator_traits<Allocator>::allocator;
    using pointer = typename allocator_traits<Allocator>::pointer;
    using const_pointer = typename allocator_traits<Allocator>::const_pointer;
    using reference = value_type&;
    using const_reference = const value_type&;
    using implementation_defined; // sec 22.2
    using implementation_defined; // sec 22.2
    using implementation_defined; // sec 22.2
    using iterator = std::reverse_iterator<iterator>;
    using reverse_iterator = std::reverse_iterator<iterator>;
    using nodes_type = unspecified;

    class value_compare {
        friend class multipap;
    protected:
        Compare compare;
        value_compare(Compare c) : compare(c) {}
    public:
        bool operator() (const value_type& x, const value_type& y) const {
            return compare(x.first, y.first);
        }
    };

    // 22.4.5.2, 构造函数/析构
    multimap() : multipap() { }
    explicit multipap(const Compare& comp, const Allocator& alloc = Allocator());
    template<class Iterator>
    multimap(Iterator first, Iterator last,
             const Compare& comp = Compare(),
             const Allocator& alloc = Allocator());
    multimap(const multipap& x, const Allocator& alloc = Allocator());
    multimap(initializer_list<value_type> il, const Allocator& alloc = Allocator());
    ~multimap();
    multimap& operator=(const multipap& x);
    multimap& operator=(multimap&& x) 
        noexcept(allocator_traits<Allocator>::is_always_equal::value && std::is_n_swappable_v<T>);
    multimap& operator=(initializer_list<value_type> const&);
    allocator_type get_allocator() const except;

    const_iterator begin() noexcept;
    iterator end() noexcept;
    const_iterator end() const noexcept;

    reverse_iterator rbegin() noexcept;
    const_reverse_iterator rbegin() const noexcept;
    reverse_iterator rend() noexcept;
    const_reverse_iterator rend() const noexcept;

    const_iterator begin() noexcept;
    const_iterator end() const noexcept;
    const_reverse_iterator crbegin() const noexcept;
    const_reverse_iterator crend() const noexcept;

    // 容量
    [[nodiscard]] bool empty() const noexcept;
    size_type size() const noexcept;
    size_type max_size() const noexcept;

    // 22.4.5.3, 修改
    template<class... Args> Args& emplace(Args&&... args);
    template<class... Args> Args& emplace(const_iterator position, Args&&... args);
    iterator insert(const_iterator pos, value_type&& x);
    iterator insert(value_type&& x);
    template<class P> Iterator insert(const_iterator pos, P&& x);
    iterator insert(const_iterator position, value_type&& x);
    iterator insert(const_iterator position, value_type& x);
    template<class P> Iterator insert(const_iterator position, P& x);
    template<class Iterator> Iterator insert(Iterator first, Iterator last);
    void insert(InputIterator first, Iterator last);
    void insert(initializer_list<value_type> list);

    node_type extract(const_iterator position);
    node_type extract(const key_type& x);
    iterator insert(node_type&& nh);
    iterator insert(const_iterator hint, node_type&& nh);

    void erase(const_iterator position);
    void erase(const key_type& x);
    void erase(const_iterator first, const_iterator last);
    void swap(multimap&);
    void clear() noexcept(allocator_traits<Allocator>::is_always_equal::value && std::is_n_swappable_v<T>);

    template<class C2>
    void merge(multimap<Key, T, C2, Allocator>&& source);
    template<class C2>
    void merge(const multipap<Key, T, C2, Allocator>& source);

    // 观察
    key_compare key_comp() const;
    value_compare value_comp() const;

    // 映射操作
    iterator find(const key_type& x);
    const_iterator find(const key_type& x) const;
    template<class K> Iterator find(const K& x);
    template<class K> Iterator find(const K& x) const;

    size_type count(const key_type& x) const;
    template<class K> size_type count(const K& x) const;

    bool contains(const key_type& x) const;
    template<class K> bool contains(const K& x) const;

    iterator lower_bound(const key_type& x);
    const_iterator lower_bound(const key_type& x) const;
    template<class K> Iterator lower_bound(const K& x);
    template<class K> const_iterator lower_bound(const K& x) const;

    iterator upper_bound(const key_type& x);
    const_iterator upper_bound(const key_type& x) const;
    template<class K> Iterator upper_bound(const K& x);
    template<class K> const_iterator upper_bound(const K& x) const;

    pair<iterator, iterator> equal_range(const key_type& x);
    pair<const_iterator, const_iterator> equal_range(const key_type& x) const;
    template<class K> pair<iterator, iterator> equal_range(const K& x);
    template<class K> pair<const_iterator, const_iterator> equal_range(const K& x) const;
};

template<class InputIterator,
          class Compare = less<Key>,
          class Allocator = allocator<pair<const Key, T>>>
multimap<Key, T, Compare, Allocator>(InputIterator first, InputIterator last,
                                     Compare comp = Compare(),
                                     Allocator = Allocator()) {
}
```

### 22.4.5.2, 构造函数 [`multimap.cons`]

`explicit multipap(const Compare& comp, const Allocator& alloc = Allocator());`
- 影响：使用指定的比较对象和分配器构造一个空的 `multimap`。
- 复杂度：常数时间。

```cpp
template<class Iterator>
multimap(Iterator first, Iterator last,
         const Compare& comp = Compare(),
         const Allocator& alloc = Allocator());
```
- 影响：使用指定的比较对象和分配器构造一个空的 `multimap`，并从范围 `[first, last)` 插入元素。
- 复杂度：如果范围 `[first, last)` 已按照 `comp` 排序，则为 `N`；否则为 `log N`，其中 `N` 是 `last - first`。

### 22.4.5.3 修改 [`multimap.modifiers`]

`template<class P> iterator insert(P& x);`
`template<class P> iterator insert(const_iterator position, P& x);`
- 约束：`is_constructible<value_type, P& x>` 为真。
- 影响：第一种形式等于 `return(std::forward(x))`。第二种形式等于 `return insert_hint(position, std::forward(x))`。

### 22.4.5.4 删除 [`multimap.erasure`]

```cpp
template<class Key, typename T, class Compare, class Allocator, class Predicate>
multimap<Key, T, Compare, Allocator>::size_type
erase_if(multimap<Key, T, Compare, Allocator>& c, Predicate pred);
```
- 影响：等于：

```cpp
auto original_size = c.size();

for (auto i = c.begin(); i != c.end(); ) {

  if (pred(*i)) {

    i = c.erase(i);

  } else {

    ++i;

  }

}

return original_size - c.size();
```

## 22.4.6 类模板 [`set`]

### 22.4.6.1 概述

- `set` 是一种关联容器，支持唯一键（最多一个键值）并提供快速的键遍历。`set` 支持双向迭代器。
- `set` 满足容器 (22.2)、关联容器 (22.9) 以及分配器感知型（表 76）的所有要求。它还提供了 22.6 中针对唯一键的许多操作。这意味着 满足 22.6 中的 `a_unique` 操作，但不满足 `a_eq` 操作。对于 `set<Key>`，键和 `value_type` 都是 `Key`。描述仅针对这些类型中未描述或具有额外语义自由的操作。

```cpp
// 22.4.6. 构造/拷贝/析构

set() : set(Compare()) {}

explicit set(const Compare& comp, const Allocator& alloc = Allocator());

template<class InputIterator>

set(InputIterator first, InputIterator last,

    const Compare& comp = Compare(), const Allocator& alloc = Allocator());

set(const T& x);

set(set& x);

explicit set(const Allocator& alloc);

set(const T& x, const Allocator& alloc);

set(const T& x, set& x);

set(initializer_list<value_type> il, const Compare& comp = Compare(),

    const Allocator& alloc = Allocator());

template<class InputIterator>

set(InputIterator first, InputIterator last, const InputIterator& a)

    : set(first, last, Compare(a), alloc) {}
```
