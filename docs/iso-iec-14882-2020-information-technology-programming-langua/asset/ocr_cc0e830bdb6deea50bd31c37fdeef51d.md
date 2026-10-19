# ISO/IEC 14882:2020(E)

Table 81: Unordered associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
|---|---|---|---|
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