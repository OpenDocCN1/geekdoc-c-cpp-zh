
+   Inserting a single element with automatic positioning
Inserting a single element with emplace takes O(1) time in the best case and O(n) in the worst case. While insert copies the new element, with emplace you provide the constructor arguments for creating it in place. Note that, with set, an element is not replaced if it is already contained in the unordered set. Whether something was actually inserted can be determined from the bool in the returned pair. Listing 24.80 shows an example.

+   Inserting a single element with a position hint
With set, you can speed up an insertion a bit if you already know where the element belongs. To do this, use insert with a position iterator or hint. However, the savings are of a completely different nature than usual. With unordered_set, the standard library can save the calculation of the hash as well the cumbersome traversal through the bucket list. A single key comparison is enough to determine whether the element needs to be inserted. Listing 24.80 contains an example of this at the end. What somewhat unnecessary with unordered_set makes more sense with unordered multiset. If the position is not correct, the additional time required is minimal.

+   Inserting multiple elements
Like all containers, unordered_set can also insert into an entire area using a pair of iterators or an initializer list. Starting with C++23, there is also insert_range. With merge, you can retrieve multiple elements from another unordered_set, but only the elements that are not already present in the current one are transferred.

The next list shows basic insertion into an unordered_set.

```cpp
//://godbolt.org/z/izMocM
unordered_set<int> data;
auto res1 = data.insert(5); // Insertion by copy
if(res1.second) cout << "yes, 5 inside"; // that works
auto res2 = data.emplace(5); // In-place insertion
if(res2.second) cout << "rounded, 5 inside\n"; // that doesn't work
auto res3 = data.insert(res1.first, 6); // With position hint
res3 is just an iterator without bool
out << res3 << "\n"; // definitely a 6
```
> Listing 24.80 Insertion into an "unordered_set"

All insertion operations potentially invalidate iterators in the container. However, if you are sure that no reordering of elements has taken place, iterators remain valid—for example, because you previously called the method appropriately.

# Accessing

Unlike set, the unordered associative containers only provide forward iterators, as I have already shown in Table 24.2. So they are not suitable for sorting at all:

- - Access via iterators
You get an iterator to the beginning with begin() and cbegin(), and an iterator past the end of the container with end() and cend(). When you iterate over the elements with ++it, next(it), or advance, their order is arbitrary but stable across multiple passes, provided you have not modified the container in the meantime.
- - Access via search
For unordered associative containers, count search functions, like those available for ordered ones, do not make sense; two searches for different keys do not enclose a range. In unordered set, count returns zero or one. equal_range either encompasses a range with exactly one element or returns end() twice.

A search with a concrete key is not possible with unordered associative containers because the search requires a hash value, and a hash value requires a specific key.

# Deleting

The methods for deletion are the same as with set, though the interface is slightly restricted:

- - Deleting all elements
You clear unordered_set With clear().
- - Deleting or transferring a single element
You can use an iterator or a key to search for erase as a parameter. The return value is an iterator to the element after the deleted one. With extract, you remove the element that you insert elsewhere with insert.
- - Deleting multiple elements
You specify multiple elements with two iterators for erase, but the unspecified order within unordered_set makes this partially meaningful unless you use begin() and end() as parameters, which you can better achieve with clear().

Iterators to nondeleted elements retain their validity.

Furthermore, deleting elements does not affect the order of the remaining elements among themselves. This means you can delete multiple elements within a loop without worrying about whether a delete action has changed the order of the elements so that you might not see some elements anymore.

```cpp
// https://godbolt.org/z/hee331WGe
unordered_set nums{1,2,3,4,5,6,7,8,9,10};
cout << nums; // Output similar to: 9 1 2 3 4 5 6 7 8 10
auto it = nums.begin();
while(it != nums.end()) {
    if(*it % 2 == 0) { // even number?
        it = nums.erase(it); // Remaining elements do not change order
    } else {
        ++it;
    }
}
cout << nums; // Output similar to: 9 1 3 5 7
```
# **Listing 24.81** Deleting preserves the order of the remaining elements.

Even if the order of the output may look different on your computer, you will get the same order in the second output as in the first, just without even numbers.

The call to erase returns an iterator to the next element. If erase is not to be called, then ++it ensures the iterator moves forward.

# Specialty: By The Bucketful

You can take a close look at the bucketful:
- With count(), you get the number of buckets.
- With max_size(), you find the maximum number of elements.
- Before max_size(), you can find the number of buckets.
- With begin(), you get the iterators to the elements.
- With end(), you get the iterators to the end.
- With hash(key), you find the hash value of a key.
- With bucket(key), you find which bucket a key belongs to.
- With bucket(size), you get the elements in a specific bucket.

```cpp
// https://godbolt.org/z/hee331WGe
unordered_set<int> d;
d.reserve(100);
cout << "Bucket count: " << d.count() << "\n";
for (int b = 0; b < d.count(); ++b) {
    cout << "Bucket " << b << ":\n";
    for (auto it = d.begin(b); it != d.end(b); ++it) {
        cout << "  " << *it << "\n";
    }
}
```
**Listing 24.82** Reserve Space

# Reserve Space

Each insertion can potentially cause all elements of the unordered_set to be rearranged. Then iterators lose their validity. Similar to vector, you can influence when these happens and control the timing. The exact mechanism is explained in Table 24.9. Here are the involved functions:

- float load_factor() is the average number of elements per bucket.
- When load_factor exceeds float max_load_factor(), a reorganization of the elements occurs. You can change the value yourself with max_load_factor(float). In some implementations, this value is initially 1.0.
- reserve(size_t c) sets the number of buckets to at least b, but never less than size()/max_load_factor().
- reserve(size_t c) is the best way to ensure that c elements are well accommodated in the container with respect to the current load_factor.
