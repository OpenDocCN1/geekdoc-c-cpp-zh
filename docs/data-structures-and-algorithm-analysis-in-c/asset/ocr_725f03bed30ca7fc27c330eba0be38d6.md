Occasionally, the best-case performance of an algorithm is analyzed. However, this is often of little interest, because it does not represent typical behavior. Average-case performance often reflects typical behavior, while worst-case performance represents a guarantee for performance on any possible input. Notice also that, although in this chapter we analyze C++ code, these bounds are really bounds for the algorithms rather than programs. Programs are an implementation of the algorithm in a particular programming language, and almost always the details of the programming language do not affect a Big-Oh answer. If a program is running much more slowly than the algorithm analysis suggests, there may be an implementation inefficiency. This can occur in C++ when arrays are inadvertently copied in their entirety, instead of passed with references. Another extremely subtle example of this is in the last two paragraphs of Section 12.6. Thus in future chapters, we will analyze the algorithms rather than the programs.

Generally, the quantity required is the worst-case time, unless otherwise specified. One reason for this is that it provides a bound for all input, including particularly bad input, which an average-case analysis does not provide. The other reason is that average-case bounds are usually much more difficult to compute. In some instances, the definition of “average” can affect the result. (For instance, what is average input for the following problem?)

As an example, in the next section, we shall consider the following problem:

# Maximum Subsequence Sum Problem

Given (possibly negative) integers A1, A2, ..., AN, find the maximum value of \sum_{i=k}^{j} A_k. (For convenience, the maximum subsequence sum is 0 if all the integers are negative.) Example: For input -2, 11, -4, 13, -5, -2, the answer is 20 (A2 through A4).

This problem is interesting mainly because there are so many algorithms to solve it, and the performance of these algorithms varies drastically. We will discuss four algorithms to solve this problem. The running time on some computers (the exact computer is unimportant) for these algorithms is given in Figure 2.2.

There are several important things worth noting in this table. For a small amount of input, the algorithms all run in the blink of an eye. So only if a small amount of input is

| Input Size | 1 O(N^3) | 2 O(N^2) | 3 O(N log N) | 4 O(N) |
|---|---|---|---|---|
| N = 100 | 0.000159 | 0.000006 | 0.000005 | 0.000002 |
| N = 1,000 | 0.095857 | 0.000371 | 0.000060 | 0.000022 |
| N = 10,000 | 86.67 | 0.033322 | 0.000619 | 0.000222 |
| N = 100,000 | NA | 3.33 | 0.006700 | 0.002205 |
| N = 1,000,000 | NA | NA | 0.074870 | 0.022711 |

Figure 2.2 Running times of several algorithms for maximum subsequence sum (in seconds)