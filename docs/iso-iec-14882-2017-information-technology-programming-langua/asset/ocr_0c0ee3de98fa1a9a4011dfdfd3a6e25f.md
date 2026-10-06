# ISO/IEC 14882:2017(E)

Table 91 — Unordered associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre/post-condition | Complexity |
| b.find(k) | iterator; const_iterator for const b. | Returns an iterator pointing to an element with key equivalent to k, or end if no such element exists. | Average case O(1), worst case O(b.size()). |
| b.count(k) | size_type | Returns the number of elements with key equivalent to k. | Average case O(b.count(k)), worst case O(b.size()). |
| b.equal_range(k) | pair<iterator, iterator>; pair<const_iterator, const_iterator> for const b. | Returns a range containing all elements with keys k. make_pair(b.end(), b.end()) if no such exists. | Average case O(b.size()). |
| b.bucket_count() | size_type | Returns the number of buckets b contains. | Constant |
| b.max_bucket_count() | size_type | Returns an upper bound on the number of buckets that b might contain. | Constant |
| b.bucket(k) | size_type | Requires: b.bucket_count() > 0. | Constant |
| b.bucket_size(n) | size_type | Returns the index of the buckets in which elements equivalent to k would be found, if any such element existed. Postconditions: the return value should be in the range [0, b.bucket_count()). | O(b.bucket_size(n)) |
| b.begin(n) | local_iterator; const_local_; iterator for const b. | Returns the number of elements in the n-th bucket. Requires: n shall be in the range [0, b.bucket_count()). b.begin(n) returns an iterator referring to the first element in the bucket. If the bucket is empty, b.begin(n) == b.end(). | Constant |
| b.end(n) | local_iterator; const_local_; iterator for const b. | Requires: n shall be in the range [0, b.bucket_count()). b.end(n) returns an iterator which is the past-the-end value for the bucket. | Constant |