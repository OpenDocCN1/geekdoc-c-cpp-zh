# Theorem 6.4

```
|- ∀ X p s p₁ Pᵢⱼ t L.
rmc X p s p₁ Pᵢⱼ ==>
(prob p ( ⋂_{k=0}^{|L|-1} { Xt+k = EL k L } ) = prob p (
⋂_{k=0}^{|L|-1} { Xt+k = EL k (REVERSE L ) }))
```

The backward proof of this theorem involves rewriting the goal by using Definition 6.7 and Theorem 6.1, which generates the following subgoal:

```
PROD (0, | L |)
( λ k. P ( ( t + k + 1) x = EL ( k + 1) (REVERSE L ) ) |
( x | X (t + k) x = EL k (REVERSE L ) )) =
PROD (0, | L |)
( λ k. prob p ({ x | X (t + k + 1) x = EL ( | L | - k - 1) L } |
{ x | X (t + k) x = EL ( | L | - k) L })))
```

Now, the proof can be completed by applying the following lemma:

```
|- ∀ f n. PROD (0, n) (λ k. f k) = PROD (0, n) (λ k. f (n - k - 1))
```

which corresponds to the mathematical expression:

```
∏_{k=0}^n f(k) = ∏_{k=0}^n f(n-k-1) (6.6)
```

# 6.3 FORMALIZATION OF STATIONARY DISTRIBUTIONS

It is often the case that we are interested in the probability of some specific states as time tends to infinity under certain conditions. This is the main reason why stationary behaviors of stochastic processes are frequently analyzed in engineering and scientific domains.

Let {X_t}_{t>=0} be a Markov chain having state space and transition probabilities/ p_ij ... if (i, j) ∈ Ω, are nonnegative numbers summing to one, then π(j) = Σ_{i∈Ω} π(i) pij is called a stationary distribution. The corresponding HOL4 definition is as follows: