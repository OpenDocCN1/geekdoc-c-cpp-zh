```
std::sort_heap(v4.begin(), v4.end());
print(v4, "Sorted heap");
}
```

The output is:

```
**** Block III, heap sort etc. ****
input vector 3, 4, 5, 6, 7, 5, 6, 7, 8, 9, 1, 2, 3, 4,
heap sorted vector 9, 8, 6, 7, 7, 5, 5, 3, 6, 4, 1, 2, 3, 4,
2nd input vector 3, 4, 5, 6, 7, 5, 6, 7, 8, 9, 1, 2, 3, 4,
2nd heap sorted input vector 1, 3, 2, 6, 4, 3, 4, 7, 8, 9, 7,5,5, 6,
popped 8, 7, 6, 7, 4, 5, 3, 6, 4, 1, 2, 3, 9,
popped vector 8, 7, 6, 7, 4, 5, 6, 3, 6, 4, 1, 2, 3,
Value 17 pushed 17, 7, 8, 7, 4, 5, 6, 3, 6, 4, 1, 2, 3, 5,
Sorted heap 1, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8, 17,
```

# 18.5 SORTED-RANGE ALGORITHMS

The algorithms in this category operate on ranges that have already been sorted according to their sorting criterion. These algorithms have significantly better performance than similar algorithms for unsorted ranges that we discussed in Chapter 17.

The algorithms address the following functionality:

+   - Does a sorted range contain a given value?
+   - Does a sorted range contain all elements of another sorted range?
+   - Give the position of the first element in a sorted range with value equal to or greater than a given value.
+   - Give the position of the first element in a sorted range with value greater than a given value.
+   - The range of elements that is equal to a given value.
+   - Merge sorted ranges.
+   - Set algorithms (union, intersection, difference, symmetric difference).
+   - Merge consecutive sorted ranges.

# 18.5.1 Binary Search

Binary search in an ordered range is a divide-and-conquer approach. Instead of sequentially searching in a range to determine if a given value is in that range (linear O(n) complexity) we decompose a problem into two or more smaller subproblems. Complexity in this case is logarithmic.

An example of use is:

```
void BinarySearch()
{
    std::cout << "\n** Block I, Binary search\n";
    // I. Binary search
    // Binary search: check ifone element is present. Range must be sorted!
```