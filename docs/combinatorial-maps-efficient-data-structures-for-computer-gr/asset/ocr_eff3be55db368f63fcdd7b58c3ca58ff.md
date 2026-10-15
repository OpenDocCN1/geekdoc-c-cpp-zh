two faces by sticking two edges of their boundaries. Once glued, the two edges are *identified* into one edge (cf. Fig. 2.8).

![](bbox=[0.1, 0.18, 0.92, 0.38])

# FIGURE 2.9

Forbidden identifications ((a) of vertices, (b) of edges), since the resulting objects are not surfaces.

It is forbidden to glue two faces by simply identifying two vertices; it is also forbidden to glue more than two edges: in both cases, the result is not a surface (cf. Fig. 2.9).

So a paper surface can be made of a single face, or by many faces glued by identifying several pairs of edges. It is thus *subdivided* (i.e. partitioned) into vertices, edges and faces.

# *Incidence and adjacency relations*

The “boundary” relation corresponds to the *incidence* relation: more precisely, an edge (resp. a vertex) which belongs to the boundary of a face is incident to the face, and conversely, the face is incident to the edge (resp. to the vertex). Moreover, if a vertex is part of the boundary of an edge (i.e. the vertex meets the edge), the vertex and the edge are incident to each other. Usually, adjacency is defined in the following way: two *i*-cells are *adjacent* if they share a common cell in their boundaries. For instance, two faces (resp. two edges) are adjacent if they share an edge or a vertex (resp. a vertex). Adjacency is sometimes defined in a generalized way: two cells are adjacent if they are incident to the same cell: for instance, two vertices are adjacent if they are incident to the same edge or to the same face.

# *Surface boundary*

A *free* edge is incident to a single face; it is *sewn*² when it is incident to two faces. The *boundaries* of a subdivided surface are made by the free edges: moreover, they are *cycles* of free edges. When a surface has no free edge, it is *without boundary*, for instance the surface of a cube, made by gluing six square

²The use of the word “sew” comes from the fact that, for constructing paper surfaces, instead of gluing faces by sticking two edges into one edge, it is also possible to sew the faces together around the resulting edge.