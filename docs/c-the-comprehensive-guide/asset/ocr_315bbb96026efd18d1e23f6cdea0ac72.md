+   - **Transferring an element**  
+     With `extract`, you remove a single element from the set. The return value is a “handle” for the removed node, which you can use for other purposes, such as transferring it to another similar set using `insert`.
+   - **Deleting multiple of elements**  
+     With a pair of iterators as arguments, `erase` can delete the elements between them.

All iterators of nondeleted elements retain their validity.

```
```cpp
// https://godbolt.org/z/dh8Yqxc64
set<int> data{ 10, 20, 30, 40, 50, 60, 70 };
auto lo = data.lower_bound(35);
auto up = data.upper_bound(55);
data.erase(lo, up);        // deletes all numbers between 35 and 55
cout << data;              // Output: 10 20 30 60 70
lo = data.lower_bound(20);
up = data.upper_bound(60);
data.erase(lo, up);        // deletes including 60, because up points to 70
cout << data;              // Output: 10 70
auto n = data.erase(69);   // deletes nothing
cout << "Number of removed elements: " << n << '\n'; // Output: Number ... 0
n = data.erase(70);        // deletes the element of 70
cout << "Number of removed elements: " << n << '\n'; // Output: Number ... 1
cout << data;              // Output: 10
```
```

**Listing 24.58** “erase” deletes one or more elements.

# 24.7.4  “map”

A map is used to quickly find values using keys. Each key (Key) in a map is associated with exactly one target (Target). The map is related to the set in that the rules for the elements of set apply to the keys of map:

+   - Keys in a map are always sorted.
+   - No key appears more than once in a map.
+   - Searching for a key is guaranteed to take at most log n steps.

Much of what applies to set also applies to map, so **Section 24.7.3** can provide additional information.

However, there is a big difference from set: the individual elements in the map are a pair, specifically a `pair<const Key, Target>`. When I refer to this pair, I use the term Element or elem in the context of map.