From ( min p : 0 ≤ p ≤ 0 ∧ A.p.0 : p ) = 0, we infer that s should be initialized at zero and we obtain a program of the following form:

```
```
1: N ≥ 0 ∧ (∀n : 0 ≤ n ≤ N : A.n.n)
2: u ← 0
3: r ← 0
4: s ← 0
5: Invariant : P₀ ∧ P₁ ∧ Q
6: bound : N - n
7: while n ≠ N do
8:     establish Q(n ← n + 1)
9:     r ← r max (n + 1 - s)
10:    n ← n + 1
11: end while    ▷ r = ( max p,q : 0 ≤ p ≤ q ≤ N ∧ A.p.q : q - p)
```
```

This program leaves “establish Q(n ← n + 1)” as a subproblem. Since A holds for empty segments, the range of the quantification in Q is non-empty and Q can be written as the conjunction of Q₀, Q₁, and Q₂, defined as

+   - Q₀ : 0 ≤ s ≤ n
+   - Q₁ : A.s.n
+   - Q₂ : (∀p : 0 ≤ p < s : ¬A.p.n)

Since A is prefix-closed, we have ¬A.p.n ⇒ ¬A.p.(n+1) for 0 ≤ p < n, and, hence

Q₂ ⇒ Q₂(n ← n + 1)

We have Q₀ ⇒ Q₀(n ← n + 1) as well and we conclude

Q₀ ∧ Q₂ ∧ A.s.(n + 1) ⇒ Q(n ← n + 1)

The fact that Q₂(n ← n + 1) is implied by Q₂ has another consequence. From

Q₂(n ← n + 1) ≡ (∀p : 0 ≤ p < s : ¬A.p.(n + 1))

we infer

Q₂ ⇒ ( min p : 0 ≤ p ≤ n + 1 ∧ A.p.(n + 1) : p ) ≥ s

i.e., only values p for which s ≤ p ≤ n + 1 have to be investigated. For p = n + 1, we know that A.p.(n + 1) holds, so we usually start our investigations with the calculation of A.p.(n + 1) for s ≤ p ≤ n.

We return to all zeros, for which A.p.q ≡ (∀i : p ≤ i < q : X.i = 0), and we compute A.p.(n + 1) for s ≤ p ≤ n :