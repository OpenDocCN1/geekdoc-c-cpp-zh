```
```cpp
#include <initializer_list>
#include <iostream>
#include <iterator>
#include <stdexcept>
#include <utility>

// class template ConstIterator for a MyArray const iterator
template <typename T>
class ConstIterator {
public:
    // public iterator nested type names
    using iterator_category = std::bidirectional_iterator_tag;
    using difference_type = std::ptrdiff_t;
    using value_type = T;
    using pointer = const value_type*;
    using reference = const value_type&;

    // default constructor
    ConstIterator() = default;

    // initialize a ConstIterator with a pointer into a MyArray
    ConstIterator(pointer p) : m_ptr{p} {}

    // OPERATIONS ALL ITERATORS MUST PROVIDE
    // increment the iterator to the next element and
    // return a reference to the iterator
    ConstIterator& operator++() noexcept {
        ++m_ptr;
        return *this;
    }

    // increment the iterator to the next element and
    // return the iterator before the increment
    ConstIterator operator++(int) noexcept {
        ConstIterator temp{*this};
        ++(*this);
        return temp;
    }

    // OPERATIONS INPUT ITERATORS MUST PROVIDE
    // return a const reference to the element m_ptr points to
    reference operator*() const noexcept {return *m_ptr;}

    // return a const pointer to the element m_ptr points to
    pointer operator->() const noexcept {return m_ptr;}

    // <=> operator automatically supports equality/relational operators.
    // Only == and != are needed for bidirectional iterators.
    // This implementation would support the <, <=, > and >= required
    // by random-access iterators.
    auto operator<=>(const ConstIterator& other) const = default;
};
```
```

**Fig. 15.11** | Class template MyArray with custom iterators implemented by class templates ConstIterator and Iterator—class ConstIterator. (Part 2 of 3.)