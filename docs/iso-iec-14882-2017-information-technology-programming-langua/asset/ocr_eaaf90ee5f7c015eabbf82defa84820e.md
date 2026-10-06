# ISO/IEC 14882:2017(E)

```
list(InputIterator first, InputIterator last, const Allocator& = Allocator());
list(const list& x);
list(list& x);
list(const list&, const Allocator&);
list(list&, const Allocator&);
list(initializer_list<T>, const Allocator& = Allocator());
-list();
list& operator=(const list& x);
list& operator=(list& x)
noexcept(alloc_traits<Allocator>::is_always_equal(value));
list& operator=(initializer_list<T>);

template <class InputIterator>
void assign(InputIterator first, InputIterator last);
void assign(size_type n, const T& t);
void assign(initializer_list<T>);
allocator_type get_allocator() const noexcept;

// iterators:
iterator begin() const noexcept;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator end() const noexcept;
reverse_iterator rbegin() const noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() const noexcept;
const_reverse_iterator rend() const noexcept;

const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
const_reverse_iterator cr不起() const noexcept;
const_reverse_iterator crend() const noexcept;

// 36.3.10.4. capacity
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
void resize(size_type sz);
void resize(size_type sz, const T& c);\n
// element access:
reference front() const;
const_reference front() const;
reference back() const;
const_reference back() const;

// 36.3.10.4. modifiers
template <class... Args> reference emplace_front(Args&&... args) noexcept;
template <class... Args> reference emplace_back(Args&&... args) noexcept;
void push_front(const T& x);
void push_front(T&& x);
void pop_front();
void push_back(const T& x);
void push_back(T&& x);
void pop_back();();
```

§ 26.3.10.1 © ISO/IEC 2017 - All rights reserved 883