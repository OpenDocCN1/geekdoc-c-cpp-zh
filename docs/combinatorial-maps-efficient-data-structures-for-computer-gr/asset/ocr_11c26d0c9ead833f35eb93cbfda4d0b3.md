than i + 1 vertices. Moreover, distinct i-simplices can be incident to the same vertices; they can even share the same boundary.

Functions can be defined on semi-simplicial sets.

# Definition 83 (semi-simplicial set morphism) Let S = (K, (d_j)_{j=0,...,n}) and S' = (K', (d'_j)_{j=0,...,n}) be semi-simplicial sets. A morphism f : S → S' is a map from the simplices of K to the simplices of K' which satisfy:

+   - ∀i, 0 ≤ i ≤ n, f : K_i → K'_i;
+   - ∀i, 0 < i ≤ n, ∀σ ∈ K_i, ∀j, 0 ≤ j ≤ i, f(d_j(σ)) = d'_j(f(σ)).

If f is bijective, f is called an isomorphism, and S and S' are said to be isomorphic.

A semi-simplicial set morphism exists between the two semi-simplicial sets depicted on Fig. 8.4(a) and (b), which associates any simplex Z with simplex Z', except E which is associated with C'.

# CW-complexes

This paragraph is based on [180].

Let B̄ⁿ (resp. Bⁿ) denotes an n-dimensional closed (resp. open) ball. In this paragraph, an n-dimensional open cell denotes a space which is homeomorphic to Bⁿ.

# Definition 84 (CW-complex) A CW-complex is a space X and a collection of disjoint open cells {e_α} whose union is X, such that:

+   1. X is Hausdorff⁵;
+   2. for each open n-cell e_α of the collection, there exists a continuous map f_α : B̄ⁿ → X that maps Bⁿ homeomorphically onto e_α and carries ∂B̄ⁿ, i.e. the boundary of B̄ⁿ, onto a finite union of open cells, each dimension less than n;
+   3. a set A is closed in X if A ∩ ē_α is closed in ē_α for each α, where ē_α denotes the closure of e_α.

Schematically, a CW-complex is a set of balls “glued” together by continuous attaching functions.

# Geometric realization

CW-complexes exist, which cannot be directly associated with semi-simplicial sets; more generally, and as said above, CW-complexes exist, which are even not triangulable.