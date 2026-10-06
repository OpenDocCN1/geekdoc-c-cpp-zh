# More NP-Complete Problems ■ 223

by adding a new variable z to each clause. Prove or disprove: This shows SAT �p TRUE-SAT.

+   8. Consider the following decision problem.

Instance: A polynomial p(x₁, ..., xₙ) of degree k in n variables having integer coefficients.
Question: Do there exist integers a₁, ..., aₙ such that p(a₁, ..., aₙ) = 0?

+   a. Why does the following argument not prove that this problem is in NP?

Guess values for a₁

+   b. This problem is undecidable. What does that say about being NP-complete?

+   9. Prove that the version of satisfiability in which every variable xᵢ and -xᵢ appears in no more than two clauses is NP-complete. (Hint: Reduction from standard CNF-SAT).

+   10. Prove that the k-link path problem is NP-complete.

Instance: Graph G = (V, E), integer k > 0, vertices v and w.
Question: Does G have a simple path from v to w with exactly k edges?

+   11. Prove that HALF_CLIQUE is NP-complete.

Instance: Graph G = (V, E), |V| is even.
Question: Does G contain a complete subgraph of size |V|/2?

+   12. Prove that Dir-HC (Hamiltonian circuit in a directed graph) is NP-complete.

+   13. Prove that ¬3_SAT is NP-complete.

Instance: A Boolean expression in CNF with three literals per clause.
Question: Does there exist an assignment of truth values that makes the expression true, but in which no clause contains three literals that are all true? (Each clause contains two literals with opposite truth values.)