
| Property | set | map | multiset | multimap |
|---|---|---|---|---|
| Iterators/ranges | Random | Random | Random | Random |
| Algorithms | All | All | All | All |

**Table 24.7** Properties of ordered associative containers. The meaning of the asterisks is explained ahead.

## 24.7.2 Methods of Ordered Associative Containers

I am not always very precise or detailed with the function signatures here to save space and increase clarity. If I do not include the parentheses with method, there are usually multiple overloads:

- Constructors: C(), C(Compare), C{}, C(It, It), **C(from_range, rg)**
  The default constructor `C()` creates an empty container. With a pair of iterators from another container, you can copy its contents. You can specify an initializer list that populates your container. For a map, this means you specify nested {...} because each element must initialize a `pair`—example, `map<int,string>{ {2,"two"}, {3,"three s"} }`. Starting from C++23, there is a `from_range` constructor.

- Copy and move: C(const&), C(&), C& op=(const C&), C& op=(&&)
  You can pass a `const T&` as an argument to the copy and move constructors and operators. Efficient `swap(Cont& other)` is implemented by all associative containers. **Note:** Compared to sequence containers, associative containers have neither `assign_range`.

- Destructor: ~Cont())
  All containers have destructors that remove the contained elements. This does not apply if you pack raw pointers into containers.

- Iterate forward: begin(), end(); and backward: rbegin(), rend()
  You can iterate here just like with sequential containers. The ordered containers guarantee that the elements are sorted when iterating. The iterators of the `map` variants reference a `pair<K,T>`.

- Element access: T& operator[](Key), T& at(Key)
  Only map has these methods. If the key does not exist in `at`, an `out_of_range` exception is thrown. With `operator[](Key)`, you can read and write in the map. It does not fail if a key is not found. For example, if you write `auto v = mymap[key]`, a new (default-constructed) target value will be created in `mymap[key]` if necessary. Only then will it be returned to `v`. Handy–and important to know.

- Size: size(), empty(), max_size()
  With `size()`, you get the current number of elements in the container; `empty()` is true if this number is zero. With `max_size()`, you get the library-specific maximum size of the container.

- Modification: clear(), erase, insert, insert_or_assign, emplace, and insert_range
  These methods work like those in sequence containers. In maps, an element consists of a `pair<K,T>`, which you can insert with `insert` and `emplace`. Only map also has `insert_or_assign`. `insert_range` available from C++23.

- Search: count, find, lower_bound, upper_bound, equal_range, contains
  With these methods, you can get information about the keys in the container. `count` returns how often one occurs; `find` returns an iterator to a found key (possibly one of several) or `end()` if it is found. `lower_bound` and `upper_bound` do something similar, but they search for the first and last key, respectively. If nothing is found, they return an iterator to the position where the searched key would be inserted, unlike `find`. `equal_range` performs both operations simultaneously and returns a pair of iterators that encompass all keys matching the searched one (this has nothing to do with the ranges library). In the non-multiset variants, it is logical that there is at most one element in between, while the multiset variants, there can be several. `contains` is available from C++20.

- Transfer: merge
  With `merge`, you transfer elements from one container to another. In the multiset variants, all elements are transferred, while in the non-multiset variants, only those not present in the target are transferred, with duplicates remaining in the source.

All ordered associative containers store their elements in a tree structure (see Figure 24.9 and Figure 24.10). To ensure the efficiency of the container, it is kept balanced at all times. This means that with each insert or delete operation, the nodes are cleverly rearranged that all leaves of the tree are pulled to (almost) the same height. This additional management effort is worthwhile because it guarantees that any search will find the element or confirm its absence in most log n steps. This holds true at all times, despite constant insertions and deletions, regardless of the data you put in.

For a set, the following main use cases exist:

### 24.7.3 "set" Deduplication

You want to store a collection of objects, and duplicates to be ignored. Because a set stores each key only once, all duplicates are already removed when reading.

### Sorting

A collection of objects should be kept sorted when you alternately store, search, store, search, and so on. A vector is often more suitable if you first store a collection of objects and then want to search quickly in a later separate phase. A set is recommended if there are not two clearly separated phases.

If you do not need this guarantee of order constant, because you, for example, access the set in two separate phases—a filling phase and a reading phase—then use a vector.

```cpp
#include <iostream>
#include <set>
#include <vector>
#include <string>

using namespace std;

template <typename T, typename Comp>
std::ostream& operator<<(std::ostream& os, const set<T, Comp>& s) {
    for (const auto& e : s) {
        os << e << " ";
    }
    return os;
}

int main() {
    set<int> s = {3, 1, 2, 3};
    cout << "Set elements: " << s << endl;
    return 0;
}
```

```cpp
map<int,string> mymap = {{2, "two"}, {3, "three"}};
auto v = mymap[4]; // creates key 4 with default value if not exists
```
