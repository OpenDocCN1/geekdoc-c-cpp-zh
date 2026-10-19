
## ISO/IEC 14882:2020(E)

### Table 81: Unordered associative container requirements (in addition to container)

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
|------------|-------------|--------------------------------------|------------|
| a.extract(k) | node_type | Effects: Removes an element in the container with key equivalent to k.<br>Returns: A node_type owning the element if found, otherwise an empty node_type. | Average case 𝒪(1), worst case 𝒪(a.size()). |
| a.extract(q) | node_type | Effects: Removes the element pointed to by q.<br>Returns: A node_type owning that element. | Average case 𝒪(1), worst case 𝒪(a.size()). |
| a.merge(a2) | void | Preconditions: a.get_allocator() == a2.get_allocator().<br>Attempts to extract each element in a2 and insert it into a using the hash function and key equality predicate of a. In containers with unique keys, if there is an element in a with key equivalent to the key of an element from a2, then that element is not extracted from a2.<br>Postconditions: Pointers and references to the transferred elements of a2 refer to those same elements but as members of a. Iterators referring to the transferred elements and all iterators referring to a will be invalidated, but iterators to elements remaining in a2 will remain valid. | Average case 𝒪(N), where N is a2.size(), worst case 𝒪(N*a.size() + N). |
| a.erase(k) | size_type | Effects: Erases all elements with key equivalent to k.<br>Returns: The number of elements erased. | Average case 𝒪(a.count(k)), worst case 𝒪(a.size()). |
| a.erase(q) | iterator | Effects: Erases the element pointed to by q.<br>Returns: The iterator immediately following q prior to the erasure. | Average case 𝒪(1), worst case 𝒪(a.size()). |
| a.erase(r) | iterator | Effects: Erases the element pointed to by r.<br>Returns: The iterator immediately following r prior to the erasure. | Average case 𝒪(1), worst case 𝒪(a.size()). |
| a.erase(q1, q2) | iterator | Effects: Erases all elements in the range [q1, q2).<br>Returns: The iterator immediately following the erased elements prior to the erasure. | Average case linear in distance(q1, q2), worst case 𝒪(a.size()). |
| a.clear() | void | Effects: Erases all elements in the container.<br>Postconditions: a.empty() is true | Linear in a.size(). |
| b.find(k) | iterator; const_iterator for const b. | Returns: An iterator pointing to an element with key equivalent to k, or b.end() if no such element exists. | Average case O(1), worst case O(b.size()). |
| a_tran.find(ke) | iterator; const_iterator for const a_tran. | Returns: An iterator pointing to an element with key equivalent to ke, or a_tran.end() if no such element exists. | Average case O(1), worst case O(a_tran.size()). |
| b.count(k) | size_type | Returns: The number of elements with key equivalent to k. | Average case O(b.count(k)), worst case O(b.size()). |
| a_tran.count(ke) | size_type | Returns: The number of elements with key equivalent to ke. | Average case O(a_tran.count(ke)), worst case O(a_tran.size()). |
| b.contains(k) | bool | Effects: Equivalent to b.find(k) != b.end() | Average case O(1), worst case O(b.size()). |
| a_tran.contains(ke) | bool | Effects: Equivalent to a_tran.find(ke) != a_tran.end() | Average case O(1), worst case O(a_tran.size()). |
| b.equal_range(k) | pair<iterator, iterator>; pair<const_iterator, const_iterator> for const b. | Returns: A range containing all elements with keys equivalent to k. Returns make_pair(b.end(), b.end()) if no such elements exist. | Average case O(b.count(k)), worst case O(b.size()). |
| a_tran.equal_range(ke) | pair<iterator, iterator>; pair<const_iterator, const_iterator> for const a_tran. | Returns: A range containing all elements with keys equivalent to ke. Returns make_pair(a_tran.end(), a_tran.end()) if no such elements exist. | Average case O(a_tran.count(ke)), worst case O(a_tran.size()). |
| b.bucket_count() | size_type | Returns: The number of buckets that b contains. | Constant |
| b.max_bucket_count() | size_type | Returns: An upper bound on the number of buckets that b can ever contain. | Constant |
| b.bucket(k) | size_type | Preconditions: b.bucket_count() > 0. Returns: The index of the bucket in which elements with keys equivalent to k would be found, if any such element existed. Postconditions: The return value shall be in the range [0, b.bucket_count()]. | Constant |
| b.bucket_size(n) | size_type | Preconditions: n shall be in the range [0, b.bucket_count()). Returns: The number of elements in the nᵗʰ bucket. | 𝒪(b.bucket_size(n)) |
| b.begin(n) | local_iterator; const_local_iterator for const b. | Preconditions: n is in the range [0, b.bucket_count()). Returns: An iterator referring to the first element in the bucket. If the bucket is empty, then b.begin(n) == b.end(n). | Constant |
| b.end(n) | local_iterator; const_local_iterator for const b. | Preconditions: n is in the range [0, b.bucket_count()). Returns: An iterator which is the past-the-end value for the bucket. | Constant |
| b.cbegin(n) | const_local_iterator | Preconditions: n shall be in the range [0, b.bucket_count()). Returns: An iterator referring to the first element in the bucket. If the bucket is empty, then b.cbegin(n) == b.cend(n). | Constant |
| b.cend(n) | const_local_iterator | Preconditions: n is in the range [0, b.bucket_count()). Returns: An iterator which is the past-the-end value for the bucket. | Constant |
| b.load_factor() | float | Returns: The average number of elements per bucket. | Constant |
| b.max_load_factor() | float | Returns: A positive number that the container attempts to keep the load factor less than or equal to. The container automatically increases the number of buckets as necessary to keep the load factor below this number. | Constant |
| a.max_load_factor(z) | void | Preconditions: z is positive. May change the container's maximum load factor, using z as a hint. | Constant |
| a.rehash(n) | void | Postconditions: a.bucket_count() >= a.size() / a.max_load_factor() and a.bucket_count() >= n. | Average case linear in a.size(), worst case quadratic. |
| a.reserve(n) | void | Same as a.rehash(ceil(n / a.max_load_factor())). | Average case linear in a.size(), worst case quadratic. |

