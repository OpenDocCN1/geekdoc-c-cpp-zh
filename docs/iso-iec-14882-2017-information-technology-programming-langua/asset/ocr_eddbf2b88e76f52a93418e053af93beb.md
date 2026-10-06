# ISO/IEC 14882:2017(E)

```
vector& operator=(initializer_list<T>);
template <class InputIterator>
void assign(InputIterator first, InputIterator last);
void assign(size_type n, const T & u);
void assign(initializer_list<T>);
allocator_type get_allocator() const noexcept;
```

```
// iterators:
iterator begin() noexcept;
const_iterator begin() noexcept;
iterator end() noexcept;
const_iterator end() noexcept;
reverse_iterator rbegin() noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() noexcept;
const_reverse_iterator rend() const noexcept;
```

```
const_iterator cbegin() const noexcept;
const_iterator cend() const noexcept;
const_reverse_iterator crbeg() const noexcept;
const_reverse_iterator crend() const noexcept;
```

```
// 26.3.11.3, capacity
```

```
bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;
size_type capacity() const noexcept;
void resize(size_type sz);
void resize(size_type sz, const T & c);
void resize(size_type n);
void shrink_to_fit();
```

```
// 26.3.11.4, data access
```

```
reference operator[](size_type n);
const_reference operator[](size_type n) const;
const_reference at(size_type n) const;
reference front();
reference back();
const_reference front() const noexcept;
const_reference back() const noexcept;
```

```
// 26.3.11.5, modifiers
```

```
template <class... Args> Args& emplace_back(Args&&... args);
void push_back(const T& x);
void push_back(T&& x);
void pop_back();
```

```
template <class... Args> iterator insert(const_iterator position, Args&&... args);
iterator insert(const_iterator position, T&& x);
```