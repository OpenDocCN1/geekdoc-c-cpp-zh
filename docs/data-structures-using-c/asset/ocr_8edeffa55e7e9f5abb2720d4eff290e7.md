If $y_1 = 1$, then $y_2, y_3, ..., y_n$ must be an optimal sequence for the problem knapsack(2, n, $M - w_1$). If it is not, then there is another 0/1 sequence $z_2, z_3, ..., z_n$ such that

```
$$\sum_{2 \le i \le n} w_i z_i \le M - w_1$$
```

and

```
$$\sum_{2 \le i \le n} P_i z_i > \sum_{2 \le i \le n} P_i y_i$$
```

Hence, $y_1, z_2, z_3, ..., z_n$ is a sequence for $\sum w_k x_k$ with a greater value.

In dynamic programming, formulating the optimal sequence for a knapsack problem can be achieved either in forward or backward approach. Let $x_1, x_2, ..., x_n$ be the variables for which a sequence of decisions has to be made. In the forward approach, the formulation of decision $x_i$ is made in terms of optimal decision sequences for $x_{i+1}, ..., x_n$. In the backward approach, the formulation for decision $x_i$ is made in terms of optimal decision sequences for $x_1, ..., x_{i-1}$. In the forward approach, we look ahead on the decision sequence $x_i, x_2, ..., x_n$, and in the backward formulation, we look backwards on the decision sequence $x_1, x_2, ..., x_n$.

For an integer $y$ such that $0 \le y \le M, f(y)$ is an ascending function.

```
$y_1 < y_2 < ... < y_k$ such that
$f(y_1) < f(y_2) < ... < f(y_k)$
$f(y) = -\infty$ for $y < y_1$
$f(y) = f(y_i)$ for $y \ge y_i$
```

We use the ordered set

```
$f(y) = S' = \{ (p, w) | 1 \le j \le k \}$
```

where $p = f(y)_j$ and $w = y_j$.

The following steps are used to solve all knapsack problems using dynamic programming forward approach:

+   1. Initially $S^0 = \{ (0, 0) \}$
+   2. $S'_i = \{ (p, w) | (p - p_j, w - w_j) \in S' \}$
+      That is, to obtain $S^{i+1}$, we either include $x_{i+1}$ or do not include $x_{i+1}$.
+      (a) If $x_{i+1} = 1$ is not included, then $S'_i = S'$. 
+      (b) If $x_{i+1} = 1$ is included, then the resulting states in $S'_i$ are obtained by adding $(p_{i+1}, w_{i+1})$ to each state in $S'$. 
+   3. $S^{i+1}$ can be computed by merging and purging the states in $S'$ and $S'_i$ together, using the dominance rule—if $S^{i+1}$ contains two pairs $(p_a, w_a)$ and $(p_b, w_b)$, where $p_a \le p_b$ and $w_a \ge w_b$, then $(p_a, w_a)$ is dominated by $(p_b, w_b)$ pair. Hence, the pair $(p_a, w_a)$ is discarded. In this way, dominated tuples get purged. We can also purge all pairs $(p, w)$ with $w > M$ because the knapsack capacity is $M$. 
+   4. Repeat steps 2 and 3 until $S^n$ is obtained.