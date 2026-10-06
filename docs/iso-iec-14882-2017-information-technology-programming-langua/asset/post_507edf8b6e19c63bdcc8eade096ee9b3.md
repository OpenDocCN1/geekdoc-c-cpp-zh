
# ISO/IEC 14882:2017(E)

```cpp
void swap(vector& x)
noexcept(allocator_traits<Allocator>::propagate_on_container_swap::value ||
    allocator_traits<Allocator>::is_always_equal);
```

Effects: Exchanges the contents and capacity() of *this with that of x.

Complexity: Constant time.

```cpp
void resize(size_type sz);
```

Effects: If sz < size(), erases the last (size() - sz) elements from the sequence. Otherwise, appends
sz - size() - inserted elements to the sequence.

Requires: T shall be MoveInsertable and DefaultInsertable *this.

Remarks: If an exception is thrown other by the move constructor of a non-CopyInsertable T there are no effects.

```cpp
void resize(size_type sz, const T& c);
```

Effects: If sz < size(), erases the last (size() - sz) elements from the sequence. Otherwise, appends
sz - size() copies of c to the sequence.

Requires: T shall be CopyInsertable into *this.

Remarks: If an exception is thrown there are no effects.

## 26.3.11.4 vector data [vector.data]

```cpp
T* data() noexcept;
const T* data() noexcept;
```

Returns: A pointer to that data(), data + size() is a valid range. For a non-empty vector,
data() == addressof(front()).

Complexity: Constant time.

## 26.3.11.5 vector modifiers [vector.modifiers]

```cpp
iterator insert(const_iterator position, const T& x);
iterator insert(const_iterator position, T&& x);
iterator insert(const_iterator position, size_type n, const T& x);
template <class InputIterator>
iterator insert(const_iterator position, InputIterator last);
iterator insert(const_iterator position, initializer_list<InputIterator> last);
```

```cpp
template <class... Args> Args& emplace_back(Args&... args);
template <class... Args> Args& emplace(const_iterator position, Args&&... args);
push_back(const T& x);
push_back(T&& x);
```

Remarks: If the new size is greater than the current size of the data. Reallocation invalidates
the references, pointers, and iterators referring to the sequence. If no reallocation
happens, all the iterators and references before the insertion remain valid. If an exception is
other than the move constructor, assignment operator, or move assignment
of T or by any InputIterator there are no effects. If an exception is thrown while
inserting a single element at the position it is CopyInsertable or is_nothrow_move_constructible-
T is true, there are no effects. Otherwise, the exception is thrown by the move constructor of a
non-CopyInsertable T, the effects are unspecified.

Complexity: The complexity is linear in the number of elements inserted plus the distance to the end of
the vector.

```cpp
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);
pop_back();
```

- Effects: Invalidates iterators and references at or after the point of the erase.
- Complexity: The destructor of T is called the number of times equal to the number of the elements erased, but the assignment operator of T is called the number of times equal to the number of elements in the vector after the erased elements.
- Throws: Unless an exception is thrown by the assignment operator or move assignment operator T.

## 26.3.11.6 vector specialized algorithms [vector.special]

```cpp
template<class T, class Allocator>
void swap(vector<T, Allocator>& x, vector<T, Allocator>& y)
noexcept(x.swap(y));
```

- Effects: As if by x.swap(y).

## 26.3.12 class vector<bool> [vector.bool]

- 1 To optimize space allocation, a specialization for bool elements is provided:

```cpp
namespace std {
template <class Allocator>
class vector<bool, Allocator> {
public:
  // types:
  using value_type = bool;
  using allocator_type = Allocator;
  using pointer = implementation-defined;
  using const_pointer = implementation-defined;
  using const_reference = bool;
  using reference_type = implementation-defined; // see 26.2
  using difference_type = implementation-defined; // see 26.2
  using iterator = implementation-defined; // see 26.2
  using const_iterator = implementation-defined; // see 26.2
  using reverse_iterator = std::reverse_iterator<iterator>;
  using const_reverse_iterator = std::reverse_iterator<const_iterator>;

  // bit_reference
  class reference {
    friend class vector;
    friend class const_vector;
public:
    reference(const bool) noexcept;
    operator bool() const noexcept;
    reference& operator=(const bool x) noexcept;
    reference& operator=(const reference& x) noexcept;
    void flip() noexcept; // flips the bit
  };

  // constructor/copy/destroy;
  vector() : vector(Allocator()) {}
  explicit vector(const Allocator& alloc);
  explicit vector(size_type n, const Allocator& alloc);
  vector(size_type n, bool);
```

