give a flagged bubble sort an array that is already sorted, it will only run through it once, doing n − 1 comparisons. We would call that O(n). Granted, that is a BEST-CASE scenario. The best-case is rarely of interest. Instead, we typically worry about AVERAGE-CASE and WORST-CASE situations.³

So what are the average and worst-case behaviors of insertion sort? The outer loop clearly happens n − 1 times. So we can do a summation much like what we did above. However, the inner loop happens a variable number of times. In the worst-case, which would be getting data in reverse order, the inner loop will run i times and we get exactly the same behavior as with the bubble and selection sorts. In the best-case, which is data in the proper order, the inner loop does only one check. This gives linear performance, O(n), because

C = Σ_{i=1}^{n-1} 1 = n − 1.

On average we expect something halfway between these extremes, we expect the inner loop to do i/2 comparisons. This gives

C = Σ_{i=1}^{n-1} i/2 = n(n − 1)/4 = 1/4 n² − 1/4 n.

While this is better than the behavior of the other sorts by a factor of two, it is still O(n²). This is because doubling the size of the input still makes it take four times longer and that is what we generally care about the most.

So how good or bad is O(n²)? Functions like this that grow as a polynomial function are referred to in a very general way as being tractable, because you can use them for fairly large values of n and still expect the calculation to finish in a reasonable time. We will see later on that not all algorithms have this behavior. However, O(n²) is not great if the value of n gets extremely large. We have no problem using these sorts for Arrays with 100 or 1000 values. However, as you continue to add zeros, these methods will prove to be too slow. Each factor of 10 in the size causes the program to do 100 times as many comparisons and generally this leads to it taking 100 times longer to complete. As such, these methods become unusable if n gets big enough. Fortunately, there are alternatives.

# 13.1.7 Shell Sort (Diminishing Gap Sort)

The first alternative sort we will look at is the SHELL SORT, also called the diminishing gap sort. This sort was first proposed in 1959 by Donald Shell and it was one of the first general sort algorithms developed that is faster than O(n²), though some minor changes had to be made in order to get that performance for the worst case. The basic idea of this sort is one that might seem a bit counterintuitive. It performs an insertion sort repeatedly on different subsets of the full array. To start with, the subsets are taken to be groups of elements that are widely spaced. The spacing between the elements in each subset is called the “gap”. As the alternate name implies, the gap is then decreased in size for each run through the sort.

The counterintuitive aspect of this sort is that performing insertion sorts multiple times should sort the array faster than doing doing it outright. This can work because a sort with a smaller gap size maintains the ordering at the larger gap size so work is not undone, and the insertion sort is very efficient on partially ordered data. The sorts with large gaps do