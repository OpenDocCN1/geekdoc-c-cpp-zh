# FIGURE 8.14

(a) Two corners of face f1, namely (e1, v1, e6) and (e3, v1, e4) share vertex v1: face f1 is adjacent to itself through this vertex.

(b) A surface subdivision in which face f1 is incident twice to edge e2.

(c) The corresponding incidence graph.

We claimed that such incidence graphs cannot take multi-incidence into account, but it seems possible to deduce incidence graphs from subdivisions in which multi-incidence occurs: cf. Fig. 8.14. It is thus necessary to precisely define the geometric objects which can be unambiguously associated with such incidence graphs.

The key notion here is the notion of cell-tuple [39]. Let ci be a main i-cell, i.e. a cell which is not the extremity of an edge in the incidence graph: for instance, f1, f2, e7, e8 in Fig. 8.13 are main cells. Let (c0, …, ci) be a sequence of cells, such that:

+   - for any j, 0 ≤ j ≤ i, cj is a j-cell;
+   - for any j, 0 ≤ j < i, there is an edge between cj+1 and cj.

Associate now an i-simplex {c0, …, ci} with (c0, …, ci); if you generalize this process for all main cells, you get the main simplices of an abstract simplicial complex. Moreover, this abstract simplicial complex can be numbered, by associating its dimension with each vertex of the complex, since any vertex of the complex corresponds to a cell of the incidence graph: cf. Fig. 8.15.

Look now at Fig. 8.15(b), in which is depicted the cellular quasi-manifold corresponding to Fig. 8.14(b). This cellular quasi-manifold corresponds to a 2-Gmap, but it is not an abstract simplicial complex: several edges share the same boundaries; for instance there are two edges incident to vertices corresponding to v2 and f1: so, it is not possible to associate an incidence graph with the subdivision depicted on Fig. 8.14(b).

Look now at the incidence graph depicted on Fig. 8.14(c): this incidence graph does not describe the topology of the surface depicted on Fig. 8.14(b). If you construct the associated abstract simplicial complex, you will see that

![](bbox=[0.08, 0.12, 0.9, 0.41])