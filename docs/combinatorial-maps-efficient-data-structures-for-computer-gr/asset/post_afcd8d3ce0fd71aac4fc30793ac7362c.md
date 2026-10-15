
α₀ in the corresponding n-Gmap. Let us consider here the case where M is without boundary. By definition, G is also without boundary. The Euler-Poincaré characteristic of G is:

χ(G) = Σ_{i=0}^{n} (-1)^{(n-i)} Σ_{0≤k₀<...<k_{i-1}≤n} #⟨α_{k₀},...,α_{k_{i-1}}⟩.

This sum can be decomposed into four parts:

χ(G) = (-1)^n #⟨⟩ + (-1)^{(n-1)} Σ_{0≤k₀≤n} #⟨α_{k₀}⟩ + Σ_{i=2}^{n} (-1)^{(n-i)} Σ_{0=k₀<k₁<...<k_{i-1}≤n} #⟨α₀,α_{k₁},...,α_{k_{i-1}}⟩ + Σ_{i=2}^{n} (-1)^{(n-i)} Σ_{0<k₀<...<k_{i-1}≤n} #⟨α_{k₀},...,α_{k_{i-1}}⟩.

For the first sum, (-1)^n #⟨⟩ = (-1)^n |D_G| (|D_G| is the number of darts of G which is equal to 2|D| the number of darts of M).

For the second sum, since G is without boundary, #⟨α_{k₀}⟩ = |D_G|/2 for any k₀ ∈ {0,...,n}. This gives (-1)^{(n-1)} Σ_{0≤k₀≤n} #⟨α_{k₀}⟩ = (-1)^{(n-1)} (n+1) |D_G|/2.

By definition of orbits, ⟨α_{k₀},...,α_{k_{i-1}}⟩ ≡ ⟨α_{k₁}∘α_{k₀},...,α_{k_{i-1}}∘α_{k₀}⟩. This property is used for the two last parts of the sum. First:

⟨α₀,α_{k₁},...,α_{k_{i-1}}⟩ = ⟨α_{k₁}∘α₀,...,α_{k_{i-1}}∘α₀⟩ = ⟨β_{k₁},...,β_{k_{i-1}}⟩.

Here the definition of the conversion between n-maps and n-Gmaps is used to link α_{k_j}∘α₀ and β_{k_j}.

Second:

⟨α_{k₀},...,α_{k_{i-1}}⟩ = ⟨α_{k₁}∘α_{k₀},...,α_{k_{i-1}}∘α_{k₀}⟩ = ⟨β_{k₁}∘β_{k₀},...,β_{k_{i-1}}∘β_{k₀}⟩.

Here α_{k_j}∘α_{k₀} is transformed into α_{k_j}∘α₀∘α₀∘α_{k₀} and the definition of the conversion between n-maps and n-Gmaps is used to obtain β_{k_j}∘β_{k₀} (here k_j > 1 thus β_{k_j} is an involution).

This gives the following Euler-Poincaré characteristic of an n-map without boundary:

## Definition 92 (Euler-Poincaré characteristic of an n-map) Let M = (D,β₁,...,βₙ) be an n-map without boundary, with n > 0. Its Euler-Poincaré

characteristic χ(M) is the alternated sum:

χ(M) = (-1)^(n-1)(n - 1)|D| + Σ_{i=2}^n (-1)^(n-i) Σ_{0<k₁<...<k_{i-1}≤n} #⟨β_{k₁},...,β_{k_{i-1}}⟩ + Σ_{i=2}^n (-1)^(n-i) Σ_{0<k₀<...<k_{i-1}≤n} #⟨β_{k₁}∘β_{k₀},...,β_{k_{i-1}}∘β_{k₀}⟩.

Note that it is possible to extend this formula to consider n-maps with boundary, but the definition becomes more complex since the case of free darts has to be taken into account.

