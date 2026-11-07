+   - The first iteration of insertion sort takes the second element value and, if it’s less than the first, swaps it with the first. The second iteration looks at the third element value and inserts it in the correct position with respect to the first two element values. After the *j*th iteration of insertion sort, the first *j* element values in the original vector are sorted. Only *n* − 1 iterations are required.
+   - The insertion sort algorithm runs in *O(n²)* time.

# Section 19.3.3 Merge Sort (A Recursive Implementation)

+   - Merge sort (p. 733) is faster, but more complex to implement, than selection sort and insertion sort.
+   - The merge sort algorithm sorts a vector by splitting the vector into two equal-sized subvectors, sorting each subvector and merging the subvectors into one larger vector.
+   - Merge sort’s base case is a vector with one element. A one-element vector is already sorted, so merge sort immediately returns when it’s called with a one-element vector. The merge part of merge sort takes two sorted vectors (these could be one-element vectors) and combines them into one larger sorted vector.
+   - Merge sort performs the merge by looking at the first element in each vector, which is also the smallest element in the vector. Merge sort takes the smallest of these and places it in the first element of the larger, sorted vector. If there are still elements in the subvector, merge sort looks at the second element in that subvector (which is now the smallest element remaining) and compares it to the first element in the other subvector. Merge sort continues this process until the larger vector is filled.
+   - In the worst case, the first call to merge sort has to make *O(n)* comparisons to fill the *n* slots in the final vector.
+   - The merging portion of the merge sort algorithm is performed on two subvectors, each of approximately size *n/2*. Creating each of these subvectors requires *n/2 − 1* comparisons for each subvector, or *O(n)* comparisons total. This pattern continues, as each level works on twice as many vectors, but each is half the size of the previous vector.
+   - Similar to binary search, this halving results in log *n* levels, each level requiring *O(n)* comparisons, for a total efficiency of *O(n log n)* (p. 740).

# Self-Review Exercises

+   1. **19.1** Fill in the blanks in each of the following statements:
+      a) A selection sort application would take approximately __________ times as long to run on a 128-element vector as on a 32-element vector.
+      b) The efficiency of merge sort is __________.
+   2. **19.2** What key aspect of both the binary search and the merge sort accounts for the logarithmic portion of their respective Big Os?
+   3. **19.3** In what sense is the insertion sort superior to the merge sort? In what sense is the merge sort superior to the insertion sort?
+   4. **19.4** In the text, we say that after the merge sort splits the vector into two subvectors, it then sorts these two subvectors and merges them. Why might someone be puzzled by our statement that “it then sorts these two subvectors”?

# Answers to Self-Review Exercises

**19.1** a) 16, because an *O(n²)* algorithm takes 16 times as long to sort four times as much information. b) *O(n log n)*.