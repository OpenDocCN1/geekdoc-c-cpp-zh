![](bbox=[0.112, 0.092, 0.804, 0.306])

# **FIGURE 6.52**

3-triangulation for 3-Gmap.
(a) The result of the 3-triangulation of the 3-cell in a 3-Gmap representing a cube.
(b) Zoom on one volume issued from the 3-triangulation.

+   - ∀d ∈ C:
+     2. α′₀(φ⁰(d)) = φ¹(d);
+     3. ∀j ∈ {1, …, i}, α′ⱼ(φ⁰(d)) = φ⁰(αⱼ₋₁(d));
+     4. ∀j ∈ {i + 1, …, n}, α′ⱼ(φ⁰(d)) = φ⁰(αⱼ(d));
+     5. ∀j ∈ {0, …, n}, j ≠ i − 1, α′ⱼ(d) = αⱼ(d);
+     6. α′ᵢ₋₁(d) = φ⁻¹(d);
+   
+   - ∀k ∈ {1, …, i − 1}, ∀d ∈ C:
+     7. ∀j ∈ {0, …, k − 2}, α′ⱼ(φᵏ(d)) = φᵏ(αⱼ(d));
+     8. α′ₖ₋₁(φᵏ(d)) = φᵏ⁻¹(d);
+     9. α′ₖ(φᵏ(d)) = φᵏ⁺¹(d);
+     10. ∀j ∈ {k + 1, …, i}, α′ⱼ(φᵏ(d)) = φᵏ(αⱼ₋₁(d));
+     11. ∀j ∈ {i + 1, …, n}, α′ⱼ(φᵏ(d)) = φᵏ(αⱼ(d)).

This operation is implemented by Algorithm 66. The n-Gmap gm is modified in order to obtain the result of the i-triangulation operation. The operation is similar to the two previous operations: new darts are created and stored in phi associative arrays (there is one associative array phi[j] for each j ∈ {0, …, i}). α involutions are modified for these darts, according to the definition. The algorithm returns a dart belonging to the new vertex, since this dart could be used after the operation.