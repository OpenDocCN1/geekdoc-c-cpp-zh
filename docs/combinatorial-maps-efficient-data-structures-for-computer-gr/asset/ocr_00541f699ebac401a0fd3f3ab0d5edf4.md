![](bbox=[0.12, 0.12, 0.88, 0.38])

# FIGURE 5.3

(a) 3-map M. For example, β₁(1) = 2, β₁(2) = 3, β₁(3) = 4 and β₁(4) = 1.

(b) The inverse 3-map M⁻¹. For example, β₁(1) = 4, β₁(4) = 3, β₁(3) = 2 and β₁(2) = 1.

+   - *cells cᵢ(d) and cⱼ(d′) are incident iff cᵢ(d) ∩ cⱼ(d′) ≠ ∅;*
+   - *cells cᵢ(d) and cᵢ(d′) are adjacent iff two darts d₁ and d₂ exist, such that d₁ ∈ cᵢ(d), d₂ ∈ cᵢ(d′), and:*
+     - *if i = 0: d₁ = βₖ(d₂) with k ∈ {0,…,n};*
+     - *if i > 0: d₁ = βᵢ(d₂) or d₂ = βᵢ(d₁).*

Note that there are two different cases for the adjacency definition: a first one for 0-cells and a second one for i-cells when i > 0. Two vertices are incident if two darts exist in the two vertices which are linked by any βₖ. For i > 0, the two darts must be linked by βᵢ. Note that the second condition of the adjacency definition (d₂ = βᵢ(d₁)) is required for i = 1, but not if i is greater than 1, because in this case βᵢ is an involution. Note also that, according to this definition, a cell is never incident to itself, since i must be different from j; but it can be adjacent to itself: for instance a loop is adjacent to itself, and more generally cells which are multi-incident to other cells: cf. Section 5.3.

An n-map M describes an nD oriented quasi-manifold. The inverse of M describes the same quasi-manifold, but with the reverse orientation (cf. Def. 34 and example in Fig. 5.3).

# Definition 34 (inverse) Let M = (D, β₁, …, βₙ) be an n-map. The n-map inverse of M is M⁻¹ = (D, β₁⁻¹, β₂, …, βₙ).

It can be tested if two n-maps describe the same subdivision, through the isomorphism notion. Two n-maps are isomorphic if there is a one-to-one mapping between their darts which preserves all relations (cf. Def. 35).