```cpp
  template<class InputIterator>
  vector(InputIterator first, InputIterator last);
  template<class InputIterator>
  vector(const InputIterator first, InputIterator last);
  template<class InputIterator>
  vector(initializer_list<InputIterator> il);
  template<class InputIterator>
  vector(std::move_iterator<InputIterator> first, std::move_iterator<InputIterator> last);
  template<class InputIterator>
  vector(const move_iterator<InputIterator> first, const move_iterator<InputIterator> last);
  template<class InputIterator>
  vector(const_move_iterator<InputIterator> first, const_move_iterator<InputIterator> last);
  template<class InputIterator>
  vector(const const_move_iterator<InputIterator> first, const const_move_iterator<InputIterator> last);

  template<class Allocator>
  vector(const vector<bool, Allocator>& other);
  template<class Allocator>
  vector(vector<bool, Allocator>&& other);

  template<class InputIterator>
  vector(InputIterator first, const InputIterator last);
  template<class InputIterator>
  vector(const InputIterator first, const InputIterator last);
  template<class InputIterator>
  vector(const InputIterator first, InputIterator last);
  template<class InputIterator>
  vector(InputIterator first, const InputIterator last);

  template<class Allocator>
  vector& operator=(const vector<bool, Allocator>& other);
  template<class Allocator>
  vector& operator=(vector<bool, Allocator>&& other);

  template<class InputIterator>
  void assign(InputIterator first, InputIterator last);
  template<class InputIterator>
  void assign(const InputIterator first, const InputIterator last);
  template<class InputIterator>
  void assign(const InputIterator first, InputIterator last);
  void assign(size_type n, bool b);
  void assign(initializer_list<bool> il);

  operator bool() const noexcept;
  reference& operator=(const bool x) noexcept;
  reference& operator=(const reference& x);
  void flip() noexcept;

  bool empty() const;
  size_type size() const;
  size_type max_size() const;
  void reserve(size_type n);
  void resize(size_type n, bool b);
  void shrink_to_fit();

  reference& operator[](size_type n);
  const reference operator[](size_type n) const;
  const reference at(size_type n) const;
  reference& front();
  const reference& front() const;
  reference& back();
  const reference& back() const;

  iterator begin();
  const_iterator begin();
  iterator end();
  const_iterator end();
  reverse_iterator begin();
  const_reverse_iterator begin();
  reverse_iterator end();
  const_reverse_iterator end();
  reverse_iterator rbegin();
  const_reverse_iterator rbegin();
  reverse_iterator rend();
  const_reverse_iterator rend();

  template<class... Args>
  Args& emplace_back(Args&&... args);
  template<class... Args>
  Args& emplace(const_iterator position, Args&&... args);

  void push_back(const bool& x);
  void push_back(bool&& x);
  void push_back(size_type n);
  void pop_back();
  void erase(const_iterator position);
  void erase(const_iterator first, const_iterator last);

  template<class Allocator>
  void swap(vector<bool, Allocator>& other);
  static void swap(vector<bool, Allocator>& x, vector<bool, Allocator>& y);
};
```

- 1 To optimize space allocation, a specialization for bool elements is provided:
- 2 Unless desired, all operations have the same requirements and semantics as the primary vector, except that operations with the bool value type map in the container storage and allocator_traits (23.10.8) is not used to construct these values.
- 3 There is no requirement that the data be stored as a contiguous allocation of bool values. A space-optimized representation of bits is recommended.
- 4 reference is a class that simulates the behavior of references of a bool vector may appear in the vector<bool>. The conversion function returns true when the bit is set, and false otherwise. The assignment operator sets the bit when the argument is (true) true else otherwise. flip reverses the state of the bit.
- 5 Effects: Replaces each element in the container with its complement.
- 6 static void swap(reference& x, reference& y) noexcept > Effects: Exchanges the contents of x and y as if:
bool b = x;
x = y;
y = b;
- 7 The specialization is enabled (23.14.15).

## 26.4 Associative containers [associative]

## 26.4.1 In general [associative.general]

- The header defines the class templates map and multimap; the header <set> defines the class templates set and multiset.
- The following example-only alias may appear in deduction guides for containers:

```cpp
template<class InputIterator>
using iter_key_t = remove_const_t<typename iterator_traits<InputIterator>::value_type>::first_type; // expression only
template<class InputIterator>
using iter_val_t =
type = typename iterator_traits<InputIterator>::value_type>::second_type; // expression only
```
