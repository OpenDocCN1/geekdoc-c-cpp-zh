{x_n} has a convergent subsequence {x_{n_k}} in \overline{K}. Suppose {x_{n_k}} → w_o, w_o ∈ \overline{K} / K. Then d(x_o, w_o) = lim d(x_o, x_{n_k}) = d(x_o, \overline{K}). Since K is uniquely remotal, there exists k_{x_o} ∈ K such that d(x_o, k_{x_o}) = δ(x_o, K), so we have d(x_o, k_{x_o}) = δ(x_o, K) = δ(x_o, \overline{K}) = d(x_o, w_o) which contradicts the fact that K is uniquely remotal. Hence K is M-compact.

# Theorem 21.9 Let (X, d, W) be a convex metric space. If K ⊆ X is a uniquely remotal and M-compact set and FarK ⊆ K' then K is a singleton.

Proof. As FarK ⊆ K', there exists k_o ∈ FarK / K'. As K is uniquely remotal, there exists x ∈ X such that d(x, k_o) = sup{d(x, k) : k ∈ K}. Consider the set C = {0 ≤ t ≤ 1, k_o is farthest point for y' = W(x, k_o, t) such that d(y', x) = t d(x, k_o) and d(y', k_o) = (1−t)d(x, k_o)}. Clearly C ≠ ∅ as 1 ∈ C. We claim that inf C > 0, otherwise k_o is farthest point of itself which implies that K is a singleton. Suppose inf C = t_o > 0. Consider x_o ∈ W(x, k_o, t_o) such that d(x_o, x) = t_o d(x, k_o)). We claim that there exist ε_o > 0 such that d(x_o, k) < d(x_o, k_o) − ε_o for every k ∈ K / {k_o}. If not, then there exists {k_n} ⊆ K / {k_o} such that d(x_o, k_n) → d(x_o, k_o) = δ(x_o, K). So {k_n} is maximizing sequence for x_o. Since K is M-compact, there exists {k_{n_q}} ⊆ {k_n} such that k_{n_q} → k' Since k_o is not a limit point of K, k' ≠ k_o. This contradicts the fact that K is uniquely remotal. Now, take y'' = W(k_o, x_o, t), 0 < t < 1. For k ∈ K / {k_o}, consider

```
d(y'', k) = d(W(x_o, k_o, t), k)
≤ (1−t)d(k_o, k) + t d(x_o, k)
< (1−t)diam K + t(d(x_o, k_o) − ε_o)
= t d(x_o, k_o) − ε_o t + (1−t)diam K
= t d(x_o, k_o) − [ε_o t − (1−t)diam K]
= d(W(k_o, x_o, t), k_o) − [ε_o t − (1−t)diam K].
```

Now consider the mapping f : R → R defined as f(t) = ε_o t − (1−t)diam K. Clearly f is continuous and f(1) = ε_o > 0 and so there exists a δ > 0 such that f(t) > 0 for all t ∈ (1−δ, 1+δ). Therefore there exists at least one t' ∈ (1−δ, 1) such that f(t') > 0 i.e. ε_o t' − (1−t')diam K > 0, so d(W(k_o, x_o, t'), k) < d(W(k_o, x_o, t'), k_o) for all k ∈ K / {k_o}. Therefore, k_o is a farthest point for W(k_o, x_o, t') in K which contradicts the fact that inf C = t_o > 0. So inf C = 0. i.e. k_o is farthest point of itself. Hence K is a singleton.

# Theorem 21.10 Let (X, d, W) be a convex metric space. If K ⊆ X is uniquely remotal and M-compact, then K' is either empty or M-compact and uniquely remotal.

Proof. If FarK ⊆ K' then K is a singleton by Theorem 21.5. Suppose FarK ⊆ K'. We claim that δ(x, K) = δ(x, K'). First we show that δ(x, K) ≥ δ(x, K') for all x ∈ X. For x ∈ X, there exists {k'_n} ⊆ K' such that d(x, k'_n) → δ(x, K') as n → ∞. As k'_n ∈ K', for each n ∈ ℕ there exists k_n ∈ K such that d(k_n, k'_n) < 1/n. Now d(x, k'_n) ≤ d(x, k_n) + d(k_n, k'_n), implies d(x, k_n) ≥ d(x, k'_n) − d(k_n, k'_n) > d(x, k'_n) − 1/n. So lim d(x, k_n) ≥ δ(x, K') and therefore δ(x, K) ≥ lim d(x, k_n) ≥ δ(x, K') for all x ∈ X.

We next show that δ(x, K') ≥ δ(x, K) for all x ∈ X. Since K is uniquely remotal, there exists k_x ∈ K such that d(x, k_x) = δ(x, K). Then k_x ∈ K', since FarK ⊆ K'. So δ(x, K') ≥ d(x, k_x) = δ(x, K). Hence δ(x, K') = δ(x, K).