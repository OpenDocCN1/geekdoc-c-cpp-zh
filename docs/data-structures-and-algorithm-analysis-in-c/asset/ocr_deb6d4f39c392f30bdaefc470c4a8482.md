# 8.6.1 Slowly Growing Functions

Consider the recurrence

T(N) = \begin{cases} 0 & N \le 1 \\ T(f(N)) + 1 & N > 1 \end{cases} (8.1)

In this equation, T(N) represents the number of times, starting at N, that we must iteratively apply f(N) until we reach 1 (or less). We assume that f(N) is a nicely defined function that reduces N. Call the solution to the equation f*(N).

We have already encountered this recurrence when analyzing binary search. There, f(N) = N/2; each step halves N. We know that this can happen at most log N times until N reaches 1; hence we have f*(N) = log N (we ignore low-order terms, etc.). Observe that in this case, f*(N) is much less than f(N).

Figure 8.17 shows the solution for T(N) for various f(N). In our case, we are most interested in f(N) = log N. The solution T(N) = log* N is known as the iterated logarithm. The iterated logarithm, which represents the number of times the logarithm needs to be iteratively applied until we reach one, is a very slowly growing function. Observe that log* 2 = 1, log* 4 = 2, log* 16 = 3, log* 65536 = 4, and log* 2^65536 = 5. But keep in mind that 2^65536 is a 20,000-digit number. So while log* N is a growing function, for all intents and purposes, it is at most 5. But we can still produce even more slowly growing functions. For instance, if f(N) = log* N, then T(N) = log** N. In fact, we can add stars at will to produce functions that grow slower and slower.

# 8.6.2 An Analysis by Recursive Decomposition

We now establish a tight bound on the running time of a sequence of M = \Omega(N) union/find operations. The unions and finds may occur in any order, but unions are done by rank and finds are done with path compression.

| f(N) | f*(N) |
|---|---|
| N-1 | N-1 |
| N-2 | N/2 |
| N-c | N/c |
| N/2 | log N |
| N/c | log_c N |
| \sqrt{N} | log log N |
| log N | log* N |
| log* N | log** N |
| log** N | log*** N |

Figure 8.17 Different values of the iterated function