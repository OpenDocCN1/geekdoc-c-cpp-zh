The first two arguments specify the range of elements in the first sorted sequence (`a1`), the second two arguments specify the range of elements in the second sorted sequence (`a2`) and the last argument specifies the starting location in the third sequence (`results2`) where the elements will be merged. A second version of this algorithm takes as its sixth argument a *binary predicate function* that specifies the *sorting order* by comparing its two arguments and returning `true` if the first is less than the second.

# `back_inserter, front_inserter` and `inserter` *Iterator Adapters*

Line 27 created the `array results2` with the total number of elements in both `a1` and `a2`. Using the `merge` algorithm requires that the sequence where the results are stored be at least the sum of the sizes of the sequences being merged. If you do not want to allocate the number of elements for the resulting sequence *before* the `merge` operation, you can use a dynamically growable `vector` and the following statements:

```
```cpp
vector<int> results;
merge(a1.begin(), a1.end(), a2.begin(), a2.end(),
    back_inserter(results));
```
```