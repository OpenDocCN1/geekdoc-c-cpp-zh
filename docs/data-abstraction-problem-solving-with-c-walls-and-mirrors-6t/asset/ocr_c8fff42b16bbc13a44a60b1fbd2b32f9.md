Do not use a recursive solution if it is inefficient and you have a clear, efficient iterative solution

However, you should not use recursion just for the sake of using recursion. For example, you probably should not use the recursive factorial function in practice. You can easily write an iterative factorial function, given the iterative definition that was stated earlier in this chapter. The iterative function is almost as clear as the recursive one and is more efficient. There is no reason to incur the overhead of recursion when its use does not gain anything. Recursion is truly valuable when a problem has no simple iterative solutions.

The second point about recursion and efficiency is that some recursive algorithms are inherently inefficient. This inefficiency is a very different issue than that of overhead. It has nothing to do with how a compiler happens to implement a recursive function, but rather is related to the technique that the algorithm employs.

As an example, recall the recursive solution for the multiplying rabbits problem that you saw earlier in this chapter:

The recursive version of rabbit is inherently inefficient

rabbit(n) = { 1 if n is 1 or 2; rabbit(n - 1) + rabbit(n - 2) if n > 2 }

The diagram in Figure 2-19 illustrated the computation of rabbit(7). Earlier, you were asked to think about what the diagram would look like for rabbit(10). If you thought about this question, you may have come to the conclusion that such a diagram would fill up most of this chapter. The diagram for rabbit(100) would fill up most of this universe!

The fundamental problem with rabbit is that it computes the same values over and over again. For example, in the diagram for rabbit(7), you can see that rabbit(3) is computed five times. When n is moderately large, many of the values are recomputed literally trillions of times. This enormous number of computations makes the solution infeasible, even if each computation requires only a trivial amount of work.

However, do not conclude that the recurrence relation is of no use. One way to solve the rabbit problem is to construct an iterative solution based on this same recurrence relation. The iterative solution goes forward instead of backward and computes each value only once. You can use the following iterative function to compute rabbit(n) even for very large values of n.

You can use rabbit's recurrence relation to construct an efficient iterative solution

```
/* Iterative solution to the rabbit problem. */
int iterativeRabbit(int n)
{
    // Initialize base cases:
    int previous = 1; // Initially rabbit(1)
    int current = 1; // Initially rabbit(2)
    int next = 1; // Result when n is 1 or 2

    // Compute next rabbit values when n > 3
    for (int i = 3; i <= n; i++)
    {
        // current is rabbit(i - 1), previous is rabbit(i - 2)
        next = current + previous; // rabbit(i)
        previous = current; // Get ready for next iteration
        current = next; // Get ready for next iteration
    } // end for

    return next;
} // end iterativeRabbit
```

Convert from recursion to iteration if it is easier to discover a recursive solution but more efficient to use an iterative solution

Thus, an iterative solution can be more efficient than a recursive solution. In certain cases, however, it may be easier to discover a recursive solution than an iterative solution. Therefore, you may need to convert a recursive solution to an iterative solution. This conversion process is easier if your recursive function calls itself once, instead of several times. Be careful when deciding whether your function calls itself more than once. Although the recursive function rabbit calls itself twice, the