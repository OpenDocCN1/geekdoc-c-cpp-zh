We can generalize this example so that the average-case running time of the serial search is written as an expression with part of the expression being the size of the array. Using n as the size of the array, this expression for the average-case running time is

(1 + 2 + ... + n) / n = (n(n + 1)/2) / n = (n + 1) / 2

The first equality in this formula is obtained from the formula that we developed on page 19. We can summarize the average-case running time for serial search:

# Average-Case Time for Serial Search

For an array of n elements, the average-case time for serial search to find an element that is in the array requires (n + 1) / 2 array accesses.

You may have noticed that both the worst-case time and the average-case time are O(n) expressions; nevertheless, the average case is about half the time of the worst case.

best case

A third way to measure running times is called best-case running time, and as the name name suggests, it takes the most optimistic view possible. The best-case running time is defined as the smallest of all the running times on inputs of a particular size. For serial search, the best case occurs when the target is found at the front of the array, requiring only one array access:

# Best-Case Time for Serial Search

For an array of n elements, the best-case time for serial search is just one array access.

Unless the best-case behavior occurs with high probability, the best-case running time generally is not used during an analysis.

# Binary Search

Serial search is easy to implement, easy to analyze, and fine to use if you are only searching a small array a few times. However, if a search algorithm will be used over and over, it is worthwhile to find a faster algorithm. A dramatically faster search algorithm is sometimes available. The algorithm, called binary search, may be used only if the array is sorted. Here are three examples for which binary search is applicable: