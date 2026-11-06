# Section 15.6.1 `multiset`
Associative Container

+   - The `multiset` **associative container** (p. 682) provides fast storage and retrieval of keys and allows duplicate keys. The key order is determined by a comparator function object. If the order of the keys is not important, you can use `unordered_multiset` (header `<unordered_set>`) instead.
+   - A `multiset`’s keys can be sorted in ascending order by ordering the keys with comparator function object `less<T>` (p. 682).
+   - The type of the keys in all associative containers must support comparison properly based on the comparator function object specified.
+   - A `multiset` supports bidirectional iterators.
+   - Header `<set>` (p. 682) must be included to use class `multiset`.
+   - Function `count` (p. 684; available to all associative containers) counts the number of occurrences of the specified value currently in a container.
+   - Function `find` (p. 684; available to all associative containers) locates a specified value in a container.
+   - Associative container functions `lower_bound` and `upper_bound` (p. 685) locate the earliest occurrence of the specified value in a