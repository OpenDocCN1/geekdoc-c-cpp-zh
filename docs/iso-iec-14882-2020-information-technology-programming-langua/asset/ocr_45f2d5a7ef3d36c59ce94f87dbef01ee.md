# ISO/IEC 14882:2020(E)

```
// 22.4.7, class template multiset
template<class Key, class Compare = less<Key>, class Allocator = allocator<Key>>
    class multiset;

template<class Key, class Compare, class Allocator>
    bool operator==(const multiset<Key, Compare, Allocator>& x,
                    const multiset<Key, Compare, Allocator>& y);
template<class Key, class Compare, class Allocator>
    synth-three-way-result<Key> operator<=>(const multiset<Key, Compare, Allocator>& x,
                                            const multiset<Key, Compare, Allocator>& y);

template<class Key, class Compare, class Allocator>
    void swap(multiset<Key, Compare, Allocator>& x,
              multiset<Key, Compare, Allocator>& y)
        noexcept(noexcept(x.swap(y)));

template<class Key, class Compare, class Allocator, class Predicate>
    typename multiset<Key, Compare, Allocator>::size_type
        erase_if(multiset<Key, Compare, Allocator>& c, Predicate pred);

namespace pmr {
    template<class Key, class Compare = less<Key>>
        using set = std::set<Key, Compare, polymorphic_allocator<Key>>;

    template<class Key, class Compare = less<Key>>
        using multiset = std::multiset<Key, Compare, polymorphic_allocator<Key>>;
}
```

# 22.4.4 Class template map [map]

# 22.4.4.1 Overview [map.overview]

1 A map is an associative container that supports unique keys (contains at most one of each key value) and provides for fast retrieval of values of another type T based on the keys. The map class supports bidirectional iterators.

2 A map meets all of the requirements of a container, of a reversible container (22.2), of an associative container (22.2.6), and of an allocator-aware container (Table 76). A map also provides most operations described in 22.2.6 for unique keys. This means that a map supports the a_unique operations in 22.2.6 but not the a_eq operations. For a map<Key,T> the key_type is Key and the value_type is pair<const Key,T>. Descriptions are provided here only for operations on map that are not described in one of those tables or for operations where there is additional semantic information.

```
namespace std {
    template<class Key, class T, class Compare = less<Key>,
             class Allocator = allocator<pair<const Key, T>>>
    class map {
    public:
        // types
        using key_type            = Key;
        using mapped_type         = T;
        using value_type          = pair<const Key, T>;
        using key_compare         = Compare;
        using allocator_type      = Allocator;
        using pointer             = typename allocator_traits<Allocator>::pointer;
        using const_pointer       = typename allocator_traits<Allocator>::const_pointer;
        using reference           = value_type&;
        using const_reference     = const value_type&;
        using size_type           = implementation-defined; // see 22.2
        using difference_type     = implementation-defined; // see 22.2
        using iterator            = implementation-defined; // see 22.2
        using const_iterator      = implementation-defined; // see 22.2
        using reverse_iterator    = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;
```