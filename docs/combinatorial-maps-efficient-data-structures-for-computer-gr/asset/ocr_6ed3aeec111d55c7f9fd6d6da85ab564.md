# FIGURE 4.3

Submap isomorphism example.

(a) A 2-Gmap G.

(b) 2-Gmap G′ which is a submap of G as it is obtained from G by deleting the six darts in c₂(5) and the ten darts in c₂(7).

(c) 2-Gmap G″ which is not isomorphic to a submap of G as the injection f that respectively matches darts 1″ to 4″ to darts 1 to 4 does not verify the conditions of Def. 10: dart 1″ is 2-free and it is matched with dart 1 which is 2-sewn with dart 3 which is itself matched with 3″ (i.e. f⁻¹(3) = 3″).

# 4.2.1 Basic Tools

The first basic tool consists in adding a new dart in an n-Gmap. To guaranty the validity of the n-Gmap, the new dart is isolated, i.e. it is free for all dimensions (∀i ∈ {0,…,n}, αᵢ(d) = d). This operation can be used several times to add any number of isolated darts in the n-Gmap.

# Definition 11 (add isolated dart) Let G = (D, α₀, …, αₙ) be an n-Gmap. The n-Gmap obtained from G by adding an isolated dart d, d ∉ D, is G₊d = (D ∪ {d}, α′₀, …, α′ₙ), where ∀i ∈ {0,…,n}, α′ᵢ is defined by:

+   • ∀e ∈ D, α′ᵢ(e) = αᵢ(e);

+   • α′ᵢ(d) = d.

The inverse operation given in Def. 12 consists in removing an isolated dart.

# Definition 12 (remove isolated dart) Let G = (D, α₀, …, αₙ) be an n-Gmap and d ∈ D be an isolated dart, i.e. ∀i ∈ {0,…,n}, αᵢ(d) = d. The n-Gmap obtained from G by removing d is G₋d = (D \ {d}, α′₀, …, α′ₙ), where ∀i ∈ {0,…,n}, α′ᵢ is the restriction of αᵢ to the set of remaining darts, i.e. α′ᵢ = αᵢ|D\{d}.

Since only isolated darts are removed, the result of the operation is an n-Gmap. Note that any dart can be removed, but it is necessary to isolate it by applying (maybe several times) the unsew operation (cf. Section 4.2.3).