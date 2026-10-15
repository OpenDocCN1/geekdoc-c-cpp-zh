
**Algorithm 66:** `triangulationNGMap(gm,d,i)`: triangulation of an *i*-cell for *n*-Gmaps

**Input:** `gm`: an *n*-Gmap;  
`d ∈ gm.Darts`: a dart;  
`i ∈ {1, ..., n}`.

**Result:** Make a triangulation of the *i*-cell `cᵢ(d)`.

**Output:** A dart of the new vertex.

```text
1  phi ← an array of i + 1 empty associative arrays between darts;
2  foreach dart d′ ∈ cᵢ(d) do
3      for j ← 0 to i − 1 do
4          phi[j][d′] ← createDartNGMap(gm);
5      phi[i][d′] ← d′;
6  foreach dart d′ ∈ cᵢ(d) do
7      phi[0][d′].Alphas[0] ← phi[1][d′];
8      for j ← 1 to i do
9          phi[0][d′].Alphas[j] ← phi[0][d′.Alphas[j − 1]];
10     for j ← i + 1 to n do
11         phi[0][d′].Alphas[j] ← phi[0][d′.Alphas[j]];
12     for k ← 1 to i − 1 do
13         for j ← 0 to k − 2 do
14             phi[k][d′].Alphas[j] ← phi[k][d′.Alphas[j]];
15         phi[k][d′].Alphas[k − 1] ← phi[k − 1][d′];
16         phi[k][d′].Alphas[k] ← phi[k + 1][d′];
17         for j ← k + 1 to i do
18             phi[k][d′].Alphas[j] ← phi[k][d′.Alphas[j − 1]];
19         for j ← i + 1 to n do
20             phi[k][d′].Alphas[j] ← phi[k][d′.Alphas[j]];
21 foreach dart d′ ∈ cᵢ(d) do
22     d′.Alphas[i − 1] ← phi[i − 1][d′];
23 return phi[0][d];
```

![](img/6ba3cf72cbe3568e76a174448323bb33_271_0.png)

**FIGURE 6.53**  
(a) A 2D object.  
(b) The result of the 1-triangulation operation applied to the edges of (a).  
(c) The result of the 2-triangulation operation applied to the faces of (b). This is the barycentric triangulation of the initial object.

As for the chamfering operation, the αᵢ₋₁ links are modified for the darts in cᵢ(d) (line 22). To avoid side effects, this modification is done in a second loop, after having defined the α links for the new darts. Moreover, the darts of cᵢ(d) are stored in a data structure during the first loop (line 2); the iteration of the second loop is done through the data structure, and not through a cell iterator (line 21). At last, the algorithm returns one dart belonging to the new vertex, as it can be used in other algorithms (as we will see in Algorithm 74 page 265).

The complexity of Algorithm 66 is linear in the number of darts #d of the given i-cell times log #d.

The *barycentric triangulation* of a given n-Gmap can be defined by applying the i-triangulation operation to the i-cells of the n-Gmap, from i = 1 to i = n. For example, look at the 2D object represented in Fig. 6.53(a). It contains 12 vertices, 17 edges and 6 faces. The 1-triangulation operation is applied to all its edges, producing the 2D object represented in Fig. 6.53(b). This object contains 29 vertices, 34 edges and 6 faces. Then, the 2-triangulation operation is applied to all its faces, producing the 2D object represented in Fig. 6.53(c). This object contains 35 vertices, 84 edges and 50 faces. This is the barycentric triangulation of the initial object: a vertex corresponds to each cell of the initial object.

![](img/6ba3cf72cbe3568e76a174448323bb33_274_0.png)

# **FIGURE 7.1**

Example of embedding of a 2-map in \(\mathbb{R}^2\). Embedding of vertices is represented by dashed lines, embedding of edges is represented by lines and embedding of faces is not represented.

embedding of \(M\) has the same structure than \(M\). Note that the mechanisms explained here are valid for both \(n\)-maps and \(n\)-Gmaps. A classical way consists in embedding an \(n\)-map in the Euclidean space \(\mathbb{R}^d\). Note that the dimension \(n\) of the \(n\)-map is not necessarily equal to \(d\), the dimension of the Euclidean space. \(n\) will be referred to as the *combinatorial dimension*, and \(d\) will be referred to as the *ambient dimension*.

A 2-map embedded into \(\mathbb{R}^2\) is represented in Fig. 7.1. Each vertex of the 2-map is associated with a point in \(\mathbb{R}^2\) (for example vertex \(\{1,6\}\) is associated with point \((0,2)\) and vertex \(\{7\}\) is associated with point \((1,3)\)); each edge is associated with an open segment (for example edge \(\{6\}\) is associated with segment \(](0,2),(1,3)[\) and edge \(\{1,5\}\) is associated with segment \(](0,2),(2,2)[\)); each face is associated with an open surface area (face \(\{5,6,7\}\) is associated with the surface area defined by \(\{(x,y) \in \mathbb{R}^2|y > 2 \text{ and } y < x-2 \text{ and } y < -x+4\}\) and face \(\{1,2,3,4\}\) is associated with the surface area defined by \(\{(x,y) \in \mathbb{R}^2|x > 0 \text{ and } x < 2 \text{ and } y > 0 \text{ and } y < 2\}\)).

