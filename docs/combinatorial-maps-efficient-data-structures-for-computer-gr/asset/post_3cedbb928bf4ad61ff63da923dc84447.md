
*cells*. For instance, the rounding operation can be applied to vertices and edges (cf. Fig. 1.4). It consists in:

- first applying *chamfering*: cf. Fig. 1.4(a) and Fig. 1.4(b). This is a structural operation, which consists in “expanding” vertices and edges into faces, the structure of the face depending on the structure of the replaced vertex or edge. For instance, a vertex incident to three edges is basically replaced with a triangular face;
- then computing surface patches, which are associated with the chamfered cells: cf. Fig. 1.4(c).

**FIGURE 1.4** Chamfering and rounding vertices and edges. (a) A cube. (b) Edges e1, e2 and vertex v are chamfered. (c) Rounding, by associating surface patches with chamfered cells (e1, e2, v and other cells have been chamfered).

![](img/6ba3cf72cbe3568e76a174448323bb33_30_0.png)

The *structural relations* between cells are also useful or necessary for many *global* operations. For instance, when simulating a traversal of a building, the adjacency relations between the represented rooms make it possible to control the traversal: obviously, it is not possible, when exiting a room, to enter a nonadjacent room.

Subdividing a geometric object corresponds in some way to discretize it, and discretizing a geometric object can be necessary or useful for many processes, for instance:

- simulating some phenomena sometimes involves solving partial differential equations, for instance simulating fluid flow in geological layers, heat in buildings, etc. Often (cf. finite element method, finite difference method, finite volume method), this requires to discretize the object or the part of geometric space containing the object², i.e. to compute a mesh with regular cells (simplices, cubes);
- many processes in computer graphics or in computational geometry handle geometric objects as triangular meshes, since many computations can be efficiently designed for triangles, e.g. computing the intersection of a light ray and a triangle for image synthesis purposes.

## 1.3 Numerous Structures

Numerous data structures have been conceived in order to represent subdivisions: cf. chapter 9. In fact, according to the *structural properties* of the subdivisions, *optimized data structures* can be conceived. For instance, it is possible to represent the structure of any wire mesh with a graph. If the wire mesh corresponds to a *curve*, i.e. at most two edges are incident to one vertex, its structure can be represented by a list. This can be generalized for higher dimensional geometric objects.

So, these numerous data structures can be classified according to:

- the local structural properties, i.e. the structural properties of cells. For instance, several simplicial structures have been defined in order to represent triangulations (for any dimension): cells are vertices, edges, triangles, tetrahedra, etc. Such structures can be generalized for other regular cells, for instance cubical structures (cells are vertices, edges, squares, cubes, hypercubes, etc.), simploidal structures (cells are products of simplices, as cubes are products of edges). Cellular structures have been defined for representing subdivisions with any cells: in fact, cells are never “any” cells, they always satisfy some structural properties.

- the global structural properties, related to the way cells are assembled together. For instance, a subdivision can always be constructed by taking cells and gluing them along cells of their boundaries, i.e. by identifying cells of their boundaries. Constraints can be added. For instance, multi-incidence can be allowed or not, i.e. it is possible, or not, to identify cells which belong to the boundary of the same cell (e.g. a loop is created when two vertices incident to the same edge are identified). Another example is the following. Many structures have been defined for representing generalizations of surfaces, i.e. n-dimensional objects which can be constructed by taking n-dimensional cells, and gluing them by identifying (n − 1)-dimensional cells, in such a way that at most two n-cells are incident to a (n − 1)-cell. Many structures have also been defined for representing a subclass of these generalizations of surfaces, i.e. for such orientable objects without boundaries, etc.

### 1.3.1 Why Numerous Structures?

In fact, there are two questions:

1. *why assuming that objects satisfy some properties?* Mainly for:

   - *coherence of representation.* Representing a volume by its boundary is a well-known method of Geometric Modeling, applied for instance for CAD applications. For instance, take a simple object of our real world, e.g. a wooden cube; it corresponds to a volume, and its boundary is an orientable surface without boundary, made of six faces, twelve edges and eight vertices. But a nonorientable surface does not define the boundary of a volume in the 3-dimensional space. So, when the data structure takes into account that only orientable surfaces without boundaries can be represented, it is impossible to construct an object which cannot be represented in the usual 3-dimensional space;

   - *optimization of operations.* For instance, objects are generally triangulable, and triangulations are well suited for many operations of computer graphics or computational geometry, e.g. as said above, it is easy to detect (and compute) the intersection between a light ray and a triangle;

   - *but it is not always possible to assume that objects still satisfy properties.* Other operations are not so easy to perform on triangulations, for instance boolean operations (union, intersection, difference). Such operations, applied to triangulations, do not directly produce triangulations (cf. Fig. 1.5(a)). A first idea consists in splitting simplices when intersections are processed (cf. Fig. 1.5(b)), but examples exist, showing that the process may be not convergent, since new simplices are added which perhaps produce new intersections; so, it could be convenient here to handle cellular structures instead of simplicial ones;

**FIGURE 1.5** Boolean operations and simplicial objects. (a) The intersection of two simplicial objects is not a simplicial one. (b) Simplex splitting generates new intersections.

![](img/6ba3cf72cbe3568e76a174448323bb33_32_0.png)

   - *and don’t forget some additional costs.* As said before, it could be efficient to handle triangulations, and thus to triangulate cellular objects; but if some operations are more efficient when applied to a triangular cell, there are more triangular cells than initial ones, so more cells to process. Moreover, information can be lost (or explicit information can become implicit). For instance, assume that the initial structure has a meaning related to the application, e.g. wooden cubes are represented. When triangulated, several triangles correspond to each initial square face: either the information is lost, or it is necessary to compute this information when needed (for instance here by computing the triangles which are coplanar).

2. *why not a general structure?* Everybody knows the answer, which stands for any data structures:

   - *optimization of the representation.* The example given above about the representations of wire meshes or wire curves (graphs or lists) can be generalized for any dimension, and thus for all data structures conceived for representing subdivisions. In other words, many structural properties can lead to optimize the representation, by making implicit some information.

   - *which can lead to optimize the operations.* Remember that volumes sometimes are represented by their boundaries, which are orientable surfaces without boundary. Intuitively, such a surface has two sides, one directed towards the inside, the other side directed towards the outside. Assume each side corresponds to a given color (e.g. black for inside, white for outside). The surface can be constructed by taking faces having their two sides colored, one black and the other white, and by identifying edges in such a way that adjacent faces are colored coherently, i.e. each side of the surface has one color. Data structures exist, which implement orientable surfaces: so, when identifying edges, there is no choice, faces are glued coherently. If the data structure does not take orientation into account, it is necessary to check how the faces are glued in order to do that in a coherent way; thus the cost of the operation for the general structure is higher than with a specialized structure;

   - *or not.* Optimizing the data structure means that no information is lost; but often, some explicit information within the general structure becomes implicit within the optimized structure. When the information is needed for some operations, it has to be computed, leading to an additional cost.
