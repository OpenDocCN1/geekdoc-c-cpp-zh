# ISO/IEC 14882:2017(E)

Otherwise inserts an object of type value_type constructed with piecewise_construct, forward_as_tuple(std::move(k)), forward_as_tuple(std::forward<Args>(args)...).

Returns in the first overload, the bool component of the returned pair is true if and only if the insertion took place. The returned iterator points to the map element which is equivalent to k.

Complexity: The same as emplace_hint, respectively.

```
template <class M>
iterator insert_assign(const key_type& k, M& obj);
template <class M>
iterator insert_or_assign(const iterator, const key_type& k, M& obj);
```

Requires: is_assignable<vcapped_type, M> shall be true. value_type shall be Emplace-Constructible into map from move(k). forward(obj).

Effects: If the map already contains an element e equivalent to k, assigns std::forward<Args>(obj) to e. Otherwise inserts an object of type value_type constructed with std::forward<Args>(obj).

Returns in the first overload, the bool component of the returned pair is true if and only if the insertion took place. The returned iterator points to the map element which is equivalent to k.

Complexity: The same as emplace_hint, respectively.

```
template <class M>
iterator insert_or_assign(const key_type& k, M& obj);
template <class M>
iterator insert_or_assign(const iterator, const key_type& k, M& obj);
```

Requires: is_assignable<vcapped_type, M> shall be true. value_type shall be Emplace-Constructible into map from move(k). forward(obj).

Effects: If the map already contains an element e equivalent to k, assigns std::forward<Args>(obj) to e. Otherwise inserts an object of type value_type constructed with std::forward<Args>(obj).

Returns in the first overload, the bool component of the returned pair is true if and only if the insertion took place. The returned iterator points to the map element which is equivalent to k.

Complexity: The same as emplace_hint, respectively.

# 26.4.5 map specialized algorithms [map.special]

```
template <class Key, class T, class Compare, class Allocator>
void swap(map<Key, T, Compare, Allocator>& x,
       map<Key, T, Compare, Allocator>& y)
       except(noexcept(x.swap(y)));
```

Effects: As by x.swap(y).

# 26.4.5 Class template multimap [multimap.overview]

# 26.4.5.1 Class template multimap overview

+   imap is an associative container that supports keys (possibly containing multiple copies of the same key value) and provides fast retrieval of another type T based on the keys. The multimap supports bidirectional iterators.

+   A multimap satisfies all the requirements of a container of a reversible container (26.2.6), of an associative container (26.2.6), and an allocator-aware container (Table 86). A multimap also provides most operations described in 26.2.6 for equal keys. This means that a multimap supports the a_eq equation