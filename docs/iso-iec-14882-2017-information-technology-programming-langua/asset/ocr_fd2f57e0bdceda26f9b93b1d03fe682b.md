# ISO/IEC 14882:2017(E)

```
explicit multiset(const Compare& comp, const Allocator& alloc = Allocator());
template <class Iterator>
multiset(InputIterator first, InputIterator last,
    const Compare& comp = Compare(),
    const Allocator& alloc = Allocator());
multiset(const Compare& comp);
multiset(multiset& x);
explicit multiset(const Allocator& alloc);
multiset(const multiset& x, const Allocator& alloc);
multiset(multiset& x, const Allocator& alloc);
multiset(initializer_list<value_type> it, const Compare& comp = Compare(),
    const Allocator& alloc = Allocator());
template <class Iterator>
multiset(InputIterator first, InputIterator last, const Allocator& alloc)
    : multiset(first, last, Compare(), alloc)
multiset(initializer_list<value_type> il, const Allocator& alloc)
    : multiset(il, il, Compare(), alloc)
multiset& operator(const Compare& x)
multiset& operator(const multiset& x)
noexcept(allocator_traits<Allocator>::is_always_equal == V &&
    is_throw_move_assignable<VCompare>);
multiset& operator(initializer_list<value_type>);
alocator_type get_allocator() const noexcept;
```

// iterators:

```
const_iterator begin() const noexcept;
const_iterator begin() const noexcept;
const_iterator end() const noexcept;
const_iterator end() const noexcept;
```

reverse_iterator:

```
reverse_iterator begin() const noexcept;
const_reverse_iterator begin() const noexcept;
reverse_iterator end() const noexcept;
const_reverse_iterator end() const noexcept;
```

// capacity:

```
const_iterator begin() const noexcept;
const_iterator end() const noexcept;
const_reverse_iterator begin() const noexcept;
const_reverse_iterator end() const noexcept;
```

// modifiers:

```
bool empty() const noexcept;
size_type size(size_type) const noexcept;
size_type max_size(size_type) const noexcept;
```

```
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