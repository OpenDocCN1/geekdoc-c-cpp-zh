At a point like this, we want to copy the elements remaining in the non-empty half into the temporary array. This yields the following final version of our pseudocode for the merge function:

+   1. Initialize copied, copied1, and copied2 to 0.
+   2. while (both halves of the array have more elements to copy)
+      if (data[copied1] <= (data + n1)[copied2])
+      temp[copied++] = data[copied1++];
+      else
+      temp[copied++] = (data + n1)[copied2++];
+   3. Copy any remaining entries from the left or right subarray.
+   4. Copy the elements from temp back to data.

This pseudocode translates to the C++ function shown in Figure 13.3. The only additional items deal with allocating the memory for the temporary array. This temporary array is a dynamic array containing n1 + n2 elements. At the end of the function, the dynamic array is released via the delete operator.

# Dynamic Memory Usage in Mergesort

During a mergesort, our merge function will be called many times. A complete analysis would show that a mergesort of an n-element array makes O(n) calls to the merge function. Each call to merge allocates a temporary dynamic array, uses the array, and then releases the array. With some computers, this repeated allocation and release of dynamic memory takes a significant amount of execution time. A solution is given in Programming Project 6 on page 681.

# Mergesort—Analysis

A complete analysis of mergesort's running time is beyond the scope of this book, but we can give the final result and hint at its derivation. First the result:

| Mergesort Running Time |
| :--- |
| The worst-case running time, the average-case running time, and the best-case running time for mergesort are all O(n log n). |

As usual, n is the number of items to be sorted. Let us try to motivate this formula. In the case of the mergesort, the algorithm performs similarly on all inputs; so our motivation will apply to both the worst-case, average-case, and best-case running times. Let's diagram the first few levels of recursive calls made by a typical mergesort: