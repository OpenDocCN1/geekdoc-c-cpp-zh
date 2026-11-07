case, by using a comparison-based algorithm to recognize whether an element *x* is in *L*, then $SRH(n) \geq \log_2(n + 1)$.

+   13. The binary search algorithm has the optimal worst-case algorithm for solving search problems by using the comparison method.
+   
+   14. To construct a search algorithm of the order less than $\log_2 n$, it cannot be comparison based.
+   
+   15. For a list of length $n$, on average, bubble sort makes $\frac{n(n-1)}{2}$ key comparisons and about $\frac{n(n-1)}{4}$ item assignments.
+   
+   16. The selection sort algorithm sorts a list by finding the smallest (or equivalently largest) element in the list and then moving it to the beginning (or end) of the list.
+   
+   17. For a list of length $n$, where $n > 0$, the selection sort algorithm makes $\frac{1}{2}n^2 - \frac{1}{2}n$ key comparisons and $3(n-1)$ item assignments.
+   
+   18. For a list of length $n$, where $n > 0$, on average, the insertion sort algorithm makes $\frac{1}{4}n^2 + O(n)$ key comparisons and $\frac{1}{4}n^2 + O(n)$ item assignments.
+   
+   19. Let $L$ be a list of $n$ distinct elements. Any sorting algorithm that sorts $L$ by comparison of the keys only, in its worst case, makes at least $\Omega(n\log_2 n)$ key comparisons.
+   
+   20. Both the quick sort and merge sort algorithms sort a list by partitioning it.
+   
+   21. To partition a list, the quick sort algorithm first selects an item from the list called *pivot*. The algorithm then rearranges the elements so that the elements in one of the sublists are less than *pivot* and the elements in the other sublist are greater than or equal to *pivot*.
+   
+   22. In a quick sort, the sorting work is done in partitioning the list.
+   
+   23. On average, the number of key comparisons in a quick sort is $O(n\log_2 n)$. In the worst case, the number of key comparisons in a quick sort is $O(n^2)$.
+   
+   24. The merge sort algorithm partitions the list by dividing it in the middle.
+   
+   25. In a merge sort, the sorting work is done in merging the list.
+   
+   26. The number of key comparisons in a merge sort is $O(n\log_2 n)$.

# EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

+   1. Mark the following statements as true or false.
+      a. The member that uniquely identifies a data item is called the key of that data item. (1)