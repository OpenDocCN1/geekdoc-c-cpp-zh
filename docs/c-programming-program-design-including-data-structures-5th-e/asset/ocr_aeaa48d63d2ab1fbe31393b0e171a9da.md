The algorithm `set_symmetric_difference` has two forms, as shown by the following prototypes:

```
```cpp
template <class InputItr1, class InputItr2,
          class OutputItr>
outputItr set_symmetric_difference(inputItr1 first1,
                                   inputItr1 last1,
                                   inputItr2 first2,
                                   inputItr2 last2,
                                   outputItr destFirst);
```
```

```
```cpp
template <class InputItr1, class InputItr2,
          class OutputItr, class BinaryPredicate>
outputItr set_symmetric_difference(inputItr1 first1,
                                   inputItr1 last1,
                                   inputItr2 first2,
                                   inputItr2 last2,
                                   outputItr destFirst,
                                   binaryPredicate op);
```
```

Both forms create a sequence of sorted elements that are in the sorted range `first1...last1-1` but not in `first2...last2-1`, or elements that are in the sorted range `first2...last2-1` but not in `first1...last1-1`. In other words, the sequence of elements created by `set_symmetric_difference` contains the elements that are in `range1_difference_range2 union range2_difference_range1`. The created sequence is placed in the container beginning with `destFirst`. Both forms return an iterator positioned one past the last element copied at the destination range. The first form assumes that the elements are in ascending order. The second form assumes that both ranges are sorted using the operation specified by `op`. The elements in the source ranges are not modified. It can be shown that the sequence created by `set_symmetric_difference` contains elements that are in `range1_union_range2` but not in `range1_intersection_range2`.

Suppose that:

```
```text
setA = {3, 4, 5, 6, 7, 8, 10}
setC = {1, 5, 6, 8, 15}
setD = {2, 5, 9, 6, 9}
```
```

Notice that `BdifferenceC = {3, 4, 7, 10}` and `CdifferenceB = {1, 15}`. Therefore:

`BsymDiffC = {1, 3, 4, 7, 10, 15}`

Now `DdifferenceC = {2, 5, 9}` and `CdifferenceD = {1, 8, 15}`. Therefore:

`DsymDiffC = {1, 2, 5, 8, 9, 15}`

Example 22–28 illustrates how the functions `set_difference` and `set_symmetric_difference` work.