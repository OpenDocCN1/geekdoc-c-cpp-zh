# ISO/IEC 14882:2017(E)

Table 91 — Unordered associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre/post-condition | Complexity |
|---|---|---||
| X X a; | X | *Requires: hasher* and *key_equal* are. DefaultConstructible. Effects: Constructs an empty container with an unspecified number of buckets, using *hasher()* as the hash function and *key_equal()* as the key equality predicate. | constant |
| X(i, j, n, hf, eq) X a(i, j, n, hf, eq); | X | *Requires: value_type* is EmplaceConstructible into X from *1*. Effects: Constructs an empty container with at least n buckets, using *hf* as the hash function and *eq* as the key equality predicate, and inserts elements from {i, j} into it. | Average case O(N) (N is distance(i, j)), worst case O(N²) |
| X(i, j, n, hf) X a(i, j, n, hf); | X | *Requires: key_equal* is *DefaultConstructible*. *value_type* is EmplaceConstructible into X from *1*. Effects: Constructs an empty container with at least n buckets, using *hf* as the hash function and *key_equal()* as the key equality predicate, and inserts elements from {i, j} into it. | Average case O(N) (N is distance(i, j)), worst case O(N²) |
| X(i, j, n) X a(i, j, n); | X | *Requires: hasher* and *key_equal* are *DefaultConstructible*. *value_type* is EmplaceConstructible into X from *1*. Effects: Constructs an empty container with at least n buckets, using *hasher()* as the hash function and *key_equal()* as the key equality predicate, and inserts elements from {i, j} into it. | Average case O(N) (N is distance(i, j)), worst case O(N²) |