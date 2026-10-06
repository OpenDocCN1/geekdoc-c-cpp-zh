224 ■ Limits of Computation

+   14. Consider 3-DISTINCT-CNF-SAT.

Instance: A Boolean expression in conjunctive normal form with three distinct literals per clause.

Question: Does there exist an assignment of truth values that makes the expression true?

+   a. Give yes and no instances of 3-DISTINCT-CNF-SAT.

+   b. Prove 3-DISTINCT-CNF-SAT is NP-complete.

+   15. Find a polynomial reduction from Bipartite-Graph to 2-Graph-Color.

Definitions to Use:

Bipartite Graph: The vertices of graph G = (V, E) can be separated into two subsets V₁ and V₂ so that every edge joins a vertex in V₁ to a vertex in V₂.

Two-Graph Color: The vertices of G = (V, E) can be colored with two colors so that no two vertices connected by an edge are assigned the same color.

+   16.

+   a. Map the instance (x₁ ∨ x₁ ∨ x₁) ∧ (¬x₁ ∨ ¬x₁ ∨ ¬x₁) of 3-CNF-SAT to an instance of VERTEX COVER. Show that it is a no instance of VERTEX COVER.

+   b. Map the no instance (x₁ ∨ x₁ ∨ x₁) ∧ (¬x₁ ∨ ¬x₁ ∨ ¬x₁) of 3-CNF-SAT to an instance of Subset Sum. Show that it is a no instance of Subset Sum.

+   17. Finish the proofs in the text.

+   a. Prove that the transformation given from VC to HC is polynomial.

+   b. Prove that in the transformation given, VC to HC, yes goes to yes (or no comes from no).

+   c. Prove that 3DM is in the class NP.

+   18. Prove X3C (exact cover by 3 sets, p. 209) is NP-complete.