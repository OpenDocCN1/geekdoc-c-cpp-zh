# ISO/IEC 14882:2017(E)

note|
[Note: If normalization (30.10.4) is needed to ensure consistent matching of elements, apply lexically-normal() to *this, base, or both. — end note|

path lexically_proximate(const path& base) const;
Returns: If the value of lexically_relative(base) is not an empty path, return it. Otherwise return *this;

[Note: If linking semantics are desired, use the operational function proximate(). — end note|
[Note: If normalization (30.10.4) is needed to ensure consistent matching of elements, apply lexically-normal() to *this, base, or both. — end note|

# 30.10.8 path iterators [fs.path.iter]

+   1 Iterators iterate over the pathname in the generic format (30.10.8.1).
2 A :path::iterator satisfies all the requirements of a bidirectional iterator (27.2.6) except, for dereferenceable iterators and b of type path::iterator a ==, there is no requirement that a and b are bound to the same object. Its value_type is path.
3 Calling any non-const member of path object invalidates all iterators referring to elements of that object.

+   4 For the elements of pathname in the generic format, the forward traversal order is as follows:
The root-name element, if present.
The root-directory element, if present. [Note: The generic format is required to ensure lexicographical comparison works. — end note|
Each successive filename, if present.
An empty element, if a trailing non-root directory-separator is present.

+   5 The backward traversal order is the reverse of forward traversal.

```
iterator begin() const;
Returns: An iterator for the first element in the traversal list above. If no elements are present, the end iterator.
iterator end() const;
Returns: The iterator.
```

# 30.10.8.6 path non-const members [fs.path.nonmember]

```
void swap(const path& lhs, path& rhs) noexcept;
Effects: Equivalent to: lhs::swap(rhs);
```

```
size_t hash_value(const path& p) noexcept;
Returns: A hash value for the path p. For two paths, p1 == p2 then hash_value(p1) == hash_value(p2).
```

```
bool operator<(const path& lhs, const path& rhs) noexcept;
Returns: lhs.compare(rhs) < 0.
```