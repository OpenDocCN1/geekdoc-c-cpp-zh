# Table G.10 Operations Defined for Sets, Multisets, Maps, and Multimaps

| Operation | Description |
|---|---|
| a.erase(q) | Erases the element pointed to by q. |
| a.erase(q1,q2) | Erases the elements in the range [q1, q2). |
| a.clear() | Does the same thing as erase(a.begin(), a.end()). |
| a.find(k) | Returns an iterator that points to an element whose key is equivalent to k; returns a.end() if no such element is found. |
| a.count(k) | Returns the number of elements that have keys equivalent to k. |
| a.lower_bound(k) | Returns an iterator to the first element that have a key not less than k. |
| a.upper_bound(k) | Returns an iterator to the first element that have a key greater than k. |
| a.equal_range(k) | Returns a pair whose first member is a.lower_bound(k) and whose second member is a.upper_bound(k). |
| a.operator[](k) | Returns a reference to the value associated with the key k (map containers only). |

# Unordered Associative Containers (C++11)

As mentioned earlier, the unordered associative containers (unordered_set, unordered_multiset, unordered_map, and unordered_multimap) use keys and hash tables to provide rapid access to data. Let’s take a simple look at these concepts. A hash function converts a key to an index value. For example, if the key were a string, the hash function could sum the numeric codes for the characters in the string and take that sum modulus 13, thus giving an index in the range 0–12. The unordered container would use 13 buckets to store strings. Any string with, say, an index of 4 would be placed in bucket 4. If you wished to search the container for a key, you would apply the hash function to the key and just search the bucket with the corresponding index. Ideally, you would have enough buckets that each one would contain only a few strings.

The C++11 library provides a hash<Key> template that the unordered associative containers use by default. Specializations are defined for the various integer and floating-point types, for pointers, and for some template classes, such as string.

Table G.11 lists types used for these containers.

The interface for the unordered associative containers is similar to that of the associative containers. In particular, Table G.10 also applies to the unordered associative containers with the following exceptions: The lower_bound() and upper_bound() methods are not required, nor is the X(i,j,c) constructor. The fact that the regular associative containers are ordered allows them to use a comparison predicate that expresses the “less