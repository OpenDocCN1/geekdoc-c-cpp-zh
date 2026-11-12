```
{
k = jth digit of theArray[i]
Place theArray[i] at the end of group k
Increase kth counter by 1
}
Replace the items in theArray with all the items in group 0,
followed by all the items in group 1, and so on.
}
```

# **Question 11** Trace the radix sort as it sorts the following array into ascending order:
3812 1600 4012 3934 1234 2724 3333 5432

**Analysis.** From the pseudocode for the radix sort, you can see that this algorithm requires n moves each time it forms groups and n moves to combine them again into one group. The algorithm performs these 2 * n moves d times. Therefore, the radix sort requires 2 * n * d moves to sort n strings of d characters each. However, notice that no comparisons are necessary. Thus, radix sort is O(n).

Despite its efficiency, the radix sort has some difficulties that make it inappropriate as a general-purpose sorting algorithm. For example, to perform a radix sort of strings of uppercase letters, you need to accommodate 27 groups—one group for blanks and one for each letter. If the original data collection contains n strings, each group must be able to hold n strings. For large n, this requirement demands substantial memory if you use arrays for both the original data and the resulting groups. However, you can save memory by using a chain of linked nodes for each of the 27 groups. Thus, a radix sort is more appropriate for a chain than for an array.

> Even though the radix sort is O(n), it is not appropriate as a general-purpose sorting algorithm

# 11.3 A Comparison of Sorting Algorithms

Figure 11-15 summarizes the time required in the worst case and average case for the sorting algorithms that appear in this chapter. For reference purposes, two other algorithms—the tree sort and heap sort—are included here, even though you will not study them until Chapters 15 and 17, respectively.

# FIGURE 11-15 Approximate growth rates of time required for eight sorting algorithms

| | Worst case | Average case |
|---|---|---|
| Selection sort | n² | n² |
| Bubble sort | n² | n² |
| Insertion sort | n² | n² |
| Merge sort | n * log n | n * log n |
| Quick sort | n² | n * log n |
| Radix sort | n | n |
| Tree sort | n² | n * log n |
| Heap sort | n * log n | n * log n |

> **Note:** The Standard Template Library (STL) provides several sort functions in the library header `<algorithm>`. Consult C++ Interlude 7 for more information about the STL and these functions.