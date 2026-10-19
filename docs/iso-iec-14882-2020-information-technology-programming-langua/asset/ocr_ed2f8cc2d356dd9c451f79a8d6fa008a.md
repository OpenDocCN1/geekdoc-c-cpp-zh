# ISO/IEC 14882:2020(E)

Complexity: Linear in N if the range [first, last) is already sorted using comp and otherwise N log N, where N is last - first.

# 22.4.5.3 Modifiers [multimap.modifiers]

```
template<class P> iterator insert(P&& x);
template<class P> iterator insert(const_iterator position, P&& x);
```

Constraints: is_constructible_v<value_type, P&&> is true.

Effects: The first form is equivalent to return emplace(std::forward<P>(x)). The second form is equivalent to return emplace_hint(position, std::forward<P>(x)).

# 22.4.5.4 Erasure [multimap.erasure]

```
template<class Key, class T, class Compare, class Allocator, class Predicate>
typename multimap<Key, T, Compare, Allocator>::size_type
erase_if(multimap<Key, T, Compare, Allocator>& c, Predicate pred);
```

Effects: Equivalent to:

```
auto original_size = c.size();
for (auto i = c.begin(), last = c.end(); i != last; ) {
  if (pred(*i)) {
    i = c.erase(i);
  } else {
    ++i;
  }
}
return original_size - c.size();
```

# 22.4.6 Class template set [set]

# 22.4.6.1 Overview [set.overview]

1 A set is an associative container that supports unique keys (contains at most one of each key value) and provides for fast retrieval of the keys themselves. The set class supports bidirectional iterators.

2 A set meets all of the requirements of a container, of a reversible container (22.2), of an associative container (22.2.6), and of an allocator-aware container (Table 76). A set also provides most operations described in 22.2.6 for unique keys. This means that a set supports the a_uniq operations in 22.2.6 but not the a_eq operations. For a set<Key> both the key_type and value_type are Key. Descriptions are provided here only for operations on set that are not described in one of these tables and for operations where there is additional semantic information.

```
namespace std {
  template<class Key, class Compare = less<Key>,
    class Allocator = allocator<Key>>
  class set {
  public:
    // types
    using key_type = Key;
    using key_compare = Compare;
    using value_type = Key;
    using value_compare = Compare;
    using allocator_type = Allocator;
    using pointer = typename allocator_traits<Allocator>::pointer;
    using const_pointer = typename allocator_traits<Allocator>::const_pointer;
    using reference = value_type&;
    using const_reference = const value_type&;
    using size_type = implementation-defined; // see 22.2
    using difference_type = implementation-defined; // see 22.2
    using iterator = implementation-defined; // see 22.2
    using const_iterator = implementation-defined; // see 22.2
    using reverse_iterator = std::reverse_iterator<iterator>;
    using const_reverse_iterator = std::reverse_iterator<const_iterator>;
    using node_type = unspecified;
    using insert_return_type = insert-return-type<iterator, node_type>;

```