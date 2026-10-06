# ISO/IEC 14882:2017(E)

```
bool operator===(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
bool operator<=(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
bool operator!=(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
bool operator>(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
bool operator>=(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
bool operator<=(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
bool operator>=(const multiset<Key, Compare, Allocator>& x,
   const multiset<Key, Compare, Allocator>& y);
template <class Key, class Compare, class Allocator>
void swap(multiset<Key, Compare, Allocator>& x,
   multiset<Key, Compare, Allocator>& y)
   noexcept(x.swap(y));
```

```
namespace pmr {
template <class Key, class Compare = less<Key>>
using set = std::set<Key,
  polymorphic_allocator<Key>>;

template <class Key, class Compare = less<Key>>
using multiset = multiset<Key, Compare,
  polymorphic_allocator<Key>>;
}
```

# 26.4.4 Class template map [map]

# 26.4.4.1 Class template map overview [map.overview]

A map is an associative container that contains unique keys (contains at most one of key value) and provides for retrieval of values of another type T based on the keys. The map classes support bidirectional iterators.

A multiset satisfies all the requirements of a container (26.2), and of an associative container (Table 86). A map also provides most operations described in 26.2.6 for unique keys. This means that a map supports the a_uniq operations in 26.2.6 but not the a_eq operations. For a map<Key,T>, the key_type is Key and the value_type is pair<const Key,T>. Descriptions are provided here for operations on map that are not described in these tables or for operations where

```
namespace std {
template <class Key, class T, class Compare = less<Key>,
class Allocator = allocator<const Key, T>>>
class map {
public:
  // types:
  using key_type = Key;
  using value_type = T;
  using pair = pair<const Key, T>;
```