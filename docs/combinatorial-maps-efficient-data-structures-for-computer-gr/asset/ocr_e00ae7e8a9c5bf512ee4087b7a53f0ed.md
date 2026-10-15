The operation which increases the dimension of an n-Gmap is straightforward, and its definition is given in Def. 13. Increasing by one the dimension of an (n − 1)-Gmap G leads to create one n-cell for each connected component of G. All i-cells, for 0 ≤ i ≤ n − 1, are not modified by this operation.

# Definition 13 (increase dimension)

Let G = (D, α₀, …, αₙ₋₁) be an (n − 1)-Gmap. The n-Gmap obtained from G by increasing its dimension is G⁺ = (D, α₀, …, αₙ₋₁, αₙ), where αₙ is the identity on D, i.e. ∀d ∈ D, αₙ(d) = d.

The operation which decreases the dimension of an n-Gmap G is defined in Def. 14. This operation is the inverse of the increase dimension operation. It leads to the disappearance of all the n-cells that were in G.

# Definition 14 (decrease dimension)

Let G = (D, α₀, …, αₙ) be an n-Gmap such that ∀d ∈ D, αₙ(d) = d. The n-Gmap obtained from G by decreasing its dimension is G⁻ = (D, α₀, …, αₙ₋₁).

Note that this operation is restricted to an n-Gmap which has all its darts n-free, in order to get the inverse of the operation which increases the dimension. However, it is possible to first n-unsew all the non n-free darts, and then to decrease the dimension of the resulting n-Gmap.

Two distinct n-Gmaps can be merged into a same n-Gmap, which connected components are thus the connected components of the initial n-Gmaps (cf. Def. 15). The number of cells (resp. of connected components) of the resulting n-Gmap is the sum of the numbers of cells (resp. of connected components) of the two initial n-Gmaps.

# Definition 15 (merge)

Let G = (D, α₀, …, αₙ) and G′ = (D′, α′₀, …, α′ₙ) be two n-Gmaps such that D ∩ D′ = ∅. The n-Gmap obtained by merging G and G′ is G ∪ G′ = (D″, α″₀, …, α″ₙ), defined by:

+   - D″ = D ∪ D′;
+   - ∀d ∈ D″, ∀i ∈ {0, …, n}, α″ᵢ(d) = { αᵢ(d) if d ∈ D; α′ᵢ(d) if d ∈ D′. }

The reverse operation consists in splitting a given n-Gmap in two. It is based on the restrict operation defined in Def. 16: it takes as input a given n-Gmap and a subset of darts which correspond to a set of connected components, and build the n-Gmap restricted to this set of darts.

# Definition 16 (restrict)

Let G = (D, α₀, …, αₙ) be an n-Gmap, and D′ ⊆ D, such that ∀d ∈ D′, ∀i ∈ {0, …, n}, αᵢ(d) ∈ D′. The n-Gmap obtained by restricting G to D′ is G|D′ = (D′, α′₀, …, α′ₙ), where ∀i ∈ {0, …, n}, α′ᵢ = αᵢ|D′.