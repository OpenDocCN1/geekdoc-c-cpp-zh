In this chapter, we will discuss different sorting techniques to sort data elements of the array in ascending order.

There are many different sorting techniques such as

+   1. Bubble Sort
+   2. Insertion Sort
+   3. Selection Sort
+   4. Quick Sort
+   5. Merge Sort
+   6. Heap Sort
+   7. Shell Sort
+   8. Radix Sort
+   9. Bucket Sort
+   10. Counting Sort

# Internal and External Sorting

When the list of elements or records to be sorted are small enough to be accommodated in the internal (primary) memory of the computer, then it is referred to as internal sorting. Bubble sort, insertion sort, selection sort, merge sort, shell sort, quick sort, heap sort, radix sort are internal sorting techniques.

On the other hand, if the list of elements or records to be sorted in files is accommodated in external storage devices (secondary memory, such as hard disks) then the sorting is referred to as external sorting. One example of external sorting is the external merge sort algorithm.

# In-Place and Stable Sorting

The sorting algorithms can be divided into two main classes: In-Place and Stable.

A sorting algorithm is in-place only if a constant amount of data elements of an input array is never stored outside the array. No additional storage is required and hence it is possible to sort a large list without the need of additional array for storage. Bubble sort, insertion sort, selection sort, Quick sort and Heap sort are in-place sorting algorithms. Merge-sort is not an in-place algorithm, as it requires extra array storage.

| 7 | 3 | 1 | 3 | 2 | 5 | 1 | 8 | 5 | 2 | 2 | 1 | 3 | 1 |

(a)

| 1 | 2 | 2 | 3 | 1 | 3 | 2 | 3 | 3 | 5 | 1 | 5 | 2 | 7 | 8 |

(b)

| 1 | 2 | 2 | 3 | 2 | 3 | 1 | 3 | 3 | 3 | 5 | 2 | 5 | 1 | 7 | 8 |

(c)

**Figure 10.3:** (a) Unsorted list, (b) Stable sort, (c) Unstable sort

A sorting algorithm is said to be stable if two elements that are equal (i.e. duplicate element) remain in the same relative order even after performing sorting. Suppose K1 and K2 are two keys such that k1 = k2, and POS (K1) > POS (K2) where POS (K1) is the position of the keys in the unsorted list, then after sorting, POS (K1) < POS (K2) where POS (K1) is the position of the keys in the sorted list.