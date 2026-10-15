
**Figure 8.10**

(a) A 2-dimensional numbered simplicial quasi-manifold.

(b) The corresponding premap.

**Definition 88 (n-premap)**

An n-dimensional premap, with 0 ≤ n, is an (n + 2)-tuple P = (D, α₀, …, αₙ) where:

- 1. D is a finite set of darts;
- 2. ∀i ∈ {0, …, n}, αᵢ is an involution on D.

It is clear that (Kₙ, a₀, …, aₙ) as defined above is an n-premap: cf. Fig. 8.10. So, any numbered simplicial quasi-manifold can be associated with a unique n-premap. For instance in Fig. 8.10, dart 1 (resp. 2, 3, 4, 5, 6, 7, 8, 9, 10) is associated with 2-simplex A (resp. B, C, D, E, F, G, H, I, J). E and F share a 1-simplex numbered (1,2), thus α₀(5) = 6 and α₀(6) = 5; E is the single 2-simplex incident to its 1-face numbered (0,2), so α₁(5) = 5; E and D share a 1-simplex numbered (0,1), thus α₂(5) = 4 and α₂(4) = 5.

Conversely, let P = (D, α₀, …, αₙ) be an n-premap. Let I be any nonempty sequence (j₀, …, jᵢ) ⊂ [0,n]: associate with the set of orbits ⟨α₀, …, α̂ⱼ₀, …, α̂ⱼᵢ, …, αₙ⟩, denoted ⟨⟩_{[0,n]∖I}, a set of simplices numbered (j₀, …, jᵢ).

For instance in Fig. 8.10:

- A (resp. B, C, D, E, F, G, H, I, J) is associated with ⟨⟩(1) = ⟨α̂₀, α̂₁, α̂₂⟩(1) = ⟨⟩_{[0,2]∖{0,1,2}}(1) (resp. ⟨⟩(2), ⟨⟩(3), ⟨⟩(4), ⟨⟩(5), ⟨⟩(6), ⟨⟩(7), ⟨⟩(8), ⟨⟩(9), ⟨⟩(10));

- 1-simplices numbered (1,2), namely L (resp. N, P, m, n, o, p), correspond to ⟨α₀⟩(1) = ⟨⟩_{[0,2]∖{1,2}}(1) (resp. ⟨α₀⟩(3), ⟨α₀⟩(5), ⟨α₀⟩(7), ⟨α₀⟩(8), ⟨α₀⟩(9), ⟨α₀⟩(10)); 1-simplices numbered (0,2), namely k (resp. l, q, r, Q, S, U), correspond to ⟨α₁⟩(6) = ⟨⟩_{[0,2]∖{0,2}}(6) (resp. ⟨α₁⟩(1), ⟨α₁⟩(4), ⟨α₁⟩(5), ⟨α₁⟩(2), ⟨α₁⟩(8), ⟨α₁⟩(3)); 1-simplices numbered (0,1), namely K (resp. M, O, R, T), correspond to ⟨α₂⟩(1) = ⟨⟩_{[0,2]∖{0,1}}(1) (resp. ⟨α₂⟩(2), ⟨α₂⟩(4), ⟨α₂⟩(7), ⟨α₂⟩(9));

- 0-simplices numbered (2), namely b (resp. d, f, h), correspond to ⟨α₀, α₁⟩(1) = ⟨⟩_{[0,2]∖{2}}(1) (resp. ⟨α₀, α₁⟩(8), ⟨α₀, α₁⟩(3), ⟨α₀, α₁⟩(5)); 0-simplices numbered (1), namely c (resp. e, i), correspond to ⟨α₀, α₂⟩(7) = ⟨⟩_{[0,2]∖{1}}(7) (resp. ⟨α₀, α₂⟩(9), ⟨α₀, α₂⟩(1)); 0-simplices numbered (0), namely a (resp. g, j), correspond to ⟨α₁, α₂⟩(1) = ⟨⟩_{[0,2]∖{0}}(1) (resp. ⟨α₁, α₂⟩(4), ⟨α₁, α₂⟩(2)).

The face operators are defined in the following way: let I = (j₀, …, jᵢ) be such that i ≥ 1, d be a dart, and σ be the simplex associated to ⟨⟩_{[0,n]∖I}(d); then dᵢ(σ) is the (i − 1)-simplex associated with ⟨⟩_{[0,n]∖(I − {jᵢ})}(d). For instance in Fig. 8.10:

