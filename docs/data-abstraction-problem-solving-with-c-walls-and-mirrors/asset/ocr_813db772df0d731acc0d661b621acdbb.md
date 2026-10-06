# 296 CHAPTER 10 Algorithm Efficiency

To dramatize further the significance of an algorithm's proportional growth rate, consider the table and graph in Figure 10-3. The table in part *a*, for various values of *n*, the approximate values of some growth-rate functions, which are listed in order of:

Order of growth of some common functions

```
$O(1) < O(\log n) < O(n) < O(n \times \log n) < O(n^2) < O(2^n)$
```

The table demonstrates the relative speed with which the values of the functions grow. Figure 10-3 shows these growth-rate functions have the following intuitive interpretations:\^2

Intuitive interpretations of growth-rate functions

+   - A growth-rate function of 1 implies a problem whose time requirement is constant and, independent of the problem's size n.

+   - The time requirement for a logarithmic algorithm increases slowly as the problem size increases. If you square the problem size, you only double its time requirement. You will see that you studied in Chapter 2 has this behavior. Recall that a binary search halves an array and searches for one of the halves. Typical logarithmic algorithms solve a problem by solving a smaller constant fraction of the problem.

+   - The base of log does not affect a logarithmic growth rate, so you can omit it in a growth-rate function. Exercise 8 at the end of this shows you why this is true.

+   - The time requirement for an $O(n)$, or **linear**, increases directly with the size of the problem. If you square the problem size, you square its time requirement.

+   - The time requirement for an $O(n \times \log n)$ increases more rapidly than linear algorithm. Each algorithm usually divides a problem into smaller problems that are each solved separately. The next chapter examines an example of this algorithm type—the merge sort.

+   - The time requirement for an $O(n^2)$, or **quadratic**, increases more rapidly with the size of the problem. Algorithms that use two nested loops are often quadratic. Algorithms are practical only for small problems. The next chapter covers several sorting algorithms.

+   - As the size of a problem increases, the time requirement for an **exponential** algorithm usually increases too rapidly to be practical.

If algorithm A requires time that is proportional to function $f$ and algorithm $B$ requires time that is proportional to a slower-growing function $g$, it is apparent that $B$ is always more efficient than $A$ for enough problems. For large problems, the proportional growth rate dominates all other factors in determining an algorithm's efficiency.

**Properties of growth-rate functions.** Several mathematical properties of Big O notation help simplify the analysis of an algorithm. As we discuss these properties

> 2 The graph of $f(n)=1$ is omitted because the scale of the figure makes it difficult to draw. It would, however, be a straight line parallel to the x axis where $y=1$.