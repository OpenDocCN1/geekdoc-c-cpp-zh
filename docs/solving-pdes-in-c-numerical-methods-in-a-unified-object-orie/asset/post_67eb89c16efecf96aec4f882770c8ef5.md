
Thus, it has to be refined not only in the sense of dividing the existing triangles but also in the sense of adding more triangles next to the circular boundary.

This is indeed done in the finer mesh in Figure 14.9. For simplicity, this mesh is produced under the assumption that the coarse numerical solution changes significantly only between the points nI and nJ in Figure 14.8, so a midpoint nIJ must be added between them. This implies that the upper-right triangle in Figure 14.8 should be divided into two smaller triangles, as is indeed done in Figure 14.9. However, this is not the end of the story: two extra triangles are also added between the edge leading from nI to nJ and the circular boundary. This way, the approximation improves not only in the interior of the domain but also at its boundary.

## 14.8 Implementation of Automatic Boundary Refinement

Let us show how easy it is to implement automatic boundary refinement in the present framework. Indeed, all that has to be done is to modify the "refineNeighbor()" function in Section 14.5. This function refines the neighbor (edge-sharing) triangle of a refined triangle. But what if there is no neighbor triangle? This implies that the edge under consideration must be a boundary edge, namely, an edge that lies next to the boundary. Automatic boundary refinement requires that two extra triangles should then be added between it and the curved boundary.

Thus, one only needs to detect the boundary edges and add two small triangles between them and the curved boundary. Fortunately, this is easy enough. Recall that the "refineNeighbor()" function in Section 14.5 contains a recursive call in its final "else" question. This recursive call is used only if no neighbor triangle has yet been found, and the search must therefore continue among the rest of the triangles in the mesh. If the entire linked list of triangles has been scanned and no neighbor has been found, then the edge must be a boundary edge.

The end of the linked list of triangles is reached when the "next" field is equal to 0. This indicates that the edge leading from nI to nJ is indeed a boundary edge, so two extra triangles should be added between it and the boundary.

Automatic boundary refinement is thus implemented simply by modifying the final "else" question in the "refineNeighbor()" function to read as follows:

```
else{
    if(next)
        ((mesh<triangle>*)next)->refineNeighbor(nI,nJ,nIJ);
    else{
        node<point>
            newNode((1./sqrt(squaredNorm(nIJ()))) * nIJ());
        triangle t1(nI,nIJ,newNode);
        triangle t2(nJ,nIJ,t1(2));
        insertNextItem(t2);
        insertNextItem(t1);
    }
}
```

The interior "else" block in this code considers the case in which no neighbor triangle exists in the entire mesh, which implies that the edge leading from nI to nJ is indeed a boundary edge. In this case, two extra triangles, named "t1" and "t2", are added between it and the circular boundary.

In the above, we assume that the domain is circular, so the above procedure should take place in every boundary edge. The extension to other convex domains is straightforward. In more general domains, a boundary edge does not necessarily lie next to a convex boundary segment. One should thus check whether the midpoint between nI and nJ indeed lies within the domain before applying the above procedure. This is discussed and illustrated next.

## 14.9 Nonconvex Domains

As we have seen above, levels of refinement are useful in refining further not only in the interior of the domain but also next to a curved boundary like that in Chapter 12, Section 9. This is done by adding smaller and smaller triangles to the inside of the circle.

This procedure can be employed not only in a circle but also in more complicated domains with curved boundaries, provided that they are convex. For nonconvex domains, the curved boundary must be approached from the outside in.

![](img/1f293b0ceb2de964310ea7f941a1b580_420_0.png)

Figure 14.10. The nonconvex domain in which the PDE is defined.

Consider, for example, the domain in Figure 14.10. The left edge in it is concave, so it cannot be approximated from the inside out, as before. Instead, it is approached from the outside in, as follows.

Assume that the initial (coarse) mesh is as in Figure 14.11. This mesh contains only three triangles, and the left, curved edge is approximated rather poorly. In order to improve the approximation, we proceed in the same spirit as in adaptive refinement.

