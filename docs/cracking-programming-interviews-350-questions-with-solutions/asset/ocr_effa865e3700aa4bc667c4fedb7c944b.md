$d4_i$ = the fourth largest departure time among those of customers $j : 0 ≤ j < i$,
and similarly, for reasons that become apparent soon, $d3_i, d2_i, d1_i$ for the third, second and first largest departure time among those of the earlier customers.

In terms of these numbers we then grasp $s_i$ by :

$$4 ≤ i < n : s_i = max(a[i], d4_i)
0 ≤ i < 4 : s_i = max(a[i], t_0)$$

in obedience to the rule that desk officers are never idle when a customer is waiting for service.

Herewith we have an effective way of computing the $s$-sequence, provided we have an effective way to compute $d4$-sequence.

The $d4$-sequence is computed very effectively if we realize that, in terms of $s_i$, customer $i$'s departure time is conveniently expressed as $s_i + b[i]$. Since $b[i] > 0$, we have $s_i + b[i] > d4_i$ on account of $4 ≤ i < n : s_i = max(a[i], d4_i)$, so that it is not difficult to see that

$$4 ≤ i < n - 1 : d4_{i+1} = min(s_i + b[i], d3_i, d2_i, d1_i)$$

or, to accommodate the other three sequences as well, the more general

$$4 ≤ i < n - 1 : (d4_{i+1}, d3_{i+1}, d2_{i+1}, d1_{i+1}) = nondecreasing
arrangement of (s_i + b[i], d3_i, d2_i, d1_i).$$

Let the invariant be $r =$ the length of the superposition of the intervals $(a[i], s_i), 0 ≤ i < j$
and $0 ≤ j ≤ n$.

and investigate an increase of $j$ by 1.

We have to examine which part of the interval $(a[j], s_j)$ is not covered by any of the intervals $(a[i], s_i) : 0 ≤ i < j$.

We infer that for $a[j] ≥ s_{j-1}$ the interval $(a[j], s_j)$ is disjoint with the other ones. For $a[j] < s_{j-1}$, we conclude that above and the monotonicity of the $a$-sequence that the part $(a[j], s_{j-1})$ is contained in $(a[j - 1], s_{j-1})$ and that the part $(s_{j-1}, s_j)$ is disjoint with all intervals $(a[i], s_i) : 0 ≤ i < j$.

Hence, the part $(max(a[j], s_{j-1}), s_j)$ is not covered by any of the other intervals, and we conclude:

$$r = the length of the superposition of the intervals (a[i], s_i) : 0 ≤ i < j
and 0 ≤ j ≤ n and 1 ≤ j < n ⟹
r ← r + s_j - max(a[j], s_{j-1}); n ← n + 1$$

Or, if we are willing to define: $s_{-1} ≤ a[0]$,

$$r = the length of the superposition of the intervals (a[i], s_i) : 0 ≤ i < j
and 0 ≤ j ≤ n and 0 ≤ j < n ⟹ r ← r + s_j - max(a[j], s_{j-1}); n ←$$