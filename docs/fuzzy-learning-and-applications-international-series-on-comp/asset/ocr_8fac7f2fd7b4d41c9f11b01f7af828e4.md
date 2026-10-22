| Impl. Name | Implication Form | Imp. Type | Prop. |
|---|---|---|---|
| Lukasiewicz | min(1 − x + y, 1) | R with T = W
S with S = W'
QL with T = min
S = W' | I1-I13 |
| Fodor | { 1          x ≤ y
  max(1 − x, y)  x > y } | R with T = min₀
S with S = max₁
QL with T = min
S = max₁ | I1-I12 |
| Reichenbach | 1 − x + xy | S with S = Π' | I1-I7, I9, I10, I12, I13 |
| Kleene-Dienes | max(1 − x, y) | S with S = max
QL with T = W
S = W' | I1-I7, I9, I10, I12, I13 |
| Zadeh | max[1 − x, min(x, y)] | QL with T = min
S = max | I2, I3, I5, I6, I9, I13 |

Table 11.1 Selected fuzzy implications

+   - products (Π ≤ ★_T ≤ ∧) ∈ [0, 1/3],
+   - averages (∧ ≤ ★_A ≤ ∨) ∈ [1/3, 2/3],
+   - sums (∨ ≤ ★_S ≤ ⊔) ∈ [2/3, 1].

As an example, let us locate two products (algebraic product x • y = xy and bold product x ⊙ y = 0 ∨ (x + y − 1)) within the [0, 1] interval according to the pseudometric distance. For the algebraic product the calculated distance is d(Π, •) = 1/4 and for bounded product we get d(Π, ⊙) = 1/6. By analogy, we get locations for the algebraic sum x ˙+ y = x + y − xy and bounded sum x ⊕ y = 1 ∧ (x + y) which are symmetric to the corresponding products with respect to 1/2 in the [0, 1] interval. These and some additional known results are illustrated in Figure 11.1(A).

We can also order other families of operations, which can be obtained using algebraic product and bounded product (e.g., Yager operations, Schweizer and Sklar operations, Frank operations, Hamacher operations and others).