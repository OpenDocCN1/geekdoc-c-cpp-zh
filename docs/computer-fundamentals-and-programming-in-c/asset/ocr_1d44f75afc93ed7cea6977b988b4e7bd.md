# 12.12.5 Analysis of Quick Sort

In quick sort, each recursive call could have a different sized set of numbers to sort. Here are the three analyses that must be performed:

+   - Best case
+   - Average case
+   - Worst case

In the best case, a perfect partition is to be set every time. If we let T(n) be the running time of quick sorting n elements, then T(n) = 2T(n/2) + O(n), since partition runs in O(n) time.

Now, consider how bad quick sort would be if the partition element was always the greatest value of the one remaining to be sorted. In this situation, one has to run partition n − 1 times, the first time comparing n − 1 values, then n − 2, followed by n − 3, etc. This points to the sum 1+2+3+…+(n−1) which is (n−1)n/2. Thus, the worst case running time is O(n²).

Now, let us calculate the average-case running time. This is certainly difficult to ascertain because one cannot get any sort of partition. It is assumed that each possible partition (0 and n−1, 1 and n−2, 2 and n−3, etc.) is equally likely. One way to work out the mathematics is as follows. Assume that you run quick sort n times. In doing so, since there are n possible partitions, each equally likely, on average, each partition occurs once. So, the following recurrence relation is found:

nT(n) = T(0)+T(n−1)+T(1)+T(n−2)+…+T(n−1)+T(0) + n²

= 2[T(1)+T(2)+…+T(n−1)] + n²  (12.1)

Now, putting n−1 in Eqn (12.1),

(n−1)T(n−1) = 2[T(1)+T(2)+…+T(n−2)] + (n−1)²  (12.2)

Subtracting Eqn (12.2) from Eqn (12.1), gives

nT(n) − (n−1)T(n−1) = 2T(n−1) + 2n − 1 + n²

= (n+1)T(n−1) + (2n − 1)

T(n) = [(n+1)/n]T(n−1) + (2n − 1)/n  (12.3)

Since it is an approximate analysis, the −1 is dropped at the end of this equation. Dividing Eqn (12.3) by n+1, yields

T(n)/(n+1) = T(n−1)/n + 2/(n+1)  (12.4)

Now, substituting different values of n into this recurrence to form several equations, it evaluates to

T(n)/(n+1) = T(n−1)/n + 2/(n+1)T(n−1)/n
= T(n−2)/(n−1) + 2/n

T(n−2)/(n−1) = T(n−3)/(n−2) + 2/(n−1)

T(2)/3 = T(1)/2 + 2/1

Now, summing up as the equations above reveal many identical terms on both sides. In fact, after cancelling identical terms, we are left with

T(n)/(n+1) = T(1)/2 + 2[1/4 + 1/2 + 1/3 + … + 1/(n+1)]

The sum on the right hand side of the equation is a harmonic number. The nth harmonic number (Hₙ) is defined as

1 + 1/2 + 1/3 + … + 1/n.

Through calculus, it can be shown that Hₙ ~ ln n (ln is the natural log with the base e; e ~ 2.718282). Now,

T(n)/(n+1) ~ 1/2 + 2 ln n
T(n) ~ n(ln n) (simplifying a bit)

Thus, even in the average case for quick sort, it is found that T(n) = O(n log n).

Note, in order analysis, any function of the form logₐₙ = O(log n), for all positive constants b and c, is greater than 1.

Let us look at the best-case complexity. The best case occurs when the pivot is the median value; thus the two recursive calls are problems with approximately half the size of the original problem. This recurrence is given by

T(n) = 2T(n/2) + 2 + O(n) = O(n log n)

We derive this best-case performance figure to be

c * n * log n + n

where c represents the constant pivot selection time.

The main consideration is quick sort’s average performance. This has been shown (see Kruse et al.) to be 1.39 * n log n + c * n.

For quick sort, best case is T(n) = O(n log n), worse case is T(n) = O(n²), and average case is T(n) = O(n log n).

# 12.12.6 Disadvantages of Complexity Analysis

Complexity analysis can be very useful, but there are problems with it too. The disadvantages of complexity analysis are as follows.

+   - Many algorithms are simply too hard to analyse mathematically.
+   - The average case is unknown. There may not be sufficient information to know what the most important ‘average’ case really is, therefore analysis is impossible.
+   - Big-O analysis only specifies how it grows with the size of the problem, not how efficient it is.
+   - If there are no large amounts of data, algorithm efficiency may not be important.