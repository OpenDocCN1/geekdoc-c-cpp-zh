
The “boundary” relation corresponds to the *incidence* relation: more precisely, an edge (resp. a vertex) which belongs to the boundary of a face is incident to the face, and conversely, the face is incident to the edge (resp. to the vertex). Moreover, if a vertex is part of the boundary of an edge (i.e. the vertex meets the edge), the vertex and the edge are incident to each other. Usually, adjacency is defined in the following way: two `i`-cells are *adjacent* if they share a common cell in their boundaries. For instance, two faces (resp. two edges) are adjacent if they share an edge or a vertex (resp. a vertex). Adjacency is sometimes defined in a generalized way: two cells are adjacent if they are incident to the same cell: for instance, two vertices are adjacent if they are incident to the same edge or to the same face.

### Surface boundary

A *free* edge is incident to a single face; it is *sewn*² when it is incident to two faces. The *boundaries* of a subdivided surface are made by the free edges: moreover, they are *cycles* of free edges. When a surface has no free edge, it is *without boundary*, for instance the surface of a cube, made by gluing six square faces: the initial twenty-four edges are identified into the resulting twelve sewn edges of the cube.

²The use of the word “sew” comes from the fact that, for constructing paper surfaces, instead of gluing faces by sticking two edges into one edge, it is also possible to sew the faces together around the resulting edge.

![](img/6ba3cf72cbe3568e76a174448323bb33_47_0.png)

**FIGURE 2.10**

(a) Correct identifications of vertices (for 1-dimensional objects), producing curves.

(b) Forbidden identifications of vertices, which do not produce a curve.

### Unnecessary constraints

In order to simplify the study of surface construction, assume the boundary of any face contains at least three edges and three vertices. Similarly, assume that the boundary of an edge contains at least, and thus exactly, two vertices (in other words, no edge is a loop). Moreover, when two edges are identified, they belong to the boundaries of two distinct faces: in other words, it is forbidden to identify two edges incident to a same face.

In fact, these constraints are added in order to reduce the number of possible configurations obtained when gluing together sheets of paper, but it is still possible to construct any surface, even when these constraints are satisfied. For instance, if it is not possible to construct an annulus by identifying a pair of edges incident to one face, it is possible to construct an annulus by identifying two pairs of edges of two faces! So, with these “unnecessary constraints”, it is not possible to construct any subdivision of any surface, but it is possible to construct subdivisions of any surfaces.

These constraints are very different from the two previous ones, added for constructing only surfaces. This can be observed by considering the following characteristic property of surfaces, informally stated as: any point of any surface, which is not a boundary point, has a neighborhood (i.e. a “part around”) which is homeomorphic to an open 2-dimensional ball³. In particular, this is true for any interior point of any face. More generally:

- when two faces are glued by identifying two free edges, any point of the resulting edge has a neighborhood which is homeomorphic to an open 2-dimensional ball (since this point results from the identification of two distinct boundary points, its neighborhood results from the union of two 2-dimensional half balls which were the neighborhoods of the two initial points);

- on the contrary, when two faces are glued by identifying two vertices, the neighborhood of the resulting vertex is homeomorphic to two 2-dimensional half balls which share a point, i.e. it is not homeomorphic to a 2-dimensional ball;

- similarly, when three (or more) faces are glued by identifying more than two edges, the neighborhood of any point of the resulting edge is not homeomorphic to a 2-dimensional ball. As seen before, this is similar in dimension 1: assume subdivided curves are constructed by welding pieces of wires. A piece of wire makes a curve; when two pieces of wires are welded, they still make a curve; when three pieces of wires are welded at a same point, they do not make a curve... (cf. Fig. 2.10).

### Orientability

The annulus and the Möbius strip (cf. Fig. 2.8) are made similarly (two free edges, which are not adjacent, are identified), but they are clearly different: the annulus has two boundaries, the Möbius strip has only one. Moreover, assume you handle real sheets of paper, and assume the two sides of each sheet of paper have different colours, for instance one side black and the other white: it is possible to get the same colour for each side of the annulus (in fact, the annulus has still two sides), but it is impossible to get the same colour along one side of the Möbius strip, since the Möbius strip has only one side! This well-known difference is related to orientability.

An edge is always orientable (cf. Fig. 2.11(a)): that means it is possible to choose a direction for going along this edge, i.e. an origin vertex and an extremity vertex. Note that any edge can be oriented in two ways, which are opposite (if you have chosen an origin vertex and an extremity vertex, you get the opposite orientation by exchanging the two vertices).