For 1D, the previous definition becomes χ(M) = 0. Any 1-map M without boundary (i.e. closed polygonal curves) has the Euler-Poincaré characteristic of a circle.

For 2D, the previous definition becomes χ(M) = -|D| + #⟨β₁⟩ + #⟨β₂⟩ + #⟨β₂∘β₁⟩. Figure 8.20 shows two examples of 2-maps and their corresponding Euler-Poincaré characteristics. For M₁ given in Fig. 8.20(a), |D| = 6, #⟨β₁⟩ = 3, #⟨β₂⟩ = 3, #⟨β₂∘β₁⟩ = 2: thus χ(M₁) = -6 + 3 + 3 + 2 = 2: this is the Euler-Poincaré characteristic of a sphere. For M₂ given in Fig. 8.20(b), |D| = 4, #⟨β₁⟩ = 1, #⟨β₂⟩ = 2, #⟨β₂∘β₁⟩ = 1: thus χ(M₂) = -4 + 1 + 2 + 1 = 0: this is the Euler-Poincaré characteristic of a torus.

![](img/6ba3cf72cbe3568e76a174448323bb33_355_0.png)

# FIGURE 8.20

Examples of 2-maps and their Euler-Poincaré characteristics.

- (a) M₁ describes a sphere: χ(M₁) = 2.
- (b) M₂ describes a torus: χ(M₂) = 0.

For 3D, the previous definition becomes χ(M) = 2|D| - #⟨β₁⟩ - #⟨β₂⟩ - #⟨β₃⟩ + #⟨β₁,β₂⟩ + #⟨β₁,β₃⟩ + #⟨β₂,β₃⟩ - #⟨β₂∘β₁⟩ - #⟨β₃∘β₁⟩ - #⟨β₃∘β₂⟩ + #⟨β₂∘β₁,β₃∘β₁⟩.

In 2D, the Euler-Poincaré characteristics of a 2-map without 1-boundary

but possibly with 2-boundary can be computed by using the correspondence between a 2-map M and an equivalent 2-Gmap G. In this case, the 2-Gmap has no 0 nor 1-boundary and thus χ(G) = −#⟨α₂⟩ + #⟨α₀, α₁⟩ + #⟨α₀, α₂⟩ + #⟨α₁, α₂⟩. Since G is without 0-boundary, #⟨α₂⟩ = 2#⟨α₀, α₂⟩ − |{d|α₀(d) = α₂(d)}|. Indeed, for a dart d such α₀(d) = α₂(d), there is one orbit ⟨α₂⟩ for one orbit ⟨α₀, α₂⟩, while for other darts, there are two orbits ⟨α₂⟩ for one orbit ⟨α₀, α₂⟩. Then the correspondence between M and G gives the Euler-Poincaré characteristic of a 2-map:

χ(M) = #⟨β₂ ∘ β₀⟩ − #⟨β₂⟩ + #⟨β₁⟩ + |{d|β₂(d) = d}|.

If the 2-map has no 1-boundary and no folded cell, |{d|α₀(d) = α₂(d)}| = 0 and the previous formula becomes χ(M) = #⟨β₂ ∘ β₀⟩ − #⟨β₂⟩ + #⟨β₁⟩. This gives the classical definition of the Euler-Poincaré characteristic equal to the number of vertices minus the number of edges plus the number of faces.

Let us consider the 2-map M₃ obtained from 2-map M₁ given in Fig. 8.20(a) where we remove the two darts 5 and 6. #⟨β₁⟩ = 1, #⟨β₂⟩ = 3, #⟨β₂ ∘ β₀⟩ = 2 and |{d|β₂(d) = d}| = 0: thus χ(M₃) = 1 − 3 + 2 + 0 = 0: this is the Euler-Poincaré characteristic of an annulus.

## 9

## Comparison with Other Cellular Data Structures

In this chapter, *n*-maps and *n*-Gmaps are compared with related cellular data structures. Many different data structures have been proposed in order to describe subdivided objects. They can be classified according to:

- the dimension of the represented objects;
- the topological properties of the represented objects: non-manifold, pseudo-manifold, quasi-manifold, orientable, nonorientable...
- the type of cells: regular cells, as triangles (and more generally simplices), quadrangles (and more generally cubes, simploids), general cells...

Remember that *n*-maps allow to represent *n*-dimensional orientable quasi-manifolds with general cells, and *n*-Gmaps allow to represent *n*-dimensional orientable and nonorientable quasi-manifolds with general cells. Thus, we limit in this chapter the comparison with data structures corresponding to these two classes (see also for instance [164, 208]). A more general discussion is conducted in the next chapter 10.

Schematically, the first work about data structures for representing subdivided geometric objects is the definition of the *winged-edge* data structure by Baumgart at the beginning of the 1970s [17]. Then, during the 1980s, many works in geometric modeling and computational geometry dealt with the definition of data structures for representing orientable (quasi-)manifolds without boundaries, then general (quasi-)manifolds, for dimension 2, then dimension 3, at last dimension *n* (cf. next section). At the end of the 1980s and during the 1990s, many data structures for representing complexes have been conceived, from dimension 2 to dimension *n* (see for instance [102, 195, 216, 104, 159]).

In parallel, several authors studied data structures and operations for representing simplicial objects (e.g. [90]). Some ideas, as the representation of adjacency relations between *n*-cells, when handling *n*-dimensional quasi-manifolds, were applied for simplicial structures as for cellular structures (see for instance [183]).

Note that during the 1990s and 2000s, the definition of subclasses close to manifolds was a subject of great interest, for simplicial structures, incidence graphs and ordered cellular structures (see for instance [89, 91, 85, 39, 165]).

Since the beginning of the 2000s, two very interesting research directions are explored:

- the conception of hierarchical structures, for instance for representing objects at different detail levels (e.g. [88, 200, 148]); this is also a subject of interest for the image analysis community since the beginning of the 1990s (e.g. [151, 44, 197, 188]);
- the compression of the representation, for instance for the storage of huge subdivisions (e.g. [204, 190, 129]).

### 9.1 History of Combinatorial Maps

The first work about combinatorial maps started in the 1960s in mathematics, more precisely in the field of combinatorics, in order to represent planar graphs embedded in the plane. They were introduced in [103] to describe *polyhedral surfaces*, then formally defined in [206, 137]. In the different works, different names were used: *planar maps*, *topological graphs*, *constellations* or *rotation systems*. These concepts were used in combinatorial graph theory, for problems of compact encoding of planar graphs, enumeration of rooted planar graphs or for the map-coloring problem [54, 55, 191, 192].

When a graph is embedded in a plane, edges are ordered around vertices, for instance according to a clockwise orientation. It is then possible to define a function *f*, giving for each edge its next edge around one of its vertex. However, since each edge has two different successors, one for each extremity vertex, each edge has two associated edges and thus *f* is not a function¹. This problem can be solved by cutting each edge in two half-edges: so, each half-edge has only one extremity, and thus only one successor by *f*. This cutting requires to add a relation between the two half-edges issued from the same edge. This gives the original definition of planar maps: a planar map is a set of half-edges (called “darts” according to the terminology of combinatorial maps), plus two functions defined on these half-edges: σ, which gives the next half-edge around its incident vertex, and α, which gives the other half-edge issued from the same edge. Formally, σ is a permutation and α is an involution.

Thanks to these two functions, the notions of vertices, edges and faces can be retrieved. A vertex is the cycle of half-edges obtained from a given half-edge, by applying σ until going back to the initial half-edge. An edge is the set of two half-edges linked by α. Since a planar map describes a planar graph embedded in the plane, cycles of edges describe the boundary of faces. Given a half-edge h, the next half-edge of the face is σ ∘ α(h), denoted φ(h). A face
