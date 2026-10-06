# ISO/IEC 14882:2017(E)

const_iterator. Elements can avoid the one-definition rule by always using const_iterator in their function lists. — end note;

The elements of an unordered container are organized into buckets. Keys with the same hash code appear in the same bucket. The number of buckets is automatically increased as elements are added to an unordered container, so that the average number of elements per bucket is kept below a bound. Rehash invalidates iterators, changes ordering between elements, and changes which buckets elements appear in. 

The unordered associative container meets all the requirements of Allocator-aware containers, except for unordered_map and unordered_multimap, the requirements placed on value_type in Table 83 apply to each type and mapped_type. [Example: key_type and mapped_type, pair<const key_type, mapped_type> are required to be Copyable. The value_type of pair<const key_type, mapped_type> is not Copyable. — end note];

+   In Table XI: An unordered associative container classes, a value of type X, a2 denotes a value of type with nodes compatible with type X (Table 89), b denotes a possible const value of type X, a_uniq denotes a value of type X when X supports unique keys, a_eq denotes input iterators that refer to value_type, i, j denotes a value of type X, p and q denote valid constant iterators to a, r denotes a valid constant iterator to (g, q), s denotes value dereferenceable constant, t denotes a value of type X initializer_list<value_type>, t denotes a value of type X:value_type, k denotes a value of type key_type, hf denotes a possible const value of type hasher, eq denotes a possible const value of type key_equal, z denotes a value of type float, and nh denotes a non-const value of type X:node_type.

Table 91 — Unordered associative container requirements (in addition to container)

| Expression | Return type | Assertion/post-condition | Complexity |
|---|---|---||}{
| X::key_type | Key | | compile time |
| X::mapped_type (unordered_map and unordered_multimap only) | T | | compile time |
| X::value_type (unordered_set and unordered_multiset only) | Key | Requires: value_type is Erasable from X | compile time |
| X::value_type (unordered_map and unordered_multimap only) | pair<const Key, T> | Requires: value_type is Erasable from X | compile time |
| X::hasher | Hash | Hash shall be a unary function object such that the exception h(k) has size_t | compile time |

§ 26.2.7 ©ISO/IEC 2017 - All rights reserved 853