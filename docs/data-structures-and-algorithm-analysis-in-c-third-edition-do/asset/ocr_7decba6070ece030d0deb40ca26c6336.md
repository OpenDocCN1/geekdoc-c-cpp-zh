504

Chap. 15 Lower Bounds

To minimize the effects of worst-case behavior, the algorithm's best strategy is to maximize the minimum improvement in strength by balancing the strengths of any two competitors. From the algorithm's point of view, the best outcome is that an element increases in strength. This happens whenever $a = b$, where $a$ and $b$ are the strengths of the two elements being compared. All strengths begin at zero, so the winner must make at least $k$ comparisons when $2^{k-1} < n \le k$. Thus, there must be at least $n + [log n] - 2$ comparisons. Our algorithm is optimal.

# 15.5 State Lower Bounds Proof

We now consider the problem of finding both the minimum and the maximum from an (unsorted) list of values. This might be useful if we want to know the range of a collection of values to be plotted, for the purpose of drawing the plot's scales. We could find them independently in $2n - 2$ comparisons. A slight modification is to find the minimum in $n - 1$ comparisons, remove it from the list, and then find the minimum in $n - 2$ further comparisons for a total of $2n - 3$ comparisons. Can we do better than this?

Before continuing, think a moment about how this problem of finding the minimum and the maximum compares to the process of the last, that of finding the second best value (and by implication, the maximum). Which of these two problems do you think is harder? It is probably not all obvious to you that one is harder or easier than the other. There is intuition that argues for either case. One intuition might argue that the process of finding the minimum should tell you something about the second best value, more than any comparison tells you which of two can be a candidate for maximum value, and which can be a candidate for minimum value, making progress in both directions.

We will start by considering a simple divide-and-conquer approach to finding the minimum and maximum. Split the list into two parts and find the minimum and maximum elements in each part. Then compare each with other with two comparisons to get the final result. The algorithm is shown in Figure 15.3.

The cost of this algorithm can be modeled by the following recurrence.

```
T(n) = \begin{cases} n & n = 1 \ n & n = 2 \ T(\lfloor n/2\rfloor) + T(\lceil n/2\rceil) + 2 & n > 2 \end{cases}
```

This is a rather interesting recurrence, and its solution ranges between $3n/2-2$ (when $n = 2^k$ or $n = 2^k \pm 1$) and $5n/3-2$ (when $n = 3 	imes 2$). We can infer from this behavior how we divide the list affects the performance of the algorithm.