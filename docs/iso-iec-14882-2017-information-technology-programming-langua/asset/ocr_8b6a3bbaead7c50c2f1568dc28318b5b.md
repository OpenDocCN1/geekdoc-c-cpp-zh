# ISO/IEC 14882:2017(E)

```
using iterator_category = output_iterator_tag;
using value_type = void;
using difference_type = void;
using pointer = void;
using reference = void;
```

```
explicit raw_storage_iterator(OutputIterator x);
raw_storage_iterator& operator();
raw_storage_iterator& operator=(const T& element);
raw_storage_iterator& operator=(T&& element);
raw_storage_iterator& operator++();
raw_storage_iterator operator++(int);
base() const;
}
```

raw_storage_iterator is provided to enable algorithms to store their results in uninitialized memory. The template parameter OutputIterator is required to have its operator* return an object for which operator* is defined and returns a pointer to T, and is also required to satisfy the requirements of an output iterator [27.2.4].

```
explicit raw_storage_iterator(OutputIterator x);
```

Effects: Initializes the iterator to point to the same value to x points.

```
raw_storage_iterator& operator() const;
```

```
raw_storage_iterator& operator=(const T& element);
```

Requires: T shall be CopyConstructible.

```
raw_storage_iterator& operator=(T&& element);
```

Effects: Constructs a value from element at the location to which the iterator points.

Returns: A reference to the iterator.

```
raw_storage_iterator& operator++() const;
```

Requires: T shall be MoveConstructible.

Effects: Constructs a value from std::move(element) at the location to which the iterator points.

Returns: A reference to the iterator.

```
raw_storage_iterator operator++(int);
```

Effects: Pre-increment: advances the iterator and returns a reference to the updated iterator.

Effects: Post-increment: advances the iterator and returns the old value of the iterator.

```
OutputIterator base() const;
```

Returns: An iterator of type OutputIterator that points to the same value as *this points to.

# D.11 Temporary buffers [depr.temporary.buffer]

The header <memory> has the following additions:

```
namespace std {
  template <class T >
```

§ D.11

©ISO/IEC 2017 – All rights reserved

1473