Sec. 7.9 Lower Bounds for Sorting

261

performance for others. They also show that for some algorithms, the order of input has little effect.

These figures show a number of interesting results. As expected, the O($n^2$) sorts are quite poor performers for large arrays. Insertion Sort is by far the best of this group, unless the array is already reversed sorted. Shellsort is clearly superior to any of these O($n^2$) sorts for lists of even 100 elements. Optimized Quicksort is the best overall for all lists but for 10 elements. For small arrays, optimized Quicksort performs well because it does one partition step before Insertion Sort. Compared to the other O($n \log n$) sorts, unoptimized Heapsort is quite slow due to the overhead of the class structure. When all of it is stripped away and the algorithm is implemented to manipulate an array directly, it is still somewhat slower than mergesort. In general, optimizing the various algorithms makes a noticeable improvement for larger array sizes.

Overall, Radix Sort is surprisingly poor performer. If the code had been tuned to use bit shifting of the key value, it would likely improve substantially but would seriously limit the range of elements that the sort could support.

# 7.9 Lower Bounds for Sorting

This book contains many analyses for algorithms. These generally define the upper and lower bounds for algorithms in their worst and average cases. For many of the algorithms presented so far, analysis has been easy. This section considers a more difficult task — analysis for the cost of a problem as opposed to an algorithm. The upper bound for a problem can be defined as the asymptotic cost of the fastest known. The lower bound defines the best possible efficiency for any algorithm that solves the problem, including algorithms not yet invented. Once the upper and lower bounds for the problem meet, we know that no algorithm can possibly be (asymptotically) more efficient.

A simple estimate for a problem's lower bound can be obtained by measuring the size of the input and the output that must be written. Certainly no algorithm can be more efficient than the problem's I/O time. From this we see that the sorting problem cannot be solved by any algorithm in less than Ω($n$) because it takes $n$ steps to read and write the $n$ values to be sorted. Alternatively, any sorting algorithm must least look at every input value to recognize whether the input values are in sort order. Based on our current knowledge of sorting algorithms and the size of the input, we know that the problem of sorting is bounded by Ω($n$) and O($n \log n$).

Computer scientists have spent much time devisinging efficient general-purpose sorting algorithms, but no one has ever found one that is faster than O($n \log n$) in the worst or average cases. Should we keep searching for a faster sorting algorithm?