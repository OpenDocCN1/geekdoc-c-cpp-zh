
```cpp
    return sHash(a.city_j);
}
int main() {
    unordered_multiset<Entry, Hash, EqEntry> directory({
        Entry("New York", 10001);
        Entry("New York", 10002);
        Entry("New York", 10003);
        Entry("Chicago", 60601);
        Entry("Chicago", 60602);
    });
    const Entry search("New York", // ZIP code does not matter in search
    cout << "New York has " << directory.count(search) << " ZIP codes.\n";
    cout << "The ZIP codes of New York are:\n";
    auto (where, until) = directory.equal_range(search);
    while (where != until) {
        cout << where->zip_j << '\n';
    }
}
```

# **Listing 24.85** You can use only part of your object as a key.

The output, of course, is as follows:

New York has 3 ZIP codes.
The ZIP codes of New York are:
10001
10002
10003

The EqEntry and HashEntry functors, which are specified as template arguments, ensure that all entries with the same city_name are considered equal. It would not be enough to define only the hash function or only the equality; both operations must match as-otherwise otherwise the entries will get mixed up and not end up in the correct buckets. Therefore, you must carefully select and program the two functors.

For example, if you include more elements in equality in the hash function, you will not find an entry with count(search), but only with count(Entry("New York", 10001)). It may be that this is what you wanted, but then your hash function is not optimal, and you should have included zip_:

```cpp
struct EqEntry {
    bool operator()(const EqEntry& a, const EqEntry& b) const {
        return tie(a.city_j, a.zip_j) == tie(b.city_j, b.zip_j); // Really?
    }
};
struct HashEntry {
    std::hash sHash;
    size_t operator()(const HashEntry& a) const {
        return sHash(a.city_j);
    }
};
```

It would be the other way around, if equality covered fewer elements
than the hash functor:

```cpp
// https://godbolt.org/r/cve7BEEi7o
struct Entry {
    bool operator()(const Entry& a, const Entry& b) const {
        return a.city == b.city;
    }
};

struct HashEntry {
    std::hash<string> hash;
    std::hash<int> hash;
    size_t operator()(const Entry& a) const {
        return hash(a.city) ^ hash(a.zip); // too many elements
    }
};
```

Now you probably won't find a single entry anymore. Different New York,
which are actually equal by == have landed in different hash buckets and are
distributed throughout the entire container. You still have the chance to
find individual entries like Entry("New York, 10001"). However, because two New
York entries can also end up in the same bucket, even that is not
guaranteed. The result is data garbage.

# Initialize

Regarding the template parameters, you declare an unordered_multiset just like
an unordered_set, meaning you need to specify the entry or key type and can also specify the hash function, key comparison functor, and allocator.

However, starting from C++17, the compiler can help you by often deducing
the template parameters from the constructor arguments.

The possibilities for initialization via constructor are similar to unordered_set,
except that duplicates are preserved. Here too, except for the copy
constructor, all options can accept an additional parameter to specify the initial
size of the hash table:

- A default constructor without arguments initializes the container as empty.
- A pair of iterators from another container or stream copies the range defined by them.
- In an initializer list, you can explicitly specify the initial elements.
- You can completely copy another unordered_multiset.
- Starting from C++23, there is also a constructor with the from_range tag.

Note in the following example that duplicates are preserved.

```cpp
// https://cppbolt.com/z/bUf8Hse
#include <unordered_set> using unordered_multiset
#include <vector>
#include <iostream>
using unordered_multiset; using std::cout; using std::ostream;
template<typename E>
std::ostream& operator<<(std::ostream& os, const unordered_multiset<E>& data) {
    for (auto &e : data) { os << e << " "; }
    return os;
}
int main() {
    // without arguments
    unordered_multiset empty(1000); // initial size of the hash table
    cout << empty; 
    // Initialization list duplicates are included:
    unordered_multiset data{1,1,2,2,3,4,4,5,5};
    cout << data; // Output: 5 5 4 4 3 2 2 1 1
    // Copy
    unordered_multiset copy(data);
    cout << copy; // Output: 5 5 4 4 3 2 2 1 1
    // Range
    std::vector<int> vec{1,2,3,10,20,30,20,30,1,2,3};
    unordered_multiset range(vec.begin(),vec.end());
    cout << range; // Output: 30 30 20 20 10
}
```

