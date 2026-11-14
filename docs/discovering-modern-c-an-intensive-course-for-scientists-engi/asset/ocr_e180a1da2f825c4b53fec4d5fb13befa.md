count. find returns an iterator referring to the value or if not found to the end iterator. If we don't need the iterator, count is more convenient. In this case, it is more convenient to use count:

```
```cpp
set<int> s = {1, 3, 4, 7, 9};
s.insert(5);
for (int i = 0; i < 6; ++i)
    cout << i << " appears " << s.count(i) << " times.\n";
```
```

yielding the expected output:

```
```
0 appears 0 time(s),
1 appears 1 time(s),
2 appears 0 time(s),
3 appears 1 time(s),
4 appears 1 time(s),
5 appears 1 time(s),
```
```

Multiple insertions of the same value have no impact; i.e., count always returns 0 or 1.

The container multiset additionally counts how often a value is inserted:

```
```cpp
multiset<int> s = {1, 3, 4, 7, 9, 1, 1, 4};
s.insert(4);
for (int i = 0; i < 6; ++i)
    cout << i << " appears " << s.count(i) << " time(s).\n";
```
```

yielding:

```
```
0 appears 0 time(s).
1 appears 3 time(s).
2 appears 0 time(s).
3 appears 1 time(s).
4 appears 3 time(s).
5 appears 0 time(s).
```
```

For only checking whether a certain value is present in the multiset, find is more efficient as it doesn't need to traverse replicated values.

Please note that there is no header file named multiset but the class multiset is also defined in <set>.

# 4.1.3.5 Maps and Multimaps

=> c++11/map_test.cpp

A map is an associative container; i.e., values are associated with a Key. The key can have any type with an ordering: either provided by operator < (via the less functor) or by a functor