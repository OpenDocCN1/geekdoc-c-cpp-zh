b. Give as accurate (Big-Oh) an analysis as you can of the expected running time of each algorithm.
c. Write (separate) programs to execute each algorithm 10 times, to get a good average. Run program (1) for N = 250, 500, 1,000, 2,000; program (2) for N = 25,000, 50,000, 100,000, 200,000, 400,000, 800,000; and program (3) for N = 100,000, 200,000, 400,000, 800,000, 1,600,000, 3,200,000, 6,400,000.
d. Compare your analysis with the actual running times.
e. What is the worst-case running time of each algorithm?

# 2.9 Complete the table in Figure 2.2 with estimates for the running times that were too long to simulate. Interpolate the running times for these algorithms and estimate the time required to compute the maximum subsequence sum of 1 million numbers. What assumptions have you made?

2.10 Determine, for the typical algorithms that you use to perform calculations by hand, the running time to do the following:
a. Add two N-digit integers.
b. Multiply two N-digit integers.
c. Divide two N-digit integers.

2.11 An algorithm takes 0.5 ms for input size 100. How long will it take for input size 500 if the running time is the following (assume low-order terms are negligible)?
a. linear
b. O(N log N)
c. quadratic
d. cubic

2.12 An algorithm takes 0.5 ms for input size 100. How large a problem can be solved in 1 min if the running time is the following (assume low-order terms are negligible)?
a. linear
b. O(N log N)
c. quadratic
d. cubic

2.13 How much time is required to compute f(x) = \sum_{i=0}^N a_i x^i.
a. Using a simple routine to perform exponentiation?
b. Using the routine in Section 2.4.4?

2.14 Consider the following algorithm (known as Horner's rule) to evaluate f(x) = \sum_{i=0}^N a_i x^i.

```
poly = 0;
for ( i = n ; i >= 0 ; -- i )
    poly = x * poly + a[ i ];
```

a. Show how the steps are performed by this algorithm for x = 3, f(x) = 4x^4 + 8x^3 + x + 2.
b. Explain why this algorithm works.
c. What is the running time of this algorithm?