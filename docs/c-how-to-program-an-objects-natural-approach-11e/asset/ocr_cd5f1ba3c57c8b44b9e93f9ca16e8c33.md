has 1,000 elements, it requires up to 999 comparisons. As n grows larger, the n part of the expression n - 1 “dominates,” and subtracting one becomes inconsequential. Big O is designed to highlight these dominant terms and ignore terms that become unimportant as n grows. For this reason, an algorithm that requires a total of n - 1 comparisons (such as the one we described earlier) is said to be O(n). An O(n) algorithm is referred to as having a linear running time. O(n) is pronounced “on the order of n” or simply “order n.”

# ### O(n^2) Algorithms

Now suppose you have an algorithm that tests whether any element of an array is duplicated elsewhere in the array. The first element must be compared with all other elements in the array. The second element must be compared with all elements except the first (it was already compared to the first). The third element must be compared with all elements except the first two. In the end, this algorithm makes (n - 1) + (n - 2) + ... + 2 + 1 or n^2/2 - n/2 comparisons. As n increases, the n^2 term dominates, and the n term becomes inconsequential. Again, Big O notation highlights the n^2 term, ignoring n/2.

Big O is concerned with how an algorithm’s running time grows in relation to the number of items processed. Suppose an algorithm requires n^2 comparisons. With four elements, the algorithm requires 16 comparisons; with eight elements, 64 comparisons. With this algorithm, **doubling** the number of elements **quadruples** the number of comparisons. Consider a similar algorithm requiring n^2/2 comparisons. With four elements, the algorithm requires eight comparisons; with eight elements, 32 comparisons. Again, **doubling** the number of elements **quadruples** the number of comparisons. Both of these algorithms grow as the square of n, so Big O ignores the constant factor, and both algorithms are considered to be O(n^2), which is referred to as quadratic running time and pronounced “on the order of n-squared” or simply “order n-squared.”

# ### Efficiency of the Linear Search O(n)

The linear search algorithm, which is typically used for searching an unsorted array, runs in O(n) time. The worst case in this algorithm is that every element must be checked to determine whether the search key exists in the array. If array’s size doubles, the number of comparisons that the algorithm must perform also doubles. Linear search can provide outstanding performance if the element matching the search key is at or near the front of the array. But we seek algorithms that perform well, on average, across all searches, including those where the element matching the search key is at or near the end of the array.

Linear search is easy to program, but it can be slow compared to other search algorithms, especially as n gets large. If a program needs to perform many searches on large arrays, it’s better to use a more efficient algorithm, such as the C++ standard library algorithm binary_search, which we used in Chapter 6 and will use again in Chapter 14. We’ll show how to implement the binary search algorithm in Chapter 21.

Sometimes the simplest algorithms perform poorly. Their virtue often is that they’re easy to program, test and debug. Sometimes more complex algorithms are required to realize maximum performance.

# ### Efficiency of the Binary Search O(log n)

In the worst-case scenario, searching a sorted array of 1,023 elements (2^10 - 1) takes only 10 comparisons with binary search. The algorithm compares the search key to the middle