- d₀(A) = L, since A is associated with ⟨⟩_{[0,2]∖{0,1,2}}(1) = ⟨⟩(1) and L is associated with ⟨⟩_{[0,2]∖({0,1,2}−{0})}(1) = ⟨α₀⟩(1); d₁(A) = l, since l is associated with ⟨⟩_{[0,2]∖({0,1,2}−{1})}(1) = ⟨α₁⟩(1); d₂(A) = K, since K is associated with ⟨⟩_{[0,2]∖({0,1,2}−{2})}(1) = ⟨α₂⟩(1); note that this is coherent with the fact that, for any i, 0 ≤ i ≤ n, αᵢ corresponds to an “adjacency relation” between n-simplices sharing a common face obtained by dᵢ;

- d₀(K) = i (resp. d₁(K) = a), since K is associated with ⟨⟩_{[0,2]∖{0,1}}(1) = ⟨α₂⟩(1) and i (resp. a) is associated with ⟨⟩_{[0,2]∖{1}}(1) = ⟨α₀, α₂⟩(1) (resp. ⟨⟩_{[0,2]∖{0}}(1) = ⟨α₁, α₂⟩(1)); d₀(l) = b (resp. d₁(l) = a), since l is associated with ⟨⟩_{[0,2]∖{0,2}}(1) = ⟨α₁⟩(1) and b (resp. a) is associated with ⟨⟩_{[0,2]∖{2}}(1) = ⟨α₀, α₁⟩(1) (resp. ⟨⟩_{[0,2]∖{0}}(1) = ⟨α₁, α₂⟩(1)); d₀(L) = b (resp. d₁(L) = i), since L is associated with ⟨⟩_{[0,2]∖{1,2}}(1) = ⟨α₀⟩(1) and b (resp. i) is associated with ⟨⟩_{[0,2]∖{2}}(1) = ⟨α₀, α₁⟩(1) (resp. ⟨⟩_{[0,2]∖{1}}(1) = ⟨α₀, α₂⟩(1));

At last, any 0-simplex corresponding to an orbit ⟨⟩_{[0,n]∖{i}} = ⟨α₀, …, α̂ᵢ, …, αₙ⟩ is numbered i (and this is coherent with the numbering of face operators).

So, any n-premap can be associated with a unique n-dimensional numbered simplicial quasi-manifold.

In conclusion, n-dimensional numbered simplicial quasi-manifolds are equivalent to n-premaps, and the conversion processes described above are inverse to each other.

## Cellular quasi-manifolds and n-Gmaps

The conversion processes described above still apply for n-dimensional cellular quasi-manifolds and n-Gmaps. So, n-dimensional cellular quasi-manifolds are equivalent to n-Gmaps.

More precisely, a 0-dimensional cellular quasi-manifold is a set of components, each component contains one or two vertices numbered 0. Each connected component of a 0-Gmap G = (D, α₀) contains one or two darts: so, the orbits ⟨⟩_{[0]∖{0}} = ⟨⟩ correspond in the first case to one vertex numbered 0, and in the second case to two vertices numbered 0.

Assume an (n − 1)-dimensional cellular quasi-manifold Q is equivalent to an (n − 1)-Gmap G = (D, α₀, …, αₙ₋₁). Let Q′ be the n-dimensional cellular quasi-manifold defined by constructing cellular cones for all connected components of Q; let G′ = (D, α₀, …, αₙ₋₁, αₙ = Id), where Id is the identity on D, be the n-Gmap deduced from G by increasing its dimension. Then Q′ is equivalent to G′. In fact (cf. Fig. 8.11):

- any i-simplex σ numbered {j₀, …, jᵢ} in Q is a simplex of Q′. Let d be a dart, such that σ corresponds to orbit O = ⟨α₀, …, α̂ⱼ₀, …, α̂ⱼᵢ, …, αₙ₋₁⟩(d) in G; σ corresponds also to orbit O′ = ⟨α₀, …, α̂ⱼ₀, …, α̂ⱼᵢ, …, αₙ₋₁, αₙ⟩(d) in G′, and O and O′ are equal since αₙ = Id;

- a unique (i+1)-simplex σ′, numbered {j₀, …, jᵢ, n}, is associated with σ in Q′: σ′ corresponds to the orbit ⟨α₀, …, α̂ⱼ₀, …, α̂ⱼᵢ, …, αₙ₋₁, α̂ₙ⟩(d) in G′, which clearly is equal to O;

