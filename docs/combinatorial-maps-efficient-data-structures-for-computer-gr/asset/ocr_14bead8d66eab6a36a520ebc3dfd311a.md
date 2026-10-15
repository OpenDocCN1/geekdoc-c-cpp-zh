α₂''(dd'¹) = d(α₁'(d'))¹. For example, α₂''(b2¹) = b3¹.

In Fig. 6.49, a 2-Gmap is extruded along a path. Three darts in G_extr(G'), dd'⁰, dd'¹ and dd'², correspond to each pair (d, d'), such that d (resp. d') is a dart of G (resp. G'). The rules for linking the darts are similar to the 1D case:

+   - α₀''(dd'⁰) = d(α₀'(d'))⁰. For example, α₀''(a1⁰) = a2⁰;
+   - α₀''(dd'¹) = (α₀(d))d'¹. For example, α₀''(a1¹) = b1¹;
+   - α₀''(dd'²) = (α₀(d))d'². For example, α₀''(a1²) = b1²;
+   - α₁''(dd'⁰) = dd'¹ (and reciprocally). For example, α₁''(a1⁰) = a1¹;
+   - α₁''(dd'²) = (α₁(d))d'². For example, α₁''(a1²) = h1²;
+   - α₂''(dd'⁰) = (α₁(d))d'⁰. For example, α₂''(a1⁰) = h1⁰;
+   - α₂''(dd'¹) = dd'² (and reciprocally). For example, α₂''(a1¹) = a1²;
+   - α₃''(dd'⁰) = (α₂(d))d'⁰. For example, α₃''(h1⁰) = i1⁰;
+   - α₃''(dd'¹) = (α₂(d))d'¹. For example, α₃''(h1¹) = i1¹;
+   - α₃''(dd'²) = d(α₁'(d'))². For example, α₃''(a2²) = a3².

These rules can be generalized for dimension n, and the extrusion operation is defined in Def. 73. n + 1 bijections φʲ are defined in order to associate the different darts issued from the same pair of original darts (i.e. φⁱ(dd') = dd'ⁱ). The first three items in the definition define α'' for the darts of D⁰, the three next items define α'' for the darts of Dⁿ, and the last four items define α'' for the darts of D¹, …, Dⁿ⁻¹ (note that the definitions for D⁰ and Dⁿ are simply particular cases of the general definitions).

# Definition 73 (extrusion) Let G = (D, α₀, …, αₙ) be an n-Gmap and G' = (D', α₀', α₁') be a 1-Gmap. The (n + 1)-Gmap resulting from the extrusion of G along G' is G_extr(G') = (D'', α₀'', …, αₙ₊₁''), defined by:

+   - ∀j ∈ {0, …, n}, let Dʲ be a set of new darts, such that a bijection φʲ maps D × D' onto Dʲ;
+   - D'' = ∪_{j=0}^n Dʲ;
+   - ∀d ∈ D, ∀d' ∈ D':
+     1. α₀''(φ⁰(d, d')) = φ⁰(d, α₀'(d'));
+     2. α₁''(φ⁰(d, d')) = φ¹(d, d');
+     3. ∀i ∈ {2, …, n + 1}, αᵢ''(φ⁰(d, d')) = φ⁰(α_{i-1}(d), d');
+     4. ∀i ∈ {0, …, n − 1}, αᵢ''(φⁿ(d, d')) = φⁿ(αᵢ(d), d');