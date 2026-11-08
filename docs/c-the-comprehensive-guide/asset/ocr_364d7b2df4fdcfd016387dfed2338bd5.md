```
```cpp
vals.erase('c');        // deletes all c's
cout << vals;            // Output: a7a1:g1
vals.erase(vals.begin()); // deletes only one of the a's
cout << vals;             // Output: a1:g1
```
```

**Listing 24.74** “erase” with a key can delete multiple elements.

# 24.8  Only Associative and Not Guaranteed

In this section, Cont or C stands for one of the container types and cont for an instance of it. As *key type* I use Key or K, as *target type* Target or T, and the *value type* pair<K,T> is Value or V. *Iterator types* are abbreviated as It.

| Container | Description |
|---|---|
| unordered_set | Contains a unique set of elements |
| unordered_map | Unique keys refer to a target value |
| unordered_multiset | Is a set of elements that can occur multiple times |
| unordered_multimap | Keys can occur multiple times |

**Table 24.8** Profile: The associative unordered containers.

These containers do not store their keys sorted, but *hash* them. This has two effects: first, the elements are not in a specific order when you iterate; and second, hashing is often faster than sorting.

![](bbox=[0.143, 0.586, 0.552, 0.754])

**Figure 24.14** An “unordered_map” internally groups the keys by hash code. In the “unordered_set”, the values themselves are the keys.

# 24.8.1  Hash Tables

While map, set, and their multi... variants store their elements in a permanently sorted tree, the unordered variants use lookup tables called *hash tables*.