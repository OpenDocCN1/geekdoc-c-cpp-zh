[p = {w1, ..., wn}] Similar to the previous case.

# Lemma 9 (Closed Expression). fv(e) = ∅ and e → e' implies fv(e') = ∅

Proof. By induction on the structure of e.

Lemmata 5-9 allow us to prove Closed Term Proposition (Proposition 1). By this proposition, we can say that a closed term t remains closed, even after t transitions to some new term t', producing an action α. Lemma 9 is analogous; it states that expressions remain closed after reductions.

# Proposition 1 (Closed Term). If fv(t) = ∅ and t →α t', then fv(t') = ∅

Proof. By induction on the structure of t.

[t = e] Holds immediately by the rule [rExpression] and the lost Expression] Lemma.

[t = (x = t1 ; t2)] Given that current structure of t, we can derive t →α t' using two cases:

+   1. [rLET1] From the rule, t' = (x = t1' ; t2) and

```
t1 →α t1' (B.2a)
```

From the premise, fv(t) = ∅, so by the fv definition. fv(t1) ∪ (fv(t2) \ {x}) = ∅, or equivalently

```
fv(t1) = ∅ (B.2b)
```

```
fv(t2) \ {x} = ∅ (B.2c)
```

If we apply the inductive hypothesis to eqs. (B.2a) and (B.2b), we get

```
fv(t1') = ∅ (B.2d)
```

So, by eqs. (B.2c) and (B.2d) and the definition of fv, we get fv(x = t1' ; t2) = ∅ as required.

+   2. [rLET2] From the rule, t = (x = v ; t2) and t' = t2 [v/x]. Since fv(t) = ∅, by the Free Variables Definition, fv(v) ∪ (fv(t2) \ {x}) = ∅, or equivalently

```
fv(v) = ∅ (B.2e)
```

```
fv(t2) \ {x} = ∅ (B.2f)
```

We need to show that fv(t') = ∅, or fv(t2 [v/x]) = ∅, so we consider two sub-cases:

+   a. If x ∉ fv(t2), then by Corollary 6, t2 = t2 [v/x]. Substituting this in eq. (B.2f), results in fv(t2 [v/x]) = ∅, as required.

+   b. If x ∈ fv(t2), then by Lemma 7, we get fv(t2 [v/x]) = fv(t2) \ {x}. If we substitute this in eq. (B.2f), the case holds.

[t = send(w, (t1.e1, ..., tn.en))] Given that current structure of t, we can derive t →α t' using two cases:

+   1. [rCHOICE1] From this rule, we know that α = τ and

```
t' = send(w, {1 ↓ v1, ..., vk-1, ek', ..., en})
```

```
ek → ek' (B.3a)
```

Since fv(t) = ∅, then by the fv definition

```
fv(t) = ∅ (B.3b)
```

```
fv(v_i) = ∅ for i ∈ 1..k-1 (B.3c)
```

```
fv(e_i) = ∅ for i ∈ k..n (B.3d)
```

Applying the Closed Expression Lemma to eqs. (B.3a) and (B.3d), results in fv(ek) = ∅. Using this information along with eqs. (B.3b-d) and the fv definition, results in fv(t') = ∅ as required.