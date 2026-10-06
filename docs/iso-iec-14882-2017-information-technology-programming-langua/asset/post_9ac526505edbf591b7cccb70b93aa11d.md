
# ISO/IEC 14882:2017(E)

Otherwise inserts an object of type value_type constructed with piecewise_construct, forward_as_tuple(std::move(k)), forward_as_tuple(std::forward<Args>(args)...).

Returns in the first overload, the bool component of the returned pair is true if and only if the insertion took place. The returned iterator points to the map element which is equivalent to k.

Complexity: The same as emplace_hint, respectively.

```cpp
template <class M>
iterator insert_assign(const key_type& k, M& obj);
template <class M>
iterator insert_or_assign(const iterator, const key_type& k, M& obj);
```

Requires: is_assignable<value_type, M> shall be true. value_type shall be Emplace-Constructible into map from move(k). forward(obj).

Effects: If the map already contains an element e equivalent to k, assigns std::forward<Args>(obj) to e. Otherwise inserts an object of type value_type constructed with std::forward<Args>(obj).

Returns in the first overload, the bool component of the returned pair is true if and only if the insertion took place. The returned iterator points to the map element which is equivalent to k.

Complexity: The same as emplace_hint, respectively.

```cpp
template <class M>
iterator insert_or_assign(const key_type& k, M& obj);
template <class M>
iterator insert_or_assign(const iterator, const key_type& k, M& obj);
```

Requires: is_assignable<value_type, M> shall be true. value_type shall be Emplace-Constructible into map from move(k). forward(obj).

Effects: If the map already contains an element e equivalent to k, assigns std::forward<Args>(obj) to e. Otherwise inserts an object of type value_type constructed with std::forward<Args>(obj).

Returns in the first overload, the bool component of the returned pair is true if and only if the insertion took place. The returned iterator points to the map element which is equivalent to k.

Complexity: The same as emplace_hint, respectively.

# 26.4.5 map specialized algorithms [map.special]

```cpp
template <class Key, class T, class Compare, class Allocator>
void swap(map<Key, T, Compare, Allocator>& x,
       map<Key, T, Compare, Allocator>& y)
       except(noexcept(x.swap(y)));
```

Effects: As by x.swap(y).

# 26.4.5 Class template multimap [multimap.overview]

# 26.4.5.1 Class template multimap overview

- multimap is an associative container that supports keys (possibly containing multiple copies of the same key value) and provides fast retrieval of another type T based on the keys. The multimap supports bidirectional iterators.

- A multimap satisfies all the requirements of a container of a reversible container (26.2.6), of an associative container (26.2.6), and an allocator-aware container (Table 86). A multimap also provides most operations described in 26.2.6 for equal keys. This means that a multimap supports the a_eq equation not a_uniq operations. for a multimap<Key,T> the key_type is Key and the value_type is pair<Key,T>. Descriptions are here only for operations on multimap that are not described in one of those or for operations where there is semantic information.

```cpp
namespace std {
    template <class Key, class T, class Compare = less<pair<const Key, T>>>
    class Allocator = allocator<pair<const Key, T>>;
    class multimap {
    public:
        using key_type = Key;
        using mapped_type = T;
        using value_type = pair<const Key, T>;
        using compare_type = Compare;
        using allocator_type = Allocator;
        using pointer = typename allocator_traits<Allocator>::pointer;
        using const_pointer = typename allocator_traits<Allocator>::const_pointer;
        using reference = value_type&;
        using const_reference = const value_type& // see 36.2
        using size_type = implementation_defined; // see 36.2
        using iterator = implementation_defined; // see 36.2
        using const_iterator = implementation_defined; // see 36.2
        using reverse_iterator = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;

    class value_compare = Compare {
        friend class multimap;
    protected:
        Compare comp;
    public:
        bool operator()(const value_type& x, const value_type& y) const {
            return comp(x.first, y.first);
        }
    };

    // 26.4.5.2. constructor/destroy
    multimap(const Compare& comp = Compare(), const Allocator& alloc = Allocator());
    template <class Iterator>
    multimap(Iterator first, Iterator last,
             const Compare& comp = Compare(),
             const Allocator& alloc = Allocator());
    multimap(const multimap& x);
    multimap(const multimap& x);
    explicit multimap(const Allocator& alloc);
    multimap(const Compare& comp, const Allocator& alloc);
    multimap(const multimap& x, const Allocator& alloc);
    multimap(initializer_list<value_type> init, const Compare& comp = Compare(), const Allocator& alloc = Allocator());
```

