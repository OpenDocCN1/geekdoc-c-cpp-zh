elements *quadruples* the number of comparisons. Consider a similar algorithm requiring n²/2 comparisons. With four elements, the algorithm will require eight comparisons; with eight elements, the algorithm will require 32 comparisons. Again, doubling the number of elements *quadruples* the number of comparisons. Both algorithms grow as the square of *n*, so Big O ignores the constant and both algorithms are considered to be *O*(*n*²). This is referred to as quadratic run time and pronounced "on the order of *n*-squared" or simply "order *n*-squared."

When *n* is small, *O*(*n*²) algorithms (running on today's billion-operations-per-second personal computers) will not noticeably affect performance. But as *n* grows, you'll start to notice the performance degradation. An *O*(*n*²) algorithm running on a million-element array would require a trillion "operations," where each could actually require several machine instructions to execute. This could require a few hours to execute. A billion-element array would require a quintillion operations, a number so large that the algorithm could take decades! As you'll see in this chapter, *O*(*n*²) algorithms are easy to write. You'll also see an algorithm with a more favorable Big O measure. Efficient algorithms often require clever coding and more work to create. Their superior performance can be well worth the extra effort, especially as *n* gets large and as algorithms are combined into larger programs.

# ## Self Check

+   1. *(True/False)* *O*(*n*²) algorithms running on today's billion-operations-per-second personal computers will not noticeably affect performance.
+   Answer: *False.* Actually, when *n* is *small*, *O*(*n*²) algorithms will not noticeably affect performance. But as *n* grows, you'll start to notice the performance degradation, even on today's powerful systems.
+   
+   2. *(Fill-In)* Big O is concerned with how an algorithm's run time grows in relation to the ______.
+   Answer: number of items processed.
+   
+   3. *(True/False)* An algorithm that is *O*(1) requires only one comparison.
+   Answer: *False.* *O*(1) means the number of comparisons is *constant*. The algorithm may require multiple comparisons, but that number does not grow as the array's size increases.
+   
+   4. *(Fill-In)* An *O*(*n*) algorithm is referred to as having a ______ run time.
+   Answer: linear.
+   
+   5. *(Fill-In)* An *O*(*n*²) algorithm is referred to as having ______ run time.
+   Answer: quadratic.

# ## 13.3 Selection Sort

Selection sort is a simple but inefficient sorting algorithm:

+   - The algorithm's first iteration selects the array's smallest element and swaps it with the array's first element.