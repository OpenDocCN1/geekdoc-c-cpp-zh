# ISO/IEC 14882:2017(E)

Table 91 — Unordered associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre/post-condition | Complexity |
| :--- | :--- | :--- | :--- |
| X::key_equal | Pred | **Requires:** Pred is CopyConstructible. **Pred** shall be a binary predicate that takes two arguments of type Key. **Pred is an equivalence relation. | compile time |
| X::local_iterator | An iterator whose category, value, difference, and pointer and reference types are the same as X::iterator. | A *local_iterator* object may be used to iterate through a single bucket, but may not be used to iterate across buckets. | compile time |
| X::const_local_iterator | An iterator type whose category, value, difference, and pointer and reference types are the same as X::const_iterator. | A *const_local_iterator* object may be used to iterate through a single bucket, but may not be used to iterate across buckets. | compile time |
| X::node_type | a specialization of a **node_handle** class template, such that the public nested types are the same types as X. | 26.2.4 | compile time |
| X(n, hf, eq) X a(n, hf, eq); | | Effects: Constructs an empty container with at least n buckets, using **hf** as the hash function and **eq** as the key equality predicate | $\O(n)$ |
| X(n, hf) X a(n, hf); | | **Requires:** key_equal is DefaultConstructible. Effects: Constructs an empty container with at least n buckets, using **hf** as the hash function and **key_equal()** as the key equality predicate. | $\O(n)$ |
| X(n) X a(n); | | **Requires:** hasher and key_equal are DefaultConstructible. Effects: Constructs an empty container with at least n buckets, using **hasher** as the hash function and **key_equal()** as the key equality predicate. | $\O(n)$ |