# ISO/IEC 14882:2020(E)

```
} else {
    ++i;
}
}
return original_size - c.size();
```

# 22.5.6 Class template unordered_set [unord.set]

# 22.5.6.1 Overview [unord.set.overview]

1 An unordered_set is an unordered associative container that supports unique keys (an unordered_set contains at most one of each key value) and in which the elements’ keys are the elements themselves. The unordered_set class supports forward iterators.

2 An unordered_set meets all of the requirements of a container, of an unordered associative container, and of an allocator-aware container (Table 76). It provides the operations described in the preceding requirements table for unique keys; that is, an unordered_set supports the a_uniq operations in that table, not the a_eq operations. For an unordered_set<Key> the key type and the value type are both Key. The iterator and const_iterator types are both constant iterator types. It is unspecified whether they are the same type.

3 Subclause 22.5.6 only describes operations on unordered_set that are not described in one of the requirement tables, or for which there is additional semantic information.

```
namespace std {
  template<class Key,
          class Hash = hash<Key>,
          class Pred = equal_to<Key>,
          class Allocator = allocator<Key>>
  class unordered_set {
  public:
    // types
    using key_type = Key;
    using value_type = Key;
    using hasher = Hash;
    using key_equal = Pred;
    using allocator_type = Allocator;
    using pointer = typename allocator_traits<Allocator>::pointer;
    using const_pointer = typename allocator_traits<Allocator>::const_pointer;
    using reference = value_type&;
    using const_reference = const value_type&;
    using size_type = implementation-defined; // see 22.2
    using difference_type = implementation-defined; // see 22.2
    using iterator = implementation-defined; // see 22.2
    using const_iterator = implementation-defined; // see 22.2
    using local_iterator = implementation-defined; // see 22.2
    using const_local_iterator = implementation-defined; // see 22.2
    using node_type = unspecified;
    using insert_return_type = insert-return-type<iterator, node_type>;
    // 22.5.6.2, construct/copy/destroy
    unordered_set();
    explicit unordered_set(size_type n,
                           const hasher& hf = hasher(),
                           const key_equal& eql = key_equal(),
                           const allocator_type& a = allocator_type());
    template<class InputIterator>
      unordered_set(InputIterator f, InputIterator l,
                    size_type n = see below,
                    const hasher& hf = hasher(),
                    const key_equal& eql = key_equal(),
                    const allocator_type& a = allocator_type());
    unordered_set(const unordered_set&);
    unordered_set(unordered_set&&);
    explicit unordered_set(const Allocator&);
    unordered_set(const unordered_set&, const Allocator&);
```