```cpp
template <class InputIterator>
multimap(InputIterator first, InputIterator last, const Compare& comp, const Allocator& a)
    : multimap(first, last, comp, a) {}
multimap(initializer_list<value_type> il, const Compare& comp, const Allocator& a)
    : multimap(il, comp, a) {}
~multimap();
multimap& operator=(const multimap& x);
multimap& operator=(const multimap& x) noexcept(allocator_traits<InputIterator>::is_always_equal);
multimap& operator=(initializer_list<value_type>);
allocator_type get_allocator() const;
```

```cpp
iterator begin() noexcept;
const_iterator begin() const noexcept;
iterator end() noexcept;
const_iterator end() const noexcept;
reverse_iterator rbegin() const noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() const noexcept;
const_reverse_iterator rend() const noexcept;
```

```cpp
const_iterator begin() const noexcept;
const_iterator end() const noexcept;
const_iterator rbegin() const noexcept;
const_iterator rend() const noexcept;
```

```cpp
const_iterator begin() const;
const_iterator end() const;
reverse_iterator rbegin()

rend() const;
```

```cpp
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
```

# 26.4.5 modifiers

```cpp
template <class... Args> iterator insert(Args&&... args);
template <class... Args> iterator insert(const iterator hint, Args&&... args);
iterator insert(value_type x);
iterator insert(const value_type& x);
template <class P> iterator insert(P&& x);
iterator insert(const const_iterator position, P&& x);
iterator insert(const const_iterator position, const value_type& x);
template <class P> iterator insert(const const_iterator position, P&& x);
template <class InputIterator>
void insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type> last);
```

```cpp
node_type extract(const const_iterator position);
node_type extract(const key_type& x);
iterator insert(node_type& nh);
iterator insert(const const_iterator hint, node_type& nh);
```

```cpp
iterator erase(const const_iterator position);
iterator erase(const const_iterator position);
size_type erase(const key_type& x);
```

# 26.4.5.1

```cpp
iterator erase(const const_iterator first, const const_iterator last);
void swap(multimap&) noexcept(allocator_traits<Allocator>::is_always_equal && is_not_throw_swappable_v<Compare>);
clear() noexcept;
```

```cpp
template<class C2>
void merge(multimap<Key, T, C2, Allocator>&& source);
template<class C2>
void merge(multimap<Key, T, C2, Allocator>&& source);
template<class C2>
void merge(map<Key, T, C2, Allocator>&& source);
```

```cpp
// observers:
key_compare key_comp() const;
value_compare value_comp() const;
```

```cpp
// map operations:
iterator find(const key_type& x);
const_iterator find(const key_type& x) const;
template <class K> iterator find(const K& x);
template <class K> iterator find(const K& x) const;
```

```cpp
size_type count(const key_type& x);
template <class K> size_type count(const K& x) const;
```

```cpp
iterator lower_bound(const key_type& x);
const_iterator lower_bound(const key_type& x) const;
template <class K> iterator lower_bound(const K& x);
template <class K> iterator lower_bound(const K& x) const;
```

```cpp
iterator upper_bound(const key_type& x);
const_iterator upper_bound(const key_type& x) const;
template <class K> iterator upper_bound(const K& x);
template <class K> iterator upper_bound(const K& x) const;
```

```cpp
pair<iterator, iterator> equal_range(const key_type& x);
pair<const_iterator, const_iterator> equal_range(const key_type& x) const;
template <class K> pair<iterator, iterator> equal_range(const K& x);
template <class K> pair<const_iterator, const_iterator> equal_range(const K& x) const;
```
