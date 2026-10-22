# 7.2 Write an Insertion Sort algorithm for integer key values. However, here’s the catch: The input is a stack (not an array), and the only variables that your algorithm may use are a fixed number of integers and a fixed number of stacks. The algorithm should return a stack containing the records in sorted order (with the least value being at the top of the stack). Your algorithm should be Θ(n²) in the worst case.

# 7.3 The Bubble Sort implementation has the following inner for loop:

```
for (int j=n-1; j>i; j--)
```

Consider the effect of replacing this with the following statement:

```
for (int j=n-1; j>0; j--)
```

Would the new implementation work correctly? Would the change affect the asymptotic complexity of the algorithm? How would the change affect the running time of the algorithm?

# 7.4 When implementing Insertion Sort, a binary search could be used to locate the position within the first i − 1 elements of the array into which element i should be inserted. How would this affect the number of comparisons required? How would using such a binary search affect the asymptotic running time for Insertion Sort?

# 7.5 Figure 7.5 shows the best-case number of swaps for Selection Sort as Θ(n). This is because the algorithm does not check to see if the i th record is already in the i th position; that is, it might perform unnecessary swaps.

+   (a) Modify the algorithm so that it does not make unnecessary swaps.
+   (b) What is your prediction regarding whether this modification actually improves the running time?
+   (c) Write two programs to compare the actual running times of the original Selection Sort and the modified algorithm. Which one is actually faster?

# 7.6 Recall that a sorting algorithm is said to be stable if the original ordering for duplicate keys is preserved. Of the sorting algorithms Insertion Sort, Bubble Sort, Selection Sort, Shellsort, Mergesort, Quicksort, Heapsort, Binsort, and Radix Sort, which of these are stable, and which are not? For each one, describe either why it is or is not stable. If a minor change to the implementation would make it stable, describe the change.

# 7.7 Recall that a sorting algorithm is said to be stable if the original ordering for duplicate keys is preserved. We can make any algorithm stable if we alter the input keys so that (potentially) duplicate key values are made unique in a way that the first occurrence of the original duplicate value is less than the second occurrence, which in turn is less than the third, and so on. In the worst case, it is possible that all n input records have the same key value. Give an