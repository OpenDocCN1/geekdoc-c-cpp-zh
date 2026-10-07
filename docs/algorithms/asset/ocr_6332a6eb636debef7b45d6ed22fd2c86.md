# 6.5 Chain matrix multiplication

concept of a subproblem to carry additional information about the items being used. We add a second parameter, $0 \le j \le n$:

$K(w, j)$ = maximum value achievable using a knapsack of capacity $w$ and items $1, \dots, j.
The answer we seek is $K(W, n)$.

How can we express a subproblem $K(w, j)$ in terms of smaller subproblems? Quite simple: either $j$ is needed to achieve the optimal value, or it isn't needed:

```
$K(w, j) = \max(K(w-w_j, j-1) + v_j, K(w, j-1)).
```

(The first case is invoked only if $w_j \le w$. In other words, we can express $K(w, j)$ in terms of subproblems $K(\cdot, j-1)$.\nThe algorithm then consists of filling a two-dimensional table, with $W+1$ rows and $n+1$ columns. Each table entry takes constant time, so even though the table is much larger than in the previous case, the running time remains the same, $O(nW)$. Here's the code.

```
Initialize $K(0, j) = 0$ and all $K(w, 0) = 0$\nfor $j = 1$ to $n:\n  for $w = 1$ to $W:\nn    if $w_j \le w$: $K(w, j) = K(w, j-1)$\n    else: $K(w, j) = \max(K(w-w_j, j-1), K(w, j-1) + v_j)$\nreturn $K(W, n)$
```

# 6.5 Chain matrix multiplication

Suppose that we want to multiply four matrices, $A \times B \times C \times D$, of dimensions $50 \times 20$, $20 \times 1$, $1 \times 10$, and $10 \times 100$, respectively (Figure 6.6). This will involve iteratively multiplying two at a time. Matrix multiplication is not

Figure 6.6 $A \times B \times C \times D = (A \times (B \times C)) \times D$.

![](bbox=[0.04, 0.64, 0.7, 0.88])