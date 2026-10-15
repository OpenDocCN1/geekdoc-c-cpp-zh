# FIGURE 8.10

(a) A 2-dimensional numbered simplicial quasi-manifold.

(b) The corresponding premap.

# Definition 88 (n-premap) An n-dimensional premap, with 0 ≤ n, is an (n + 2)-tuple P = (D, α₀, …, αₙ) where:

+   1. D is a finite set of darts;

+   2. ∀i ∈ {0, …, n}, αᵢ is an involution on D.

It is clear that (Kₙ, a₀, …, aₙ) as defined above is an n-premap: cf. Fig. 8.10. So, any numbered simplicial quasi-manifold can be associated with a unique n-premap. For instance in Fig. 8.10, dart 1 (resp. 2, 3, 4, 5, 6, 7, 8, 9, 10) is associated with 2-simplex A (resp. B, C, D, E, F, G, H, I, J). E and F share a 1-simplex numbered (1,2), thus α₀(5) = 6 and α₀(6) = 5; E is the single 2-simplex incident to its 1-face numbered (0,2), so α₁(5) = 5; E and D share a 1-simplex numbered (0,1), thus α₂(5) = 4 and α₂(4) = 5.

Conversely, let P = (D, α₀, …, αₙ) be an n-premap. Let I be any nonempty sequence (j₀, …, jᵢ) ⊂ [0,n]: associate with the set of orbits ⟨α₀, …, âⱼ₀, …, âⱼᵢ, …, αₙ⟩, denoted ⟨⟩ₙ\I, a set of simplices numbered (j₀, …, jᵢ).

For instance in Fig. 8.10:

+   A (resp. B, C, D, E, F, G, H, I, J) is associated with ⟨⟩(1) = ⟨â₀, â₁, â₂⟩(1) = ⟨⟩[0,2]\{1,2}(1) (resp. ⟨⟩(2), ⟨⟩(3), ⟨⟩(4), ⟨⟩(5), ⟨⟩(6), ⟨⟩(7), ⟨⟩(8), ⟨⟩(9), ⟨⟩(10));

+   1-simplices numbered (1,2), namely L (resp. N, P, m, n, o, p), correspond to ⟨α₀⟩(1) = ⟨⟩[0,2]\{1,2}(1) (resp. ⟨α₀⟩(3), ⟨α₀⟩(5), ⟨α₀⟩(7), ⟨α₀⟩(8), ⟨α₀⟩(9), ⟨α₀⟩(10)); 1-simplices numbered (0,2), namely k (resp. l, q, r, Q, S, U), correspond to ⟨α₁⟩(6) = ⟨⟩[0,2]\{0,2}(6) (resp. ⟨α₁⟩(1), ⟨α₁⟩(4), ⟨α₁⟩(5), ⟨α₁⟩(2), ⟨α₁⟩(8), ⟨α₁⟩(3)); 1-simplices numbered (0,1), namely K (resp. M, O, R, T), correspond to ⟨α₂⟩(1) = ⟨⟩[0,2]\{0,1}(1) (resp. ⟨α₂⟩(2), ⟨α₂⟩(4), ⟨α₂⟩(7), ⟨α₂⟩(9));