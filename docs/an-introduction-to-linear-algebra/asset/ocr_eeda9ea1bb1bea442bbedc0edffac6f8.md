u ∈ U ∩ W, and hence can be written as u = d₁v¹ + ⋯ + dᵣvʳ, where dᵢ are scalars. Thus, from (9.3) it follows that

$$d_1v^1+\cdots+d_rv^r+c_1w^1+\cdots+c_{n-r}w^{n-r}=0.$$

But since S₃ is a basis of W, the above relation implies that c₁ = ⋯ = cₙ₋ᵣ = 0. Substituting this in (9.1), we get

$$a_1v^1+\cdots+a_rv^r+b_1u^1+\cdots+b_{m-r}u^{m-r}=0.$$

Finally, since S₂ is a basis of U, the above relation implies that a₁ = ⋯ = aᵣ = b₁ = ⋯ = bₘ₋ᵣ = 0.

The vector space V is said to be a direct sum of its subspaces U and W, denoted as U ⊕ W, if for every v ∈ V there exist unique vectors u ∈ U and w ∈ W such that v = u + w.

**Example 9.5.** Consider V = ℝ³, U = {(a₁, a₂, 0)ᵗ : a₁, a₂ ∈ ℝ}, W = {(0, a₂, a₃)ᵗ : a₂, a₃ ∈ ℝ}. Then, ℝ³ = U + W but ℝ³ ≠ U ⊕ W, since sums are not necessarily unique, e.g., (1, 3, 1)ᵗ = (1, 1, 0)ᵗ + (0, 2, 1)ᵗ = (1, 2, 0)ᵗ + (0, 1, 1)ᵗ. However, if we let U = {(a₁, a₂, 0)ᵗ : a₁, a₂ ∈ ℝ}, W = {(0, 0, a₃)ᵗ : a₃ ∈ ℝ}, then ℝ³ = U ⊕ W.

# **Theorem 9.6.**

The vector space V is the direct sum of its subspaces U and W, i.e., V = U ⊕ W, if and only if V = U + W, and U ∩ W = {0}.

# **Proof.**

Suppose V = U ⊕ W. Then any v ∈ V can be uniquely written in the form v = u + w, where u ∈ U and w ∈ W. This in particular implies that V = U + W. Now let v ∈ U ∩ W, then v = v + 0 where v ∈ U, 0 ∈ W; also, v = 0 + v where 0 ∈ U, v ∈ W. But this in view of the uniqueness implies that v = 0 + 0 = 0 and U ∩ W = {0}.

Conversely, suppose that V = U + W and U ∩ W = {0}. If v ∈ V, then there exist u ∈ U and w ∈ W such that v = u + w. We need to show that this sum is unique. For this, let v = u′ + w′ where u′ ∈ U and w′ ∈ W is also such a sum. Then, u + w = u′ + w′, and hence u − u′ = w − w′. But u − u′ ∈ U and w − w′ ∈ W; therefore in view of U ∩ W = {0} it follows that u − u′ = 0 and w − w′ = 0, i.e., u = u′ and w = w′.

# **Corollary 9.4.**

Let U and W be subspaces of a vector space V. Then, dim U ⊕ W = dim U + dim W.

# Problems

+   1. **9.1.** Find the dimension of the following spaces spanned by all
+      (i) m × n matrices, and give a basis for this space