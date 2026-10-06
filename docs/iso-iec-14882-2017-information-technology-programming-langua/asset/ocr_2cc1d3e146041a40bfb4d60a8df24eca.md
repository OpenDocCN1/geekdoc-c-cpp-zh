# ISO/IEC 14882:2017(E)

```
// 24.6.6.2. construct/copy/destroy
set() : set(Compare()) { }
explicit set(const Compare& comp, const Allocator& alloc = Allocator());
template <class InputIterator>
set(InputIterator first, InputIterator last, const Compare& comp = Compare(), const Allocator& alloc = Allocator());
set(const set& x);
set(set& x);
explicit set(const Allocator& alloc);
set(const set& set, const Allocator& alloc);
set(const set& set, const Allocator& alloc);
set(initializer_list<value_type> init, const Compare& comp = Compare(), const Allocator& alloc = Allocator());
template <class InputIterator>
set(InputIterator first, InputIterator last, const Allocator& alloc) 
    : set(first, last, comp, alloc) { }
set(initializer_list<value_type> il, const Allocator& alloc) 
    : set(il, alloc) { }
operator=(const set& x)
operator=(const set& x)
noexcept(allocator_traits<Allocator>::is_always_equal<Compare> && is_nothrow_move_assignable<Compare&>)
operator=(initializer_list<value_type> const noexcept)
allocator_type get_allocator() const noexcept;
```

+   // iterators:
iterator begin() noexcept;
const_iterator begin() const noexcept;
iterator end() noexcept;
const_iterator end() const noexcept;

reverse_iterator begin() noexcept;
const_reverse_iterator begin() const noexcept;
reverse_iterator rend() noexcept;
const_reverse_iterator rend() const noexcept;

const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
const_reverse_iterator crbeg() const noexcept;
const_reverse_iterator crend() const noexcept;

+   // capacity:
bool empty() const noexcept;
size_type size() const noexcept;
size_type max() const noexcept;

+   // modifiers:
template <class... Args>
template <class... Args>
pair_iterator(Args& args, Args& hint(const Args&... args) : args...);
template <class... Args>
pair_iterator insert(const_iterator position, const Args&... args);
pair_iterator, bool insert(const value_type& x);
iterator insert(const_iterator position, const value_type& x);
iterator insert(const_iterator position, value_type, value_type& x);