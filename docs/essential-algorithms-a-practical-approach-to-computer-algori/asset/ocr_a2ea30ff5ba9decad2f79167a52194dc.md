the indicated number as a parameter. The figure shows, for example, the call to Fibonacci(6) in the top node calls Fibonacci(5) and Fibonacci(4). If you look at the figure, you can see that the tree is filled with duplicated calls. For example, Fibonacci(0) is calculated five times, and Fibonacci(1) is calculated eight times.

![](bbox=[0.196, 0.206, 0.842, 0.443])

**Figure 9-1:** The Fibonacci algorithm’s call tree is filled with duplicated calculations.

Analyzing this algorithm’s run time is a bit trickier than analyzing the Factorial algorithm’s run time, because this algorithm is multiply-recursive.
Suppose T(N) is the run time for the algorithm on input N. If N > 1, the algorithm calculates Fibonacci(N-1) and Fibonacci(N-2), which performs an extra step to add values, and returns the result. That means T(N) = T(N-1) + T(N-2) + 1.

This is slightly greater than T(N-1) + T(N-2). If you ignore the extra constant 1 at the end, this is the same as the definition of the Fibonacci function, which has a run time at least large as the function itself.

The Fibonacci function doesn’t grow as quickly as the factorial function, but it still grows very quickly. For example, Fibonacci(92) = 7.5x10¹⁸ doesn’t fit in a large integer. That means you can calculate up to Fibonacci(92) with a maximum depth of recursion of 92, which shouldn’t be a problem for most programming environments.

However, the run time of the Fibonacci algorithm grows very quickly. On my computer, calculating Fibonacci(44) takes more than a minute so calculating much larger values of the function is impractical anyway.

# Tower of Hanoi

Chapter 5 introduced the Tower of Hanoi puzzle, with a stack of disks, where each disk is smaller than the one below it, sits on one of three pegs. The