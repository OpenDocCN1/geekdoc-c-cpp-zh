# Analysis of Algorithm Complexity

Algorithms usually possess the following qualities and capabilities:

+   - Easily modifiable if necessary.
+   - They are correct for clearly defined solution.
+   - Require less computer time, storage and peripherals, i.e. they are more economical.
+   - They are documented well enough to be used by others who do not have a detailed knowledge of the inner working.
+   - The solution is pleasing and satisfying to its designer and user.
+   - They are able to be used as a sub-procedure for other problems.

Two or more algorithms can solve the same problem in different ways. So, quantitative measures are valuable in that they provide a way of comparing the performance of two or more algorithms that are intended to solve the same problem. This is an important step because the use of an algorithm that is more efficient in terms of time, resources required, can save time and money.

# Computational Algorithm Complexity

We can characterize an algorithm’s performance in terms of the size (usually n) of the problem being solved. More computing resources are needed to solve larger problems in the same class. Table 3.1 illustrates the comparative cost of solving the problem for a range of n values.

Table 3.1 shows that only very small problems can be solved with an algorithm that exhibit exponential behavior. An exponential problem with n = 100 would take immeasurably longer time. At the other extreme, for an algorithm with logarithmic dependency would merely take much less time (13 steps in case of log₂n in Table 3.1). These examples

| log₂n | n | nlog₂n | n² | n³ | 2ⁿ |
|---:|---:|---:|---:|---:|---:|
| 1 | 2 | 2 | 4 | 8 | 4 |
| 3.322 | 10 | 33.22 | 10² | 10³ | >10³ |
| 6.644 | 10² | 664.4 | 10⁴ | 10⁶ | >>10²⁵ |
| 9.966 | 10³ | 9966.0 | 10⁶ | 10⁹ | >>10³⁰ |
| 13.287 | 10⁴ | 132877 | 10⁸ | 10¹² | >>10²⁵⁰⁰ |

emphasize the importance of the way in which algorithms behave as a function of the problem size. Analysis of an algorithm also provides the theoretical model of the inherent computational complexity of a particular problem.

To decide how to characterize the behavior of an algorithm as a function of size of the problem n, we must study the mechanism very carefully to decide just what constitutes the dominant mechanism. It may be the number of times a particular expression is evaluated, or the number of comparisons or exchanges that must be made as n grows. For example, comparisons, exchanges, and moves count most in sorting algorithm. The number of comparisons usually dominates so we use comparisons in the computational model for sorting algorithms.

# The Order of Notation

The O-notation gives an upper bound on a function within a constant factor. For a given function g(n), we denote by O (g (n)) the set of functions. O (g (n)) = {f (n) : there exist positive constants c and n₀, such that 0 ≤ f (n) ≤ cg (n) for all n ≥ n₀}

Using the O-notation, we can often describe the running time of an algorithm merely by inspecting the algorithm’s overall structure. For example, a double nested loop structure of the following algorithm immediately yields O(n²) upper bound on the worst case running time.

```
for i=0 to n
    for j=0 to n
        print i,j
        next j
    next i
```

What we mean by saying “the running time is O(n²)” is that the worst case running time (which is a function of n) is O(n²). Or equivalently, no matter what the particular input of size n is chosen for each value of n, the running time on that set of inputs is O(n²).

# Rules for Using Big-O Notation

Big-O bounds, because they ignore constants, usually allow for very simple expression for the running time bounds. Below are some