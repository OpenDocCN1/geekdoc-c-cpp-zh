```
```cpp
{
    return iterator(this->std::vector<std::string *>::begin());
}
inline StringPtr::iterator StringPtr::end()
{
    return iterator(this->std::vector<std::string *>::end());
}
```
```

• All of iterator’s remaining members are public. It’s very easy to implement them, mainly manipulating and dereferencing the available iterator `d_current`. A `RandomAccessIterator` (which is the most complex of iterators) requires a series of operators. They usually have very simple implementations, making them good candidates for inline-members:

+   - `iterator &operator++();` the pre-increment operator:

```
```cpp
inline StringPtr::iterator &StringPtr::iterator::operator++()
{
    ++d_current;
    return *this;
}
```
```

+   - `iterator operator++(int);` the post-increment operator:

```
```cpp
inline StringPtr::iterator StringPtr::iterator::operator++(int)
{
    return iterator(d_current++);
}
```
```

+   - `iterator &operator--();` the pre-decrement operator:

```
```cpp
inline StringPtr::iterator &StringPtr::iterator::operator--()
{
    --d_current;
    return *this;
}
```
```

+   - `iterator operator--(int);` the post-decrement operator:

```
```cpp
inline StringPtr::iterator StringPtr::iterator::operator--(int)
{
    return iterator(d_current--);
}
```
```

+   - `iterator &operator=(iterator const &other);` the overloaded assignment operator. Since iterator objects do not allocate any memory themselves, the default assignment operator can be used.

+   - `bool operator==(iterator const &rhv) const;` testing the equality of two iterator objects:

```
```cpp
inline bool StringPtr::iterator::operator==(iterator const &other) const
{
    return d_current == other.d_current;
}
```
```

+   - `bool operator<(iterator const &rhv) const;` testing whether the left-hand side iterator points to an element of the series located *before* the element pointed to by the right-hand side iterator:

```
```cpp
inline bool StringPtr::iterator::operator<(iterator const &other) const
{
    return d_current < other.d_current;
}
```
```