**List 24.86** These are the ways to initialize an "unordered_multiset". Of the course, the order of elements in the output can vary from system to system.

# Assignment

With all other containers, you can use operator= to copy or move data from another unordered_multiset. Also, swap is defined for quick exchange.

# Insert

Insertion happens in unordered_multiset just like multiset. Unlike unordered_set, every insertion is successful because duplicates are also stored:

- Inserting a single element with automatic positioning with insert copy a new element into the container, while with emplace, you create it in place.
- Inserting a single element with an iterator with insert, it may save the computation of the hash value and the traversal of elements within a bucket. The position hint should point to an element that is equal to the new element. If you do not provide a correct element, the advantage is lost, but the element ends up in the right place.
- Inserting multiple elements insert also accepts a pair of iterators or an initializer list for inserting multiple elements. From C++23, there is also insert_range. With merge, you retrieve all elements from another container, including duplicates.

If you have made provisions with reserve, you must assume that all iterators to the container have become invalid after an insertion.

# Access

You have forward iterators available, as you can see in Table 24.2:

- Access via iterators with begin() and end() as well as cbegin() and cend(), you get iterators to the beginning and end of the container.
- Access via search find any matching element, or get end() back if there is none. For multi variants, count and equal_range methods make sense: With count, you can count the number of elements, and with contains, you can check for existence. The equal_range method returns the range of all matching elements with a pair of iterators.

Here is an example of accessing an unordered multiset:

```cpp
// https://cppreference.com/w/cpp/unordered_multiset
#include <unordered_set> // unordered multiset
#include <iostream>
#include <string>

using std::unordered_multiset; using std::cout; using std::string;
int main() {
  const string in = "She sells shells by the seashore.";
  unordered_multiset<int> cs(in.begin(),in.end()); // string as container
  cout << cs.count('s') << " times s\n"; // Output: 7 times s
}
```

**Listing 24.87** For the "multi" variants, count makes perfect sense. If creating a key is expensive and you only need to do it for searching, consider the unordered multiset. This allows you to search without creating a complete key.

# Deleting

The relative order of nondeleted elements to each other remains valid when deleting, as iterators referencing these elements:

- Deleting all elements clear() deletes all elements.
- Deleting or transferring a single element erase with a value deletes all occurrences of that element. The return value is the number of elements deleted. If you specify an iterator, the element at that position is deleted. The return value is then the position of the next element. With extract, you delete an element that you would normally insert elsewhere.
- Deleting multiple elements with a pair of iterators, you can delete multiple elements. This actually only makes sense for unordered containers if this range includes all elements, which is equivalent to clear(), or if the range includes all or some elements of equal_range. Both are possible, but probably rare in practice. Deletion also works with areas that include several different elements, but which elements lie between is hard to predict for unordered containers.

# Specialty: By the Bucket

You can gain detailed insights into the inner workings of the unordered_multiset using bucket_count(), bucket_size, and bucket as well as the int variants of begin(int) and end(int).

# Specialty: Reserve Space

To repel unwanted interruptions from reallocations of the hash table when inserting, you can manipulate the hash mechanism using the load_factor, max_load_factor, rehash, and reserve methods.

> The unordered_map can do everything that 24.8.7 “unordered_multimap can do (Section 24.7.6), but as an unordered associative container, it also has an interface that is closely related to the unordered_multiset (Section 24.8.6).

Keys are mapped to target values, which usually takes O(1) time, but in exceptional cases can also take O(n). Instead of using less than, the keys are compared using == and a hash function.

A key can be inserted multiple times, each time referring to target values.

# Element Properties

With all map-like containers, the elements of the unordered_multimap are of type pair<const Key, Target>. This means that if you have a reference to an element or a Target, you can assign a new value to Target. The Key is const and not be changed under any circumstances; otherwise, the container will get confused.

[ 62 ]

For the key, equality == must be check and a hash must be computable. This can be done either via the free function operator== and the functor std::hash<Key>, or you can specify your own functors as template parameters.