- at last, for each connected component of Q, a unique 0-simplex numbered n is created in Q′; corresponding to the unique orbit ⟨α₀, …, αₙ₋₁⟩ in G′ associated with the corresponding connected component in G.

Assume an n-dimensional cellular quasi-manifold Q is equivalent to an n-Gmap G = (D, α₀, …, αₙ₋₁, αₙ). Let c₁ and c₂ be two (n − 1)-cells, incident respectively to (n − 1)-simplices σ₁ and σ₂, such that σ₁ ≠ σ₂, σ₁ (resp. σ₂) is incident to a unique n-simplex, and an isomorphism φ associates c₁ and c₂, with φ(σ₁) = σ₂ (and φ = φ⁻¹ if c₁ = c₂). Let d₁ (resp. d₂) be the dart of D corresponding to the n-simplex incident to σ₁ (resp. σ₂): note that ⟨αₙ⟩(d₁) = {d₁} corresponds to σ₁ (resp. ⟨αₙ⟩(d₂) = {d₂} corresponds to σ₂). Let Q′ be the n-dimensional cellular quasi-manifold defined by identifying c₁ and c₂ according to φ; let G′ = (D, α₀, …, αₙ₋₁, α′ₙ) be the n-Gmap deduced from G by n-sewing d₁ and d₂. Then Q′ is equivalent to G′. In fact:

- isomorphism φ induces an isomorphism φ′ between orbits ⟨α₀, …, αₙ₋₂⟩(d₁) and ⟨α₀, …, αₙ₋₂⟩(d₂) (or an automorphism such that φ′ = φ′⁻¹ on orbit ⟨α₀, …, αₙ₋₂⟩(d₁) if φ is an automorphism on c₁);

- identifying σ₁ and σ₂ (and all simplices corresponding by φ) corresponds to link d₁ and d₂ by α′ₙ (and all darts corresponding by φ′), since ⟨α′ₙ⟩(d₁) = {d₁, d₂}.

**Figure 8.11**

(a) A connected 1-dimensional cellular quasi-manifold.

(b) The connected 2-dimensional cellular quasi-manifold obtained by a cellular cone.

(c) The 1-Gmap corresponding to (a).

(d) The 2-Gmap corresponding to (b). i (resp. j) in (a) corresponds to orbit ⟨⟩(1) (resp. ⟨α₀⟩(1)) in (c). i (resp. j) in (b) corresponds to orbit ⟨α₂⟩(1) (resp. ⟨α₀, α₂⟩(1)) in (d). i′ (resp. j′), associated with i (resp. j), corresponds to orbit ⟨⟩(1) (resp. ⟨α₀⟩(1)) in (d). The connected component of (a) (resp. of (b)) corresponds to orbit ⟨α₀, α₁⟩(1) in (c) (resp. to orbit ⟨α₀, α₁, α₂⟩(1) in (d)); 0-simplex v numbered (2) in (b) corresponds to orbit ⟨α₀, α₁⟩(1) in (d).

So, n-Gmaps correspond to cellular quasi-manifolds and premaps correspond to numbered simplicial quasi-manifolds. The interior of any cell of any cellular quasi-manifold corresponds to the interior of a cellular quasi-manifold; this is not the case for any cell of a numbered simplicial quasi-manifold. This corresponds to the fact that, given any n-Gmap, the involutions whose indices differ by at least 2 commute; this is not the case for any premap.

## Orientable quasi-manifolds and (hyper)maps

Let Q be an n-dimensional numbered simplicial quasi-manifold, and let P = (D, α₀, …, αₙ) be the associated premap. Remember that simplices are implicitly oriented within semi-simplicial sets. For instance, look at the 2-dimensional simplicial quasi-manifold in Fig. 8.12: assume 2-simplices are oriented according to their numbering, i.e. their orientations correspond to the sequence (0, 1, 2). So, the orientation of a 2-simplex is the inverse of the orientations of the 2-simplices which share a 1-simplex with it. This property can be extended for any dimension. That means that, given an n-simplex σ corresponding to a dart d in P, its orientation is inverse to that of the n-simplices corresponding to darts αᵢ(d), for 0 ≤ i ≤ n.

Let Q be a connected quasi-manifold without boundary, i.e. any (n − 1)-simplex is incident to two distinct n-simplices; this means that P is connected too, and that all involutions in P are without fixed points. Q is orientable if it is possible to orient all n-simplices in a coherent way. This can be checked in the following way. Choose an n-simplex with its implicit orientation; for
