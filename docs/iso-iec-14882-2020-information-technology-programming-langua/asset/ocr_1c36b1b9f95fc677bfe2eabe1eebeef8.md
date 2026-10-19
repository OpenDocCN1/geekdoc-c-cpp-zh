# ISO/IEC 14882:2020(E)

Table 81: Unordered associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
|---|---|---|---|
| a.reserve(n) | void | Same as a.rehash(ceil(n / a.max_load_factor())). | Average case linear in a.size(), worst case quadratic. |

12 Two unordered containers a and b compare equal if a.size() == b.size() and, for every equivalent-key group [Ea1, Ea2) obtained from a.equal_range(Ea1), there exists an equivalent-key group [Eb1, Eb2) obtained from b.equal_range(Ea1), such that is_permutation(Ea1, Ea2, Eb1, Eb2) returns true. For unordered_set and unordered_map, the complexity of operator== (i.e., the number of calls to the == operator of the value_type, to the predicate returned by key_eq(), and to the hasher returned by hash_function()) is proportional to N in the average case and to N² in the worst case, where N is a.size(). For unordered_multiset and unordered_multimap, the complexity of operator== is proportional to Σ E_i² in the average case and to N² in the worst case, where N is a.size(), and E_i is the size of the iᵗʰ equivalent-key group in a. However, if the respective elements of each corresponding pair of equivalent-key groups Ea_i and Eb_i are arranged in the same order (as is commonly the case, e.g., if a and b are unmodified copies of the same container), then the average-case complexity for unordered_multiset and unordered_multimap becomes proportional to N (but worst-case complexity remains O(N²), e.g., for a pathologically bad hash function). The behavior of a program that uses operator== or operator!= on unordered containers is undefined unless the Pred function object has the same behavior for both containers and the equality comparison function for Key is a refinement²³⁰ of the partition into equivalent-key groups produced by Pred.

13 The iterator types iterator and const_iterator of an unordered associative container are of at least the forward iterator category. For unordered associative containers where the key type and value type are the same, both iterator and const_iterator are constant iterators.

14 The insert and emplace members shall not affect the validity of references to container elements, but may invalidate all iterators to the container. The erase members shall invalidate only iterators and references to the erased elements, and preserve the relative order of the elements that are not erased.

15 The insert and emplace members shall not affect the validity of iterators if (N+n) <= z * B, where N is the number of elements in the container prior to the insert operation, n is the number of elements inserted, B is the container's bucket count, and z is the container's maximum load factor.

16 The extract members invalidate only iterators to the removed element, and preserve the relative order of the elements that are not erased; pointers and references to the removed element remain valid. However, accessing the element through such pointers and references while the element is owned by a node_type is undefined behavior. References and pointers to an element obtained while it is owned by a node_type are invalidated if the element is successfully inserted.

17 The member function templates find, count, equal_range, and contains shall not participate in overload resolution unless the qualified-ids Pred::is_transparent and Hash::is_transparent are both valid and denote types (13.10.3).

18 A deduction guide for an unordered associative container shall not participate in overload resolution if any of the following are true:

+   (18.1) — It has an InputIterator template parameter and a type that does not qualify as an input iterator is deduced for that parameter.
+   (18.2) — It has an Allocator template parameter and a type that does not qualify as an allocator is deduced for that parameter.
+   (18.3) — It has a Hash template parameter and an integral type or a type that qualifies as an allocator is deduced for that parameter.
+   (18.4) — It has a Pred template parameter and a type that qualifies as an allocator is deduced for that parameter.

230) Equality comparison is a refinement of partitioning if no two objects that compare equal fall into different partitions.