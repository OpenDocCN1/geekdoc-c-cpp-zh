# Theorem 7.1

+   • **Property:** The set of the times when state $i$ has a non-null probability of being visited is closed under addition in a DTMCS.

⊢ ∀ X p s P₀ P₁ⱼ i.
Aperiodic_DTMC X p s p₀ P₁ⱼ ∧ i ∈ space s ⇒
∀ a b. a ∈ Period_Set X p s i ∧ b ∈ Period_Set X p s i ⇒
(a + b) ∈ Period_Set X p s i

# Theorem 7.2

+   • **Property:** The transition probability $p^{j(n)}$ is greater than zero, for all states $i$ and $j$ in its state space. For any state $i$ in the finite state space $S$ of an aperiodic DTMC, there exists an $N < \infty$ such that $0 < p_{i,j}^{(n)}$, for all $n \ge N$ and all $i$ in the state space.

⊢ ∀ X p s P₀ P₁ⱼ i t.
Aperiodic_DTMC X p s p₀ P₁ⱼ ∧ i ∈ space s ⇒
∃ N. ∀ n. N ≤ n ⇒ 0 < Trans X p s t n i i

In this theorem, $N$ is of HOL4 datatype num that represents positive integers. formal reasoning about the correctness of the above theorems involves Theorem 7.1, some DTMC properties and the following three lemma, along with some arithmetic reasoning and set theoretic reasoning.

# Lemma 7.1

+   • **Positive Element in a Closed Set:** If an integer set $S$ contains at least one nonzero element and $S$ is closed under addition and subtraction, then $S = \{ kc; k \in Z \}$, where $c$ is the least positive element of $S$.

⊢ ∀ s:int → bool. s ≠ ∅ ∧
(∀ a b. a ∈ s ∧ b ∈ s ⇒ (a + b) ∈ s ∧ (a - b) ∈ s) ⇒
0 < MINSET { r | 0 < r ∧ r ∈ s } ∧
(s = { r | ∃k. r = k * MINSET { r | 0 < r ∧ r ∈ s } })

where MINSET A refers to the minimum element in the set A.