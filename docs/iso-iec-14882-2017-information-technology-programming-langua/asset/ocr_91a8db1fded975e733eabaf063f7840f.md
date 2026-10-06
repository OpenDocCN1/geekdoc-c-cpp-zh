# ISO/IEC 14882:2017(E)

object comp, comp(k1, k2) == false && comp(k2, k1) == false. For any two k1 and k2 in the same container, comp(k1, k2) should always return the same value.

+   An associative container stores unique keys it may contain at most one element for each key. Otherwise, it supports equivalent keys. The set and map classes store unique keys; the multiset and multimap classes store equivalent keys. For multiset and multimap, insert, erase, and preserve the relative order of equivalent keys.

+   For set and multiset the value type is the same as the key type. For map and multimap it is equal to pair<const Key, T>.

+   iterator of an associative container is of the bidirectional type. If the value type is the same as the key type, both iterator and const_iterator are same iterators. It is unspecified whether iterator and const_iterator are the same. [Note: const_iterator have identical semantics in this case, and iterator is convertible to const_iterator. Users can violating the definition rules by using const_iterator in their function parameters — end note]

+   The associative containers meet all the requirements of Allocator-aware (26.2.1), except for map and multimap, the requirements of value_type in Table 83 apply to key type and mapped_type. [Note: In some cases, key type and mapped_type are required to be Copyable even though the associated value_type, pair<const key_type, mapped_type>, is not Copyable.— end note]

In Table 90, X associative container with type X (Table 80), demands a value of type X, a demands a value of type with no declared, a unique of type X when X supports unique keys, a_eq of the value of type X when X supports unique keys, a_trans implicitly convertible to value_type, [1, j) demands when the qualified-if X:key_compare::is_transient is valid and demands type (17.8.2), and i demands input iterators which refer to elements [q1, q) demands a valid range, p demands a valid constant iterator to a. q demands a value dereferable iterator to a. r demands a value dereferable range to. s designated value of type X:key_compare: a demands a value such that a is partitioned (28.7) with respect to (cr, kl), which is the key value of e and e in a: kl is a value such that a is partitioned with respect to (cr, ke) and l(ke, r): c(ke, r) with c(fr, r) implying! c(ke, r). A demands the storage allocator of a, and nh demands a non-convertible value of type X: node_type. of type X:key_compare: a demands a possibly constant value of type X:key_compare: kl demands a value such that a is a value such that a is partitioned with a value that is partitioned with (cr, ke) and l(ke, r): c(ke, r) with c(fr, r) implying! c(ke, r). A demands the storage allocator of a, and nh demands a non-convertible value of type X: node_type.

# Table 90 Associative container requirements (in addition to)

| Expression | Return type | Complexity |
|---|---|--|
| X::key_type | Key pre-/post-condition | compile time |
| X::mapped_ | T type (map and multimap only) | compile time |
| X::value_ | Key type (set and multiset only) Requires: value_type is Erasable from X | compile time |

§ 26.2.6 © ISO/IEC 2017 All rights reserved 842