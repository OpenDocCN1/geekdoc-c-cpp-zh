![](bbox=[0.18, 0.09, 0.92, 0.58])

# Figure 7.14 An illustration of Quicksort.

total of s steps for a subarray of length s. However, this does not directly tell us how much work is done by the nested while loops. The do loop as a whole is guaranteed to move both l and r inward at least one position on each first pass. Each while loop moves its variable at least once (except in the special case where r is at the left edge of the array, but this can happen only once). Thus, we see that the do loop can be executed at most s times, the total amount of work done moving l and r is s, and each while loop can fail its test at most s times. The total work for the entire partition function is therefore Θ(s).

Knowing the cost of findpivot and partition, we can determine the cost of Quicksort. We begin with a worst-case analysis. The worst case will occur when the pivot does a poor job of breaking the array, that is, when there are no elements in one partition, and n − 1 elements in the other. In this case, the divide and conquer strategy has done a poor job of dividing, so the conquer phase will work on a subproblem only one less than the size of the original problem. If this happens at each partition step, then the total cost of the algorithm will be ∑_{k=1}^{n} k = Θ(n²).

In the worst case, Quicksort is Θ(n²). This is terrible, no better than Bubble Sort.² When will this worst case occur? Only when each pivot yields a bad partitioning of the array. If the pivot values are selected at random, then this is extremely unlikely to happen. When selecting the middle position of the current subarray, it

> ²The worst insult that I can think of for a sorting algorithm.