We can verify that this example is a correct embedding by checking that two incident cells in the 2-map are associated with two incident elements of the plane and reciprocally. For example vertex \(\{1,6\}\) associated with point \((0,2)\) is incident to edge \(\{1,5\}\) associated with segment \(](0,2),(2,2)[\) and point \((0,2)\) belongs to the boundary of the segment.

This 2-map is “linearly embedded” into \(\mathbb{R}^2\): vertices are associated with points, edges are associated with segments and faces are associated with poly-

![](img/6ba3cf72cbe3568e76a174448323bb33_275_0.png)

# FIGURE 7.2

Embedding a 2-map in ℝ²: edges and faces are implicitely embedded.

gons. More generally, a linear embedding consists in associating a part of an iD hyperplane with each i-cell. This type of embedding is often used because it is simple to handle. However many other types of embedding exist. For example splines can be used to embed edges or nurbs surfaces to embed faces. However even in these cases, the embedding still consists in associating iD geometrical elements to i-cells, and constraints related to the incidence between the cells still have to be satisfied. The choice of a given embedding will depend on the specific needs of the applications.

Note that it can be avoided to explicitly describe all the geometrical objects, when some of them can be computed using the embedding of other cells and the incidence relations in n-maps. This is for example the case for the linear embedding presented above, explained here for n = 2 in order to simplify. In this case, the embedding of any edge is the open segment which extremities are the two points associated with the two vertices incident to the edge. Thus it is not necessary to explicitly associate open segments with edges as they can be retrieved from the 0-embedding. Similarly, the embedding of any face is a part of a plane which boundary contains all segments associated with the incident edges. Thus it is also not necessary to explicitly describe this 2-embedding as it can be retrieved thanks to the 1-embeddings. So it is possible to only associate points with vertices in order to linearly embed a 2-map (cf. Fig. 7.2). This is usually the way linear embeddings are defined, for any n. Note that consistency constraints still have to be satisfied: for instance, the points associated with two vertices incident to the same edge have to define a line segment, i.e. they must be different; the points associated with the vertices incident to a face have to be coplanar, otherwise the shape of the face is not defined; etc.

Conversely, a dual approach can be followed, explained here for linear embedding and n = 2 in order to simplify; but in fact, it is usually applied for nonlinear embedding (e.g. trimmed surfaces: cf [2]). Associate a plane of ℝ³ with any face. The plane is the support space of the face. The surfaces associated with two adjacent faces which share an edge intersect along a line: this line is the support space of the common edge. All lines associated with the edges which share a vertex intersect on a point, which is the embedding of the vertex. The line segment associated with an edge is defined by its support line, delimited by the points associated with its incident vertices. Similarly, the part of plane associated with a face can be retrieved from its support plane, and the lines associated with its incident edges. In fact, all embedding information can be retrieved from the support spaces associated with the faces, since the embedding of other cells can be deduced. Here also, consistency constraints still have to be satisfied: for instance, the planes associated with two edges which share an edge have to be different. This approach can be generalized for higher dimensions, and also for nonlinear embedding. For instance, support spaces associated with faces are often free-form surfaces (e.g. nurbs).

The main interests of implicit embedding are:

+   1. decrease the memory size: there are less geometrical elements to store and less links to describe;
+   2. simplify the operations: only one type of embedding is handled;
+   3. increase the guaranty of validity: some validity constraints of some cell embedding can be implied by the use of the embedding of incident cells.

As a main drawback, there is an additional cost since it can be necessary to explicitly compute (information about) the different implicit embeddings; but generally this cost is small.

There are several possibilities for associating an embedding with an i-cell. However as cells are set of darts, this association is always done through darts. For example a pointer can be added to each dart, that points to the embedding of the i-cell containing the dart. This solution allows a direct access to all embeddings. However it requires to update the pointers of all darts of the i-cell to initialize its embedding. Moreover, there is one pointer for each dart and for each dimension i having an embedding. It is also possible to create an associative array that links each dart of an i-cell with its corresponding embedding. This allows to add or remove a certain embedding without modifying the dart data structure. Moreover if a hash-table is used, the access to the embedding of a dart can be done in constant time in average. As a last example, it is possible to link only one dart per i-cell with the corresponding i-embedding. Some memory space is saved since describing less relations are described; moreover this can speed up some operations modifying the links between darts and embedding, since there is only one dart to modify. However,
