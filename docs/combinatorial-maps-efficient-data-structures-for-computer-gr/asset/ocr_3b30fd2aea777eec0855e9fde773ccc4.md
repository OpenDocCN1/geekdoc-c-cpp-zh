![](bbox=[0.22, 0.1, 0.78, 0.4])

# FIGURE 8.2

(a) A simplicial complex.

(b) A simplicial complex, image of the simplicial complex of (a) by the simplicial map which associates P1 and P1', P2 and P2', P3 and P3', P4 and P4', P5 and P5' and P6 and P6'.

Simplicial maps induce continuous maps on the underlying spaces. Let f : K → L be a simplicial map. Define |f| : |K| → |L| as follows: if x ∈ |K|, then x belongs to the interior of a unique simplex P0 P1 … Pi of K; let x = Σj=0^i λj Pj, where λj are the barycentric coordinates of x, and define |f|(x) = Σj=0^i λj f(Pj). |f| is continuous; if it is a homeomorphism, it is called a linear homeomorphism. Note that |f| is a linear homeomorphism if and only if f is an isomorphism.

# Geometric realization

Every simplicial complex K determines an abstract simplicial complex A(K) = {{P0, P1, …, Pi} | P0 P1 … Pi is an i-simplex of K}.

Conversely:

# Definition 81 (geometric realization of an abstract simplicial complex)

Let K be an abstract simplicial complex. A geometric realization of K is a pair (φ, GR(K)), where GR(K) is a simplicial complex and φ is a bijection between the vertices of K and the vertices of GR(K), such that {v0, v1, …, vi} is an i-simplex of K if and only if φ(v0) φ(v1) … φ(vi) is an i-simplex of GR(K).

Every abstract simplicial complex has a unique geometric realization, up to isomorphism.

Note also that a simplicial map between simplicial complexes induces an abstract simplicial map between the corresponding abstract simplicial complexes; conversely, an abstract simplicial map between two abstract simplicial complexes induces a simplicial map between their geometric realizations.

# Operations