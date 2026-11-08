
### Specialty: By the Bucketful

You can take a closer look at the contents of the individual buckets:

- With `bucket_count()`, you get the current number of buckets in the container. The number cannot exceed `max_bucket_count()`.
- `begin(int)` and `end(int)` provide you with iterators to the elements of a single bucket.
- Beforehand, you can check the number of elements in a single bucket with `bucket_size(int)`.
- With `int bucket(Key)`, you can find out which bucket an element would end up in.

I find it difficult to imagine a meaningful application for this deep interface. However, I can imagine that such insights can be useful when you have to deal with the disadvantage of unordered containers, which do not offer any time guarantees. I can only provide you with an example that lists the contents of the individual buckets of an *unordered_set* with curious eyes.

```cpp
// https://godbolt.org/z/39v4aqgd1
// Fill with 100 values
unordered_set<int> d{};
d.rehash(10);               // try to have 10 buckets
d.max_load_factor(100.0);   // 100 elements per bucket are okay
cout << "Bucket count: " << d.bucket_count() << '\n';
for(int x : std::ranges::iota_view{0,100}) { // C++20 iota(): 0,1,2,...99
    d.insert(x);
}
// output
for(int b = d.bucket_count()-1; b>=0; --b) {
    cout << "Bucket "<<b<<": ";
    for(auto it=d.begin(b); it!=d.end(b); ++it)
        cout << *it << ' ';
    cout << '\n';
}
```

**Listing 24.82** You can access “unordered_set” by bucket.

For me, the attempt with `rehash(10)` resulted in getting 11 buckets. Often, prime numbers are a good idea. Otherwise, the output on my computer looked as follows:

```text
Bucket 10: 98 87 76 65 54 43 32 21 10
Bucket 9: 97 86 75 64 53 42 31 20 9
Bucket 8: 96 85 74 63 52 41 30 19 8
Bucket 7: 95 84 73 62 51 40 29 18 7
Bucket 6: 94 83 72 61 50 39 28 17 6
Bucket 5: 93 82 71 60 49 38 27 16 5
Bucket 4: 92 81 70 59 48 37 26 15 4
Bucket 3: 91 80 69 58 47 36 25 14 3
Bucket 2: 90 79 68 57 46 35 24 13 2
Bucket 1: 89 78 67 56 45 34 23 12 1
Bucket 0: 99 88 77 66 55 44 33 22 11 0
```

You can see here for each individual bucket which elements it contains.

### Specialty: Reserve Space

Each insertion can potentially cause all elements of the unordered_set to be rearranged. Then iterators lose their validity. Similar to vector, you can influence when this happens and thus control the timing. The exact mechanism is explained in Table 24.9. Here are the involved functions:

- `float load_factor()` is the average number of elements per bucket.
- When `load_factor` exceeds `float max_load_factor()`, a reorganization of the elements occurs. You can change the value yourself with `max_load_factor(float)`. In most implementations, this value is initially `1.0`.
- `rehash(size_t b)` sets the number of buckets to at least `b`, but never less than `size()/max_load_factor()`.
- `reserve(size_t c)` is the best way to ensure that `c` elements are well accommodated in the container with respect to the current `load_factor`.

In [Listing 24.82](...), I demonstrated rehash and reserve. `reserve(size_t c)` takes into account a previously set `max_load_factor(float)`. It corresponds to the call of `rehash(ceil(c/max_load_factor()))`.

## 24.8.5 “unordered_map”

The unordered_map shares large parts of its interface with map (Section 24.7.4) and often exhibits similar behavior to unordered_set (Section 24.8.4).

This implies that it is possible to link target values to keys and retrieve them rapidly. Of particular note is that this is usually achieved in O(1) time, which is optimal. Regrettably, this may not always be guaranteed, and in extreme cases the process could take O(n) time.

As with map, you have operator[], at, and insert_or_assign available. Otherwise, you search with forward iterators.

