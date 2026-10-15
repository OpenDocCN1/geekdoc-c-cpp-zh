+   1. G is without boundaries, i.e. all involutions switch_i are without fixed points;
+   2. G is without multi-incidence, i.e.10
+   ∀d ∈ D, ∀I ⊆ N = {0, …, n}, ⟨⟩_{N\I}(d) = ⋂_{i∈I} ⟨⟩_{N\{i}}(d).

The equivalence between n-surfaces and connected n-Gmaps without boundary and without multi-incidence leads to the fact that the simplicial analog of any n-surface is an n-dimensional cellular quasi-manifold. The local property characterizing n-surfaces, namely the strict neighborhood of any cell is an (n − 1)-surface, corresponds to the fact that any i-cell of an n-Gmap is an (n − 1)-Gmap.

# 8.3 Some Consequences

# 8.3.1 Chain of Maps

Definition and basic operations

For several applications, it can be useful to handle other classes of “objects”, for instance subdivided “objects” which cells are quasi-manifolds but which are not quasi-manifolds themselves. This leads to the definition of chains of maps:

Definition 90 (chain of maps) [104] An n-dimensional chain of maps is a tuple C = ((G^i)_{i=0,…,n}, (σ^i)_{i=1,…,n}) such that (cf. Fig. 8.17(a) and (b)):

+   1. ∀i, 0 ≤ i ≤ n, G^i = (D^i, α_0^i, …, α_{i-1}^i, α_i^i = ω) is an i-dimensional generalized map such that ω is undefined on D^i;
+   2. ∀i, 1 ≤ i ≤ n, σ^i : D^i ⟶ D^{i-1};
+   for i ≥ 2, σ^i satisfies, for any dart d of D^i:
+   (a) for any j, 0 ≤ j ≤ i − 2, σ^i(α_j^i(d)) ∈ {σ^i(d), α_j^{i-1}(σ^i(d))} (in other words, σ^i is a function which associates an orbit ⟨α_0^i, …, α_{i-2}^i⟩ of G^i with (a subset of) an orbit ⟨α_0^{i-1}, …, α_{i-2}^{i-1}⟩ of G^{i-1});
+   (b) σ^{i-1} ∘ σ^i ∘ α_{i-1}^i(d) = σ^{i-1} ∘ σ^i(d).