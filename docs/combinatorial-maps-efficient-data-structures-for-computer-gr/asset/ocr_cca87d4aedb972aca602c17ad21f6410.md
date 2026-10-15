![](bbox=[0.111, 0.094, 0.861, 0.337])

**FIGURE 3.11**  
Examples of cells in a 3-map.  
(a) Face containing dart 18.  
(b) Edge containing dart 18.  
(c) Vertex containing dart 18.

quasi-manifolds with boundaries. The principle is similar, i.e. cells are progressively decomposed by decreasing dimensions, the only difference being that *i*-cells that belong to a boundary are not split, because these cells belong to the boundary of only one (*i* + 1)-cell.

# 3.1.2.1  1D

In 1D, an oriented quasi-manifold with boundary is an open oriented polygonal curve. In the example depicted in Fig. 3.12(a), the object is composed by four edges (labeled from *e*₁ to *e*₄) and five vertices (labeled from *v*₁ to *v*₅). The curve is decomposed into edges by splitting each vertex in two, except vertices that belong to a boundary (vertex *v*₁ and *v*₅ in this example). Indeed, such a vertex belongs to the boundary of only one edge and thus does not need to be split. As before, a dart represents an oriented edge and its origin vertex. Thus, four darts exist, corresponding to (*v*₁, *e*₁), (*v*₂, *e*₂), (*v*₃, *e*₃) and (*v*₄, *e*₄). *v*₅ is not explicitly represented in this case¹.

The dart describing a nonsplit vertex has no dart before it in the oriented

> ¹ This is generally not a problem because this case does not occur in practice. Moreover, if needed, this case can be considered specifically to retrieve the missing vertex. Indeed, a dart corresponds to an oriented edge; it is thus possible to explain all notions by associating an oriented edge and its two incident vertices with a dart. We chose to describe all notions related to *n*-maps by associating an oriented edge and its origin vertex with a dart in order to simplify several explanations.