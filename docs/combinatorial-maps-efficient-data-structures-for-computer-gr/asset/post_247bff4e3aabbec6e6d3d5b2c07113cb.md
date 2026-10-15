
## FIGURE 9.1

Planar map and link with 2-maps.

- (a) Planar graph embedded in the plane.
- (b) Corresponding planar map. D = {1, …, 18} is the set of half-edges; σ is represented by gray arrows; α links two half-edges sharing a little perpendicular segment.
- (c) Corresponding 2-map (D, φ, α).

is thus the cycle of half-edges obtained from a given half-edge, by applying φ until going back to the initial half-edge.

As illustrated in Fig. 9.1, planar maps are equivalent to 2-maps without boundary, where darts correspond to half-edges, β₁ to φ and β₂ to α. Figure 9.1(b) shows a planar map, and Fig. 9.1(c) the corresponding 2-map. For example: σ(1) = 7, σ(7) = 9 and σ(9) = 1; α(1) = 2 and α(2) = 1; φ(2) = 7, φ(7) = 6, φ(6) = 4 and φ(4) = 2.

Planar maps have been extended during the 1980s by several works in the field of combinatorics, leading to notions equivalent to 2-Gmaps [47] and to n-Gmaps [212].

In the 1980s, similar notions were retrieved by works related to geometric modeling, computational geometry and computer graphics. For instance, the half-edge data structure [214] is basically a 2-map without boundary. Several versions and variants were also defined [172, 86] (see Section 9.2.2). The quad-edge data structure is close to 2-Gmaps: cf. Section 9.3.1; the facet-edge data structure is close to 3-Gmaps: cf. Section 9.3.2. The radial-edge data structure [216] has been defined in order to represent 2-dimensional complexes, i.e. 2D non-manifolds. In fact, this structure is very close to 3-maps, extended to take into account several “non-manifold configurations”: cf. Section 9.2.3 and Section 9.2.4.

At the end of the 1980s, 2-maps were extended in 3D [9, 10, 203] and in nD [162, 165]. In the original definition, n-maps allow to describe n-dimensional orientable quasi-manifold without boundary. The extension for representing n-dimensional orientable quasi-manifold with or without boundary was made formally much later [189, 83], even if many people use since a long time in many different softwares different implementations of modified n-maps allowing boundaries.

## TABLE 9.1

Winged-edge pointers, and relations with 2-maps. Each edge corresponds to two darts linked by β₂

| Winged-edge pointer | In 2-maps |
| --- | --- |
| vertex1 | vertex emb₀(d) |
| vertex2 | vertex emb₀(β₂(d)) |
| right_face | face emb₂(β₂(d)) |
| left_face | face emb₂(d) |
| prev_left_face | winged edge β₀(d) |
| next_left_face | winged edge β₁(d) |
| prev_right_face | winged edge β₁(β₂(d)) |
| next_right_face | winged edge β₀(β₂(d)) |

Also at the end of 1980s, n-Gmaps were introduced in the field of geometric modeling [162, 165].

Simultaneously, at the end of the 1980s, several works related to image processing started to use combinatorial maps in order to describe 2D segmented images: they extended previous works based on region adjacency graphs [36]. These works were pursued in the 1990s: several image processing algorithms have been proposed, based on 2-maps and some variants (such as the topological graph of frontier [109, 110] or discrete maps [36, 95, 40]). Mainly, image edition methods [16, 116, 37] and image segmentation algorithms [42, 41, 33, 32, 3, 144, 43, 66] were concerned. In the beginning of the 2000s, previous works were extended for processing 3D images, thanks to the use of 3-maps [34, 58, 59, 15, 98, 100, 97].

## 9.2 Oriented Cellular Quasi-Manifolds

### 9.2.1 Winged-edge

The first data structure defined in order to describe 2D subdivisions for computer vision purposes is the winged-edge data structure [17].

The main element of this data structure is the winged-edge, which is an edge having eight pointers to different incident cells. The main structural information is related to the four pointers which make it possible to access the incident edges by turning clockwise and counterclockwise around the incident vertices: cf. Fig. 9.2. The winged-edge is often used for solid modeling, i.e. for representing the surface which bounds a polyhedron. By convention, clockwise ordering corresponds to a view from outside of the polyhedron, and this ordering is used for traversing the subdivision.