A face is always orientable: that means intuitively that it has two sides, i.e. you can go around all points of the faces by walking and turning always left (or oppositely always right); this corresponds also to the fact that the boundary of the face is a cycle of edges and vertices, which can be oriented into one direction or into the opposite direction (cf. Fig. 2.11(b)). So, orienting a face consists in choosing an orientation of its boundary, and thus each edge of this boundary is itself oriented; but the orientations of the edges are coherent along the boundary of the face.

The idea is quite similar for defining orientable surfaces: all faces are oriented, but in a coherent way, meaning that (cf. Figs. 2.11(c) and (d)):

- any sewn edge is oriented in opposite ways for its two incident faces; this is not intuitive, but this corresponds to the fact that if you have chosen to turn left for instance for one face, when the relative orientations of

  公共边方向相反时，你也选择了对另一个面左转；

- 自由边构成定向边界，即边的定向环。

![](img/6ba3cf72cbe3568e76a174448323bb33_49_0.png)

**图 2.11**  

(a) 一条边及其两个相反的方向。  

(b) 一个面及其两个相反的方向。  

(c) 共享一条边的两个面的相干定向：表面的边界是相干定向的，且公共边相对于其关联的面具有相反的方向。  

(d) 环面（圆环）的相干定向（意味着圆环是可定向的）。  

(e) 不可能定义莫比乌斯带的相干定向（意味着莫比乌斯带是不可定向的）。

当一个表面是可定向的（即可以相干定向）时，可以定义两个相反的方向（例如参见圆环）。当一个表面是不可定向的时，不可能定义相干定向（例如参见图 2.11(e) 中的莫比乌斯带）。

还要注意，当边界是相干定向时，你可以通过沿着它粘合一个具有相同边数且以相干定向方式的面来将其闭合。因此，如果一个带边界的表面是可定向的，你可以将其闭合为没有边界的可定向表面：例如，你可以通过沿其边界粘贴另一个面来闭合一个面；你可以通过沿两个边界粘贴两个面来闭合一个圆环；在两种情况下你都得到一个*拓扑球面*（如果你的纸张是可延展的，你可以修改所得形状以得到一个几何球面）。但如果一个带边界的表面是不可定向的（即不能以上述方式相干定向），那么无论你如何尝试闭合边界，都不可能得到没有边界的可定向表面。

无边界的可定向表面（如球面、环面等）的一个重要性质是它可以*嵌入*到通常的三维空间中（即你可以在该空间中赋予它形状），使得它将其划分为三个部分：“内部”（有界）体积、表面本身以及“外部”（无界）体积。这在 1 维中类似，但这里所有曲线都是可定向的：嵌入到通常的平面中时，任何无边界的曲线都将其划分为三个部分：一个“内部”（有界）面、曲线本身和一个“外部”（无界）面。

## 2.3 纸面分类

### 2.3.1 拓扑曲面

可以与任意纸面 `S` 关联若干个数：

- `b(S)` 是 `S` 的*边界数*；

- `c(S)` 是 `S` 的*欧拉示性数*，定义为：

  `c(S) = v(S) − e(S) + f(S)`

  其中 `v(S)`、`e(S)` 和 `f(S)` 分别是 `S` 的顶点数、边数和面数。

- `q(S)` 是 `S` 的*可定向因子*，定义为：

  `q(S) = { 0 如果 S 是可定向的；1 如果 S 是不可定向的且 (b(S) + q(S)) 为奇数；2 否则。 }`

- `g(S)` 是 `S` 的*亏格*，定义为： `g(S) = 1 − (b(S) + c(S) + q(S))/2.`

例如，图 2.7 中描绘的所有多边形都有一个边界；它们的欧拉示性数等于 1，它们是可定向的，所以其可定向因子等于 0，且其亏格为零。所有多边形都有这些特征（都只有一个边界，它们是可定向的，它们的欧拉示性数等于 1，因为它们有一个面，且顶点数和边数相等），但其他表面也有，例如一个正方形和一个三角形的粘合，或两个正方形的粘合：参见图 2.8(a) 和图 2.11(c)。圆环有两个边界，其欧拉示性数等于 0，它是可定向的，所以其亏格等于 0。莫比乌斯带有一个边界，其欧拉示性数等于 0，它是不可定向的，所以其可定向因子等于 1 且其亏格等于 0。

所有这些数都是整数，且对于任意纸面 `S`，`b(S)`、`q(S)` 和 `g(S)` 都是正数。

拓扑曲面 `TS_{b,q,g}`，其中 `0 ≤ q ≤ 2`，是所有满足 `b(S) = b`、`q(S) = q`、`g(S) = g` 的纸面 `S` 的集合。任意纸面都属于唯一的拓扑曲面 `TS_{b,q,g}`；且任意拓扑曲面都包含
