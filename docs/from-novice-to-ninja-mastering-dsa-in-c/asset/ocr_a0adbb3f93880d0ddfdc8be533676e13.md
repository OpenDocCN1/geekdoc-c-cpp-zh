# Efficient Sorting: Merge Sort, Quick Sort

# The Need for Efficient Sorting:

While fundamental sorting algorithms serve their purpose, they may become impractical for large datasets. Efficient sorting algorithms address this limitation, offering improved time complexity and performance.

# Merge Sort:

Principle: A divide-and-conquer algorithm that recursively divides the array into halves until each sub-array contains a single element. It then merges these sub-arrays in a sorted manner until the entire array is sorted.

# Process:

+   1. Divide the array into two halves.
+   2. Recursively apply the merge sort algorithm to each half.
+   3. Merge the sorted halves to produce the final sorted array.

Time Complexity: O(n log n) in the worst and average cases.

# Example:

```
Original Array: 5 2 9 1 5
Divide: 5 2 | 9 1 5
Divide: 5 | 2     9 | 1 5
Merge: 2 5     1 5 9
Merge: 1 2 5 5 9
```

# Quick Sort:

Principle: Also, a divide-and-conquer algorithm, quicksort selects a "pivot" element and partitions the array into two sub-arrays: elements less than the pivot and elements greater than the pivot. The process is then applied recursively to each sub-array.

# Process:

+   1. Choose a pivot element from the array.
+   2. Partition the array into elements less than and greater than the pivot.
+   3. Recursively apply the quicksort algorithm to the two sub-arrays.
+   4. Concatenate the sorted sub-arrays.

Time Complexity: O(n log n) in the average case, O(n^2) in the worst case (can be mitigated with randomized pivot selection).

# Example:

```
Original Array: 5 2 9 1 5
```