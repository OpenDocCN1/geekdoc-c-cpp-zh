In the worst case of quick sort n passes and each pass n number of comparisons are required.

Average-case time complexity: In average case, not always get evenly balanced partitions, but always get at worst a 3-to-1 split on an average. Let, each time we get one partition with n/4 elements and other partition with 3n/4 elements. The tree of subproblem sizes and partitioning time looks like the following figure.

![](bbox=[0.15, 0.18, 0.85, 0.55])

Figure 10.10: Subprogram size in Quick Sort for average case

There are maximum log4/3 n levels in the tree and partitioning time for every level at most cn. Therefore, if all the splits are 3-to-1 then total average running time is cnlog4/3 n = cn / log 4/3 * log n = O(nlog n).

| Quick Sort algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| | O(nlog n) | O(nlog n) | O(n^2) |

In the quicksort, the leftmost element of the array would often be chosen as the pivot element. However, for this reason, when the array is sorted then the time complexity becomes O (n ^2) in worst-case, which is a rather common use-case. The problem was easily solved by either choosing a random index for the pivot or choosing the middle index of the partition or (especially for longer partitions) choosing the median of the first, middle and last element of the partition for the pivot. Then the time complexity will become O (n log n) in worst case.

# Merge Sort

Mergesort algorithm is a classic example of recursive divide and conquer. This algorithm was invented by John von Neumann. As the merging operation is performed in this sorting technique, hence it is