In adaptive refinement, the midpoint between node 1 and node 2 in Figure 14.11 is connected to node 4 to divide the upper triangle into two smaller triangles. Here, however, this midpoint lies outside the domain; therefore, it is replaced by the nearest point across from it on the curved boundary. This point is then connected to nodes 1, 2, and 4 to form the required two smaller triangles instead of the original upper triangle. The same is done for the lower coarse triangle in Figure 14.11. The resulting fine mesh is displayed in Figure 14.12.

![](img/1f293b0ceb2de964310ea7f941a1b580_421_0.png)

Figure 14.11. The original coarse mesh that gives a poor approximation to the nonconvex domain.

![](img/1f293b0ceb2de964310ea7f941a1b580_421_1.png)

Figure 14.12. The refined mesh that gives a better approximation to the nonconvex domain.

The above procedure may be repeated, yielding better and better approximations to the curved boundary on the left. Better yet, it can be combined with adaptive refinement to produce an improved algorithm that refines simultaneously in both the interior of the domain and on its boundary:

### Algorithm 14.2.

- 1. Let T be the initial coarse finite-element triangulation, that is, the set of triangles in the mesh.
- 2. Construct the stiffness matrix A and the right-hand side f corresponding to T.
- 3. Solve the stiffness system

\[
Ax=f
\]

for the vector of unknowns $x$.
- 4. Let $E$ be the set of edges in $T$.
- 5. Scan the edges in $E$ one by one in some order. For every edge $e$ encountered in this scanning, do the following:
  - (a) Denote the endpoints of $e$ by $i$ and $j$ (see Figure 14.5).
  - (b) If $e$ lies in the interior of the domain, then there are two triangles that share it. If $e$ lies next to the boundary (e is “boundary edge”), then there is only one triangle that uses it. Let

  \[
  t=\Delta(i,j,k)
  \]

  be a triangle with vertices $i$, $j$, and $k$ that uses $e$ (Figure 14.5).
  - (c) Let $m=(i+j)/2$ be the midpoint between $i$ and $j$.
  - (d) If $e$ is a boundary edge, then $m$ can lie outside the domain and must be replaced by a boundary point that is nearest to it in some sense. This is done as follows: let $l$ be the point on the line leading from $k$ to $m$ that also lies on the boundary, and substitute

  \[
  m\leftarrow l.
  \]

  This guarantees that $m$ lies either on the boundary or in the interior of the domain.
  - (e) If

  \[
  |x_i-x_j|>\text{threshold},
  \]

  then divide $t$ into the two triangles

  \[
  t_1=\Delta(i,m,k),
  \qquad
  t_2=\Delta(j,m,k).
  \]

  (Figure 14.6). In other words, include $t_1$ and $t_2$ in $T$ instead of $t$.
  - (f) Do the same to the other triangle that shares $e$, if it exists. If $e$ is a boundary edge, then no such triangle exists. Still, if $m$ lies in the interior of the domain, then we need to add two more triangles next to the boundary. This is done as follows: extend the line leading from $k$ to $m$ until it meets the boundary at a point denoted by $l$. Add to $T$ the triangles

  \[
  t_3=\Delta(i,m,l),
  \qquad t_4=\Delta(j,m,l).
  \]

- 6. If the mesh is not yet sufficiently fine, then go back to step 2.
- 7. Use $x$ as the numerical solution of the boundary-value problem on the final mesh $T$.

## 14.10 Exercises

- 1. Implement the adaptive-refinement algorithm in Section 14.3 using the "refine" function. (You may assume that a function "solve" that solves the stiffness system at the current mesh is available.) The solution can be found in Section A.21 of the Appendix.
- 2. Modify the "refine" function so that every edge is refined, regardless of the numerical solution (global refinement). This can actually be done by choosing a zero threshold in the adaptive-refinement algorithm.
- 3. Assume that the domain is circular. Modify the "refine" function so that the boundary edges are always refined.
- 4. Use graphic software (or LaTeX) to print the meshes resulting from the adaptive-refinement algorithm. Verify that the meshes are indeed conformal.
- 5. Currently, the "refine" function uses an internal loop with index 'j' that decreases from 2 to 'i'+1, where 'i' = 0,1,2 scans the list of vertices in the current triangle. Modify this loop so that 'j' increases from 'i'+1 to 2. What is the effect of this change on the refinement?