The examples in this section for unordered_map should be considered embedded in the code of Listing 24.83. However, note my comment on `<=>` in the box that follows Listing 24.12.

```cpp
// https://godbolt.org/z/15KKWwX4z4
#include <unordered_map>
#include <iostream>
using std::unordered_map; using std::cout;
template<typename K, typename T>
std::ostream& operator<<(std::ostream& os, const unordered_map<K, T>&data) {
    for(auto &e : data) {
        os << e.first << ": " << e.second << ', ';
    }
    return os << '\n'; // with operator<< followed by a newline
}
int main() {
    // Example code here
}
```

**Listing 24.83** This is the template for the example listings on “unordered_map”.

### The Elements and Their Properties

The elements of an `unordered_map` are `pair<const Key, Target>`. For Key, you need two things:

- You need a hash function, which is either `std::hash<Key>` or specified by you as a template argument.
- Key must be comparable with `==`, meaning it must be defined, or you must provide a functor for this.

For custom data types, the easiest way is to define `operator==` as friend or `operator<=>` with `= default` and also provide a custom hash functor. A short example is shown in Listing 24.84.

```cpp
// https://godbolt.org/z/cdeGW6a3P
#include <unordered_map>
#include <iostream>
#include <string>
using std::string; using std::unordered_map; using std::cout;
struct City {
    string name_;
    explicit City(const string &name) : name_{name} {}
    auto operator<=>(const City &b) const = default;
};
struct CityHash {
    std::hash<string> shash;
    size_t operator()(const City& a) const {
        return shash(a.name_);
    }
};
int main() {
    unordered_map<City, string, CityHash> cty{
        {City{"San Francisco"}, "CA"},
        {City{"Austin"}, "TX"},
        {City{"Miami"}, "FL"},
    };
    cout << cty[City{"San Francisco"}] << '\n'; // Output: CA
}
```

**Listing 24.84** A custom data type as a key in an “unordered_map”.

The spaceship operator `<=>` with `= default` ensures that the compiler can use it for `==` and thus it can be used by the `unordered_map`.

The CityHash functor requires a `size_t operator()(const City&) const` method. In it, I use the hash functor provided by the standard library for `string`.

### Initialize

When defining an `unordered_map`, you need at least the template arguments for Key and Target.

You can only omit them if you use pair for initialization; unfortunately, the compiler cannot help with nested initialization lists.

The rest is optional:

- Key—the key type for searching
- Target—the type to which the keys should refer
- Optional Hash—the hash functor for Key, default is `std::hash<Key>`
- Optional KeyEqual—the comparison operator for Key; by default `std::equal_to<Key>` and thus `operator==`
- Optional Allocator—memory allocator for the elements

Besides the types, you can use various constructor overloads. Most of the following options also have the possibility to provide a hash function, a comparison operator, or an allocator:

- The default constructor without arguments to create an empty container
- An iterator pair for copying from another container or stream
- An initializer list with initial values
- From C++23, *from_range* with a range
- Another `unordered_map` for a complete copy or move

A peculiarity of all unordered associative containers is that in the first three variants, an optional `size_t count` can still be passed, which sets the minimum size of the initial hash table.

### Assignment

Like all unordered containers, you can use `operator=` for both copying and moving to reinitialize the container. With swap, you have a tool for very quickly exchanging all data with another `unordered_map`.

### Insert

When inserting, there is no difference in the interface compared to map. Only the runtime guarantees are different as they are consistently between constant and linear per inserted element:

- **Inserting a single element with automatic positioning**  
  Use `insert(pair<Key,Target>)` or `emplace(Key,Target)` to insert a new element. Be careful here as well: the container will not overwrite if the key already exists.
- **Automatic insertion and overwriting**  
  Alternatively, you can also use `operator[]` for insertion, but this will first create an empty `Target`. If you use this on the left side of an assignment, you will get a reference to this `Target` back, which you can then reassign. `insert_or_assign` saves the creation of an empty value.