12 Two unordered containers a and b compare equal if a.size() == b.size() and, for every equivalent-key group [Ea1, Ea2) obtained from a.equal_range(Ea1), there exists an equivalent-key group [Eb1, Eb2) obtained from b.equal_range(Ea1), such that is_permutation(Ea1, Ea2, Eb1, Eb2) returns true. For unordered_set and unordered_map, the complexity of operator== (i.e., the number of calls to the == operator of the value_type, to the predicate returned by key_eq(), and to the hasher returned by hash_function()) is proportional to N in the average case and to N² in the worst case, where N is a.size(). For unordered_multiset and unordered_multimap, the complexity of operator== is proportional to Σ E_i² in the average case and to N² in the worst case, where N is a.size(), and E_i is the size of the iᵗʰ equivalent-key group in a. However, if the respective elements of each corresponding pair of equivalent-key groups Ea_i and Eb_i are arranged in the same order (as is commonly the case, e.g., if a and b are unmodified copies of the same container), then the average-case complexity for unordered_multiset and unordered_multimap becomes proportional to N (but worst-case complexity remains O(N²), e.g., for a pathologically bad hash function). The behavior of a program that uses operator== or operator!= on unordered containers is undefined unless the Pred function object has the same behavior for both containers and the equality comparison function for Key is a refinement²³⁰ of the partition into equivalent-key groups produced by Pred.

13 The iterator types iterator and const_iterator of an unordered associative container are of at least the forward iterator category. For unordered associative containers where the key type and value type are the same, both iterator and const_iterator are constant iterators.

14 The insert and emplace members shall not affect the validity of references to container elements, but may invalidate all iterators to the container. The erase members shall invalidate only iterators and references to the erased elements, and preserve the relative order of the elements that are not erased.

15 The insert and emplace members shall not affect the validity of iterators if (N+n) <= z * B, where N is the number of elements in the container prior to the insert operation, n is the number of elements inserted, B is the container's bucket count, and z is the container's maximum load factor.

16 The extract members invalidate only iterators to the removed element, and preserve the relative order of the elements that are not erased; pointers and references to the removed element remain valid. However, accessing the element through such pointers and references while the element is owned by a node_type is undefined behavior. References and pointers to an element obtained while it is owned by a node_type are invalidated if the element is successfully inserted.

17 The member function templates find, count, equal_range, and contains shall not participate in overload resolution unless the qualified-ids Pred::is_transparent and Hash::is_transparent are both valid and denote types (13.10.3).

18 A deduction guide for an unordered associative container shall not participate in overload resolution if any of the following are true:

- (18.1) — It has an InputIterator template parameter and a type that does not qualify as an input iterator is deduced for that parameter.
- (18.2) — It has an Allocator template parameter and a type that does not qualify as an allocator is deduced for that parameter.
- (18.3) — It has a Hash template parameter and an integral type or a type that qualifies as an allocator is deduced for that parameter.
- (18.4) — It has a Pred template parameter and a type that qualifies as an allocator is deduced for that parameter.

230) Equality comparison is a refinement of partitioning if no two objects that compare equal fall into different partitions.
