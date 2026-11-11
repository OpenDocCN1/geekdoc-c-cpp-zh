zero-level set for the function whose values we know at the grid points, as shown in Figure 25.23.

In doing so, however, we are ignoring additional data: At each estimated zero point, we can also make an estimate of the gradient of the function (see Figure 25.24) (or perhaps get the gradient directly as part of gathering the original data) and use these in estimating the shape of the level set.

This can be called an “Hermite” version (see Chapter 22) of marching squares. The **extended marching cubes algorithm** [KBSS01] uses this Hermite data to determine how the interior of a square appears: If the normals for the data in a square are similar, the algorithm defaults to standard marching squares. But if the point-normal pairs for a square (say (X₁, n₁) and (X₂, n₂)) are inconsistent (if n₁ and n₂ are not nearly parallel enough), then the square is treated differently: A new vertex, X, is placed in the square in such a way that it minimizes a **quadratic error function**,

X = arg min_X Σ_i ((X − X_i) · n_i)², (25.9)

as shown in Figure 25.25; in other words, X seeks to lie on the lines determined both by (X₁, n₁) and (X₂, n₂). (In 2D, this is trivial; in 3D, where there may be more contributing point-normal pairs, the minimization can be more complicated.) The newly inserted point is connected (with a pair of edges in 2D, or with a triangle fan based at X in 3D) to the zero-set on the boundary of the grid cell.

There are two small problems.

+   1. If the normal vectors are sufficiently antiparallel, it’s possible that the minimizer X lies outside the square, and X must be adjusted to lie within it.
+   2. In the 3D case, if there are “extra points” X₁ and X₂ in two adjacent cells, we perform an edge flip on the contour edge that lies in the grid face between the two cells so that this grid edge now goes from X₁ to X₂.

> **Inline Exercise 25.8:** ◆ Argue that the “bad minimizer” problem above is the result of *aliasing*. What sampling is going on? Where are the too-high frequencies?

In estimating (at least in special cases) a surface point in the interior of a cell, the extended marching cubes algorithm suggests a different approach: If we had a surface point in adjacent cells, we could join these with edges (and faces, in 3D), using the points on grid edges as guides. Such an approach is called **dual contouring**; Ju et al. [JLSW02] developed a scheme for dual contouring of Hermite data, which involves two steps.

+   1. For each cell with differently signed vertices (i.e., not all positive or all negative), generate a mesh vertex within the cell by minimizing a quadratic error function.
+   2. For each edge with differently signed vertices, generate an edge (for 2D) or a quad (for 3D) connecting the minimizing vertices in the adjacent cells.

This algorithm has the pleasant characteristic that all cells are treated identically—there’s no threshold on when “normal vectors are close enough”—but there are subtleties: Again, the minimizing point for a quadratic error function

![](bbox=[0.71, 0.07, 0.93, 0.294])

![](bbox=[0.71, 0.319, 0.93, 0.538])

![](bbox=[0.71, 0.553, 0.93, 0.762])