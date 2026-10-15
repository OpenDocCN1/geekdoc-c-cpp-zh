not possible to check a cellular structure in order to know if (a subpart of) it corresponds to a ball: so, given a cellular structure, it is not even possible to decide whether a CW-complex can be directly associated with it.

+   - CW-complexes exist, which cannot be triangulated. But all cellular structures (as n-Gmaps or incidence graphs) have a simplicial analog. That means that only triangulable objects are taken into account by these cellular structures. This corresponds to the fact that these cellular structures are combinatorial structures (defined by a set of discrete objects on which discrete applications act), and that only simplicial objects (and objects derived from simplicial ones) have a combinatorial characterization (cf. Section 8.1.1 and Section 8.1.2).

The intuitive idea of simplicial analogs is related to the classical notion of barycentric triangulation. Let O be a k-dimensional “subdivided object” in ℝⁿ, such that all its cells are convex ones (as a consequence, any cell is homeomorphic to a ball). The barycentric triangulation of O is constructed incrementally in the following way (cf. Fig. 8.1):

+   - “triangulate” all vertices: it simply consists in replacing all vertices of O by vertices numbered 0 (note that 0 is the dimension of the vertices);
+   - triangulate all edges. Given an edge, it consists in adding a new vertex numbered 1 at the barycenter of the edge (1 being the dimension of the edge), and in replacing the edge by its triangulation related to this new vertex, i.e. by two edges both incident to this new vertex and to an extremity of the initial edge;
+   - triangulate all faces. Given a face, it consists in adding a new vertex numbered 2 at the barycenter of the face (2 being the dimension of the face), and in replacing the face by its triangulation related to this new vertex, i.e. by a set of triangles, each incident to a vertex numbered 0, to a vertex numbered 1 and to a vertex numbered 2;
+   - iterate this process for all i-cells, for i increasing from 3 to k; the last triangulation produces the barycentric triangulation of O.

Note that any main i-dimensional simplex of the barycentric triangulation (i.e. a simplex which is not incident to a higher-dimensional simplex) is incident to i + 1 vertices, numbered from 0 to i. More generally:

+   - there is a bijection between initial i-dimensional cells and vertices numbered i;
+   - the interior of any initial i-dimensional cell corresponds to the associated vertex numbered i, and all j-dimensional simplices (1 ≤ j ≤ i) which are incident to this vertex and such that their incident vertices are numbered by integers lower than or equal to i.