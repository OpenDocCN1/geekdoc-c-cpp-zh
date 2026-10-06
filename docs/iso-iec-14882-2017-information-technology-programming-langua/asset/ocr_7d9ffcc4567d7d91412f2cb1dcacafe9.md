# ISO/IEC 14882:2017(E)

```
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
unordered_map& operator=(const unordered_map&)
const allocator_traits<Allocator>::is_equal::value &&
    is_throw_move_assignable<VPred> &&
unordered_map& operator(initializer_list<Value> type);
allocator_type get_allocator() const noexcept;

// Iterators:
```

```
iterator;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator begin() const noexcept;
const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
```

Appendix:

```
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
```

```
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

```
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

©ISO/IEC 2017 - All rights reserved

929