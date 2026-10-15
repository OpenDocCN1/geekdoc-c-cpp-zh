+   5. α''_n(φ^n(d, d')) = φ^{n-1}(d, d');
+   6. α''_{n+1}(φ^n(d, d')) = φ^n(d, α'_1(d')).

+   • ∀j ∈ {1, …, n−1}, ∀d ∈ D, ∀d' ∈ D':

+   7. ∀i ∈ {0, …, j−1}, α''_i(φ^j(d, d')) = φ^j(α_i(d), d');
+   8. α''_j(φ^j(d, d')) = φ^{j-1}(d, d');
+   9. α''_{j+1}(φ^j(d, d')) = φ^{j+1}(d, d');
+   10. ∀i ∈ {j+2, …, n+1}, α''_i(φ^j(d, d')) = φ^j(α_{i-1}(d), d').

The extrusion operation is implemented by Algorithm 65. Contrary to the previous operations, the n-Gmap gm is not modified. A new (n + 1)-Gmap is built, which is the result of the extrusion of gm along the path defined by gm'. Indeed, it is not possible to modify gm, since the dimension of the resulting Gmap is n + 1. The algorithm follows directly the definition. First, the darts of gm' are created, and the bijections φ' are stored in n+1 associative arrays. Second, all pairs of darts (d, d') are processed, in order to define all α involutions.

Note that contrary to the chamfering algorithm, no side effects can occur, since the given n-Gmap is not modified.

The complexity of Algorithm 65 is linear in the number of darts #d1 of the n-Gmap gm times the number of darts #d2 of the 1-Gmap gm' times log(#d1 + #d2).

Note that several operations can be deduced from the extrusion operation. For instance, let G be a connected n-Gmap and Q be the associated quasi-manifold. The cone operation, applied to G, creates a (n + 1)-Gmap, denoted G_cone, such that its associated quasi-manifold is the cone of Q (cf. Section 8.1).

# Definition 74 (cone) Let G = (D, α0, …, αn) be an n-Gmap. The (n + 1)-Gmap resulting from the cone of G is G_cone = (D'', α''0, …, α''_{n+1}), defined by:

+   • ∀j ∈ {0, …, n}, let D^j be a set of new darts, such that a bijection φ^j maps D onto D^j; let D' be a set of new darts, such that a bijection φ' maps D onto D';
+   • D'' = D' ∪_{j=0}^n D^j;
+   • ∀d ∈ D:

+   1. α''0(φ^0(d)) = φ'(d);
+   2. α''1(φ^0(d)) = φ^1(d);
+   3. ∀i ∈ {2, …, n + 1}, α''i(φ^0(d)) = φ^0(α_{i-1}(d));
+   4. ∀i ∈ {0, …, n − 1}, α''i(φ^n(d)) = φ^n(α_i(d));