## FIGURE 9.2

- (a) Winged-edge representation of the 2D quasi-manifold without boundary depicted in Fig. 3.4(a) page 56. The eight pointers from edge e1 are drawn by arrows.
- (b) Corresponding 2-map.

![](img/6ba3cf72cbe3568e76a174448323bb33_361_0.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_361_1.png)

In addition to the list of winged-edges, there is also a list of vertices and a list of faces. Different information is associated with vertices and faces: for example, a 3D point is associated with each vertex, a color is associated with each face, and a pointer is associated with each vertex (resp. face), making it possible to access one of its incident winged-edge.

Winged-edges allow to represent oriented 2D manifold without boundary: they are equivalent to 2-maps without boundary. Each winged-edge corresponds to a pair of darts linked by β₂; relations between the winged-edges can easily be translated in corresponding relations in the 2-map (see Table 9.1). Note that the lists of vertices and faces often exist in 2-maps data structures (cf. chapter 7), when 0- and 2-embeddings are defined; in this case, embeddings are often linked with one of the darts of the associated cells, in order to access the structural information from a given embedding.

A winged-edge structure is represented in Fig. 9.2(a); it corresponds to the 2D object depicted in Fig. 3.4(a) page 56; the corresponding 2-map is represented in Fig. 9.2(b). For example, vertex1(e1) = v1, vertex2(e1) = v4, left_face(e1) = f2, right_face(e1) = f3, prev_left_face(e1) = e2, next_left_face(e1) = e4, prev_right_face(e1) = e8, next_right_face(e1) = e5.

A simplified version of the winged-edge data structure was proposed, in which all pointers are not represented [179]. This version uses less memory space, but it allows only the traversal of the boundary of a face in the clockwise direction. Note that this memory optimization can also be done for 2-maps, by not explicitly representing β₀ in the dart data structure. An extension of winged-edges has also been proposed in [48], in order to describe 2-manifolds with or without boundary.

## TABLE 9.2

Half-edge relations and link with 2-maps

| Half-edge pointer | In 2-maps |
| --- | --- |
| vertex | vertex emb₀(d) |
| face | face emb₂(d) |
| previous half-edge | β₀(d) |
| next half-edge | β₁(d) |
| opposite half-edge | β₂(d) |

### 9.2.2 Half-edge

One problem related to the winged-edge data structure is the fact that pointers between edges correspond to adjacency relations between edges according to some vertex (or face). A simple way to illustrate this problem is to consider a subdivision of an orientable surface without boundary in which an edge e is a loop: so, vertex1(e) = vertex2(e). The traversal of the incident cells in a coherent way is possible, but it is more complicated for e than for an edge which is incident to two distinct vertices. Since traversals can be complicated, it can be necessary to conceive complex modification operations.

To solve this problem, the winged-edge data structure was modified by splitting each edge in two half-edges. A half-edge is incident to exactly one face and to exactly one vertex: so, no confusion can arise, even when multi-incidence occurs.

This idea is the basis of the definition of the face-edge data structure [214], the half-edge data structure [172], and the DCEL data structure [86] (DCEL, for Doubly Connected Edge List). These three data structures are equivalent, the only difference being the names of the relations between the half-edges (e.g. opposite is called sometimes twin or pair, previous is called sometimes prev). This is probably the data structure which is the most used for describing surface meshes with irregular faces. See [140] for a comparison of different versions of half-edges, and for an efficient implementation.

The main element of the half-edge data structure is the half-edge: four pointers associate the half-edge with incident cells: cf. Fig. 9.3.

In addition to the list of half-edges, there is also a list of vertices and a list of faces. Each vertex and each face is associated with some information, and a pointer links it to one of its incident half-edges.

Half-edge data structures allow to represent oriented 2D manifolds without boundary. They are directly equivalent to 2-maps without boundary: for instance, half-edges correspond to darts (see Table 9.2). The two lists of vertices and faces exist also in 2-map data structures, when 0- and 2-embeddings are defined.

Figure 9.3(a) shows a half-edge data structure which represents the 2D object depicted in Fig. 3.4(a) page 56. Half-edges are numbered from 1 to 18. For example, previous(4) = 1, next(4) = 3, opposite(4) = 9, vertex(4) = v1 and face(4) = f2.
