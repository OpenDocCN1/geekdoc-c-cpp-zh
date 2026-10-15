
# FIGURE 3.29

(a) A 1D quasi-manifold with boundary.

(b) The decomposition of the polygonal curve produces a set of isolated edges linked by α₁.

(c) The result of the decomposition of the pair of vertices describing the boundary of the isolated edges.

(d) Representation of the corresponding 1-Gmap.

![](img/6ba3cf72cbe3568e76a174448323bb33_102_0.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_102_1.png)

# FIGURE 3.30

(a) A 2D quasi-manifold with boundary.

(b) The decomposition of the surface in isolated faces, then the decomposition of the polygonal curves describing the boundary of the isolated faces produces a set of isolated edges linked by relations α₁ and α₂.

(c) Result of the decomposition of the pair of vertices describing the boundary of the isolated edges.

(d) Representation of the corresponding 2-Gmap.

# FIGURE 3.31

(a) Example of 3D quasi-manifold with boundary.
(b) Result of the decomposition of the 3D quasi-manifold into isolated volumes, the decomposition of the surfaces describing the boundary of the isolated volumes and the decomposition of the polygonal curves describing the boundary of the isolated faces.
(c) Result of the decomposition of the pair of vertices describing the boundary of the isolated edges.

![](img/6ba3cf72cbe3568e76a174448323bb33_103_0.png)

# FIGURE 3.32

(a) 3-Gmap describing the 3D quasi-manifold with boundary given in Fig. 3.31(a).
(b) Zoom on the face separating the hexahedron and the white pyramid.

![](img/6ba3cf72cbe3568e76a174448323bb33_103_1.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_104_0.png)

# FIGURE 3.33

Examples of cells in a 3-Gmap.

- (a) Volume containing dart 17.
- (b) Face containing dart 17.
- (c) Edge containing dart 17.
- (d) Vertex containing dart 17.

all the cells are successively decomposed by decreasing dimensions, from n to 1. At the end of this process, a set of isolated vertices is obtained, which correspond to the darts of the n-Gmap, plus n + 1 involutions on these darts α0, . . . , αn.

Each dart d corresponds to an n + 1 tuple of cells (c0, . . . , cn) and all these cells are incident to each other. A dart describes a part of a vertex, a part of an edge, a part of a face . . . a part of an n-cell. Each i-cell containing dart d is thus a set of darts that can be retrieved thanks to some specific orbits. As before, the notion of incidence and of adjacency between cells can be transposed directly on the corresponding set of darts.

For objects with boundaries, αi(d) = d encodes the fact that dart d has no neighbor dart for αi. This is different for n-maps, for which the convention is: βi(d) = ∅. Indeed, for n-maps, a dart d such that β1(d) = d is a loop (cf. chapter 8 for explanations based on simplicial interpretation).

# 4

# *n*-Gmaps

An *n*-Gmap is a combinatorial data structure allowing to describe an *n*-dimensional orientable or nonorientable quasi-manifold with or without boundary. An intuitive presentation of *n*-maps and *n*-Gmaps is provided in the previous chapter.

In this chapter, *n*-Gmaps are defined in Section 4.1, as the basic notions of cells, incidence and adjacency relations between the cells. Some basic operations allowing to modify existing *n*-Gmaps are presented in Section 4.2. These operations allow to add/remove darts, increase/decrease the dimension of an *n*-Gmap, merge/split *n*-Gmaps; the sew/unsew operations allow to identify cells. It is shown in Section 4.3 that these operations make a small basis of operations allowing to build any *n*-Gmap. Moreover, multi-incidence between cells can be taken into account with *n*-Gmaps, and some specific configurations related to multi-incidence are illustrated, such as dangling cells and folded cells. In Section 4.4, a possible data structure for implementing *n*-Gmaps is presented, and also some algorithms allowing to develop a computer software handling *n*-Gmaps. Section 4.5 contains some additional notions related to *n*-Gmaps.

In this book, *n*-Gmaps are studied before *n*-maps, because their definition is simpler: it is homogeneous, i.e. all functions involved in their definition are involutions. This simplifies many definitions and algorithms.

# 4.1 Basic Definitions

As explained in the previous chapter, an *n*-Gmap is defined by a set of darts on which act *n* + 1 involutions, satisfying some composition constraints. This leads to the following definition of *n*-Gmaps.

**Definition 1 (*n*-Gmap)** An *n*-dimensional generalized map, or *n*-Gmap, with 0 ≤ *n*, is an (*n* + 2)-tuple *G* = (*D*, α₀, . . . , αₙ) where:

