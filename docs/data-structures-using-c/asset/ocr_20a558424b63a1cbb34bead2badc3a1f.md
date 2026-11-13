In brief, we follow the following three steps:

+   1. Partition A and B into quarter matrices.
+   2. Compute the intermediate matrices:
+      (a) If sizes of the matrices are greater than a threshold value, multiply them recursively using Strassen's algorithm.
+      (b) Else, use the traditional matrix multiplication algorithm.
+   3. Construct C using the intermediate matrices.

With this construction, we have not yet reduced the number of multiplications. We still needed eight multiplications to calculate the Cij matrices; the same number of multiplications needed while using the standard matrix multiplication. We iterate this division process n times until the submatrices degenerate into numbers.

Practical implementations of Strassen's algorithm result in standard methods of matrix multiplication for smaller submatrices, for which those algorithms are more efficient.

Let us compute the time complexity of this algorithm. The standard matrix multiplication takes approximately 2N^3 (where N = 2^n) arithmetic operations (additions and multiplications); the asymptotic complexity is O(N^3). The number of additions and multiplications required in the Strassen's algorithm can be calculated as follows:

Let f(n) be the number of operations for a 2^n x 2^n matrix. Then, by recursive application of the Strassen's algorithm, we see that T(n) = 7T(n-1) + 4n for some constant that depends on the number of additions performed at each application of the algorithm. Hence, T(n) = (7 + O(1))n, that is, the asymptotic complexity for multiplying matrices of size N = 2^n using the Strassen's algorithm is

```
O([7 + O(1)]^n) = O(N^{log2 7 + O(1)}) ≈ O(N^{2.807})
```

Note the reduction in the number of arithmetic operations achieved at the additional cost of reduced numerical stability.

# 16.3 GREEDY METHOD

A greedy method is any algorithm that follows the problem-solving heuristic of making the locally optimal choice at each stage with the hope of finding the optimum solution. For example, applying the greedy strategy to the traveling salesman problem yields the following algorithm: 'At each stage, visit the unvisited city nearest to the current city.' In general, greedy algorithms are used for optimization problems. Often, we look at optimization problems whose performance is exponential. A feasible solution to which the optimization function has the best possible value is called an optimal solution.

In greedy method, we attempt to construct an optimal solution in the sequence of choice. At each choice, we make a decision that appears to be the best at that time. A decision made at one choice is not changed at a later choice, so each decision should