# Specialty: By The Bucketful

The unordered_map also has an interface that allows you to gain precise insights into its internal workings. You can use bucket_count() to get the number of buckets and [c]begin/end(int) iterators to access the contents of buckets. In addition, bucket_size(int) and int bucket(Key) are available to you.

# Specialty: Reserve Space

To maintain control over when a reordering of elements occurs during insertion, you can influence this mechanism with several methods, similar to unordered_set.load_factor and max_load_factor the interfaces for load factor, and with rehash and reserve you can directly influence the size of the hash table.

The unordered_multiset inherits its properties from unordered_set (Section 24.7.3) and from multiset (Section 24.7.5).

It usually finds its keys optimally in O(1), but unfortunately guarantee this and then needs O(n) time in the worst case, which is why the ordered multiset might be the better choice if you want to avoid nasty surprises.

As with multiset, each key can be stored multiple times. One of the typical use cases is that only a part of the stored objects actually serves as keys. There is an example in Listing 24.85.

# Element Properties

The elements of an unordered_multiset are simultaneously its keys, as with set. And with unordered_set, you need equality == for the keys and a hash function. For custom types, the best option is to define operator== with default, or if not possible, operator==.

```
//://godbolt.org/z/Ed8znPn9
#include <unordered_set> // unordered_multiset
#include <iostream>
#include <string>
using std::string; using std::unordered_set; using std::cout;
struct City {
    string name;
    explicit City(const string& name) : name(name) {}
    auto operator==(const City& b) const = default;
};
struct Entry {
    City city;
    int zip;
};
struct Edntry {
    bool operator()(const Entry& a, const Entry& b) const {
        return a.city==b.city_;
    }
};
struct HashEntry {
    std::string sHash;
    size_t operator()(const Entry& a) const {
```