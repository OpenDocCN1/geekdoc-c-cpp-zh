+   - Big O is designed to highlight dominant factors and ignore terms that become unimportant with high values of n.

+   - Big O notation is concerned with the growth rate of algorithm run times, so constants are ignored.

# ### Section D.3 Selection Sort

+   - Selection sort (p. 938) is a simple, but inefficient, sorting algorithm.

+   - The first iteration of selection sort selects the smallest element in the array and swaps it with the first element. The second iteration of selection sort selects the second-smallest element (which is the smallest of those remaining) and swaps it with the second element. Selection sort continues until the last iteration selects the second-largest element and swaps it with the second-to-last, leaving the largest element as the last. At the ith iteration of selection sort, the smallest i elements of the whole array are sorted into the first i positions of the array.

+   - The selection sort algorithm runs in O(n²) time (p. 941).

# ### Section D.4 Insertion Sort

+   - The first iteration of insertion sort (p. 942) takes the second element in the array and, if it’s less than the first element, swaps it with the first element. The second iteration of insertion sort looks at the third element and inserts it in the correct position with respect to the first two elements. After the ith iteration of insertion sort, the first i elements in the original array are sorted. Only n − 1 iterations are required.

+   - The insertion sort algorithm runs in O(n²) time (p. 945).

# ### Section D.5 Merge Sort

+   - The merge sort algorithm (p. 945) is faster, but more complex to implement, than selection sort and insertion sort.

+   - The merge sort algorithm sorts an array by *splitting* the array into two equal-sized subarrays, sorting each subarray and *merging* the subarrays into one larger array.

+   - Merge sort’s base case is an array with one element, which is already sorted, so merge sort immediately returns when it’s called with a one-element array. The merge part of merge sort takes two sorted arrays (these could be one-element arrays) and combines them into one larger sorted array.

+   - Merge sort performs the merge by looking at the first element in each array, which is also the smallest element. Merge sort takes the smallest of these and places it in the first element of the larger, sorted array. If there are still elements in the subarray, merge sort looks at the second element in that subarray (which is now the smallest element remaining) and compares it to the first element in the other subarray. Merge sort continues this process until the larger array is filled.

+   - In the worst case, the first call to merge sort has to make O(n) comparisons to fill the n slots in the final array.

+   - The merging portion of the merge sort algorithm is performed on two subarrays, each of approximately size n/2. Creating each of these subarrays requires n/2 − 1 comparisons for each subarray, or O(n) comparisons total. This pattern continues, as each level of work on twice as many arrays, but each is half the size of the previous array.

+   - This halving results in log n levels, each level requiring O(n) comparisons, for a total efficiency of O(n log n) (p. 951), which is far more efficient than O(n²).

# ## Self-Review Exercises

**D.1** Fill in the blanks in each of the following statements:

+   a) A selection sort application would take approximately ______ times as long to run on a 128-element array as on a 32-element array.
+   b) The efficiency of merge sort is ______.