- 1. *D* is a finite set of darts;
- 2. ∀*i* ∈ {0, . . . , *n*}: αᵢ is an involution on *D*;
- 3. ∀*i* ∈ {0, . . . , *n* − 2}, ∀*j* ∈ {*i* + 2, . . . , *n*}: αᵢ ∘ αⱼ is an involution.

![](img/6ba3cf72cbe3568e76a174448323bb33_106_0.png)

# FIGURE 4.1

Examples of 1-Gmap, 2-Gmap and 3-Gmap.
(a) A 1-Gmap (D, α₀, α₁).
(b) A 2-Gmap (D, α₀, α₁, α₂).
(c) A 3-Gmap (D, α₀, α₁, α₂, α₃).

A 0-Gmap (D, α₀) represents the structure (the topology) of a set of isolated vertices, or pairs of vertices (corresponding thus to 0-spheres); a 1-Gmap (D, α₀, α₁) represents the structure of a set of polygonal curves with or without boundaries (cf. Fig. 4.1(a)); a 2-Gmap (D, α₀, α₁, α₂) represents the structure of a set of surfaces (cf. Fig. 4.1(b)); a 3-Gmap (D, α₀, α₁, α₂, α₃) represents the structure of assemblies of volumes (cf. Fig. 4.1(c))...

As seen before, darts can be linked with themselves for some involutions when describing objects with boundaries. Dart d is i-free if it is linked with itself by αᵢ, and it is i-sewn otherwise (cf. Def. 2 and example in Fig. 4.2).

# Definition 2 (i-free, i-sewn) Let G = (D, α₀, …, αₙ) be an n-Gmap, d ∈ D, and i ∈ {0, …, n}:

- d is i-free if αᵢ(d) = d;
- d is i-sewn with dart d₂ ∈ D if αᵢ(d) = d₂ and d ≠ d₂.

When a dart is free for an involution, it is a fixed point for this involution.

For practical applications, it may be useful to handle objects with boundaries. Usually, a 3-dimensional subdivided object embedded into the usual 3-dimensional Euclidean space has 2-dimensional boundaries, which are surfaces without boundaries: it is composed by volumes, which boundaries are also surfaces without boundaries. So, these objects can be represented by a 3-Gmap, such that all darts are 0-sewn, 1-sewn, 2-sewn, and some darts can be 3-free. More generally, all involutions are often without fixed points, except αₙ.

However, in all generality, boundaries can exist in all dimensions: for instance, assume an n-dimensional object is cut by another object, for instance

![](img/6ba3cf72cbe3568e76a174448323bb33_107_0.png)

# FIGURE 4.2

A 2-Gmap with 0-boundary, 1-boundary and 2-boundary.

For example, dart 1 is 0-free, i.e. α₀(1) = 1. Thus dart 1 belongs to an edge incident to only one vertex.

Dart 2 is 1-free, i.e. α₁(2) = 2, so it belongs to an edge, such that no other edge is incident to the same vertex and to the same face.

Dart 3 is 2-free, i.e. α₂(3) = 3, thus dart 3 belongs to an edge which is incident to only one face.

by an (n − 1)-dimensional hyperplane: this hyperplane can cut cells of any dimensions, creating boundaries of any dimensions. An i-boundary (or a boundary in dimension i) corresponds to the fact that darts can be i-free (for any i).

As we have seen in the intuitive presentation, an n-Gmap can have different connected components. The set of darts that belong to the same connected component than a given dart can be retrieved, thanks to Def. 3: a connected component corresponds to an orbit for all involutions.

# Definition 3 (connected component) Let G = (D, α₀, …, αₙ) be an n-Gmap and d ∈ D. ⟨α₀, …, αₙ⟩(d) is the connected component containing d.

As said before, according to the context, an orbit denotes either a set of darts or this set of darts with the corresponding involutions. Thanks to this definition, we can directly test if a given n-Gmap is connected, i.e. made of only one connected component, simply by testing if the connected component of a dart is the set of all the darts of the n-Gmap (cf. Def. 4).

# Definition 4 (connected n-Gmap) Let G = (D, α₀, …, αₙ) be an n-Gmap. G is connected iff ⟨α₀, …, αₙ⟩(d) is equal to D, with d ∈ D.

Remember that a graph can be associated with a discrete structure such as an n-Gmap: a node of the graph corresponds to a dart, and an edge numbered i links two nodes corresponding to two darts linked by αᵢ (when a dart is a
