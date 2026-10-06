# ISO/IEC 14882:2017(E)

# 26.3.8.2 deque constructors, copy, and assignment [deque.cons]

```
explicit deque(const Allocator&);
```

+   1 Effects: Constructs an empty deque, using the specified allocator.
2 Complexity: Constant.

```
deque(size_type n, const Allocator& n = Allocator());
```

+   3 Effects: Constructs a deque with n default-inserted elements using the specified allocator.
4 Requires: T shall be DefaultInsertable into *this.
5 Complexity: Linear in n.

```
deque(size_type n, const T& value, const Allocator& n = Allocator());
```

+   6 Effects: Constructs a deque with copies of value, using the specified allocator.
7 Requires: T shall be CopyInsertable into *this.
8 Complexity: Linear in n.

```
template <class InputIterator>
deque(InputIterator first, InputIterator last, const Allocator& n = Allocator());
```

+   9 Effects: Constructs a deque equal to the range (first, last), using the specified allocator.
10 Complexity: Linear in distance(first, last).

# 26.3.8.3 deque capacity [deque.capacity]

```
void resize(size_type sz);
```

+   1 Effects: If sz < size(), erases the last size() - sz elements from the sequence. Otherwise, appends sz - size() default-inserted elements to the deque.
2 Requires: T shall be Moveable and DefaultInsertable into *this.

```
void resize(size_type sz, const T& c);
```

+   3 Effects: If sz < size(), erases the last size() - sz elements from the sequence. Otherwise, appends sz - size() copies of c to the sequence.
4 Requires: T shall be Insertable into *this.

```
void shrink_to_fit();
```

+   5 Requires: T shall be Moveable into *this.
6 Effects: shrink_to_fit is a non-binding request to reduce memory but does not change the size of the sequence. [Note: The request is non-binding to allow latitude for implementation-specific optimizations. -- note] If an exception is thrown other than by the constructor of a nonCopyInsertable T there are no effects.
7 Complexity: Linear in the sequence.
8 Remarks: shrink_to_fit invalid all references, pointers, and iterators referring to the elements in the sequence as the past-the-end iterator.