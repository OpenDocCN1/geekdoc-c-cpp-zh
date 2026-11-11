![](bbox=[0.15, 0.085, 0.62, 0.285])

Figure 9.2: The point $P$ is in the triangle with vertices $v_0$, $v_1$, and $v_2$, where the function has values $f_0$, $f_1$, and $f_2$, respectively. What value should we assign to the point $P$?

This “continuous extension” of $f$ has analogs for other situations. Before we look at those, let’s examine some of the properties. First, the value of the interpolated function at noon or midnight each day ($t_i$) is just $f_i$; it doesn’t depend at all on the values at noon or midnight on the other days. Second, the value at noon on one day influences the shape of the graph only for the 12 hours before and the 12 hours after. Third, the interpolated function is in fact continuous.

Now let’s consider interpolating values given at discrete points on a surface. Since we often use triangle meshes in graphics to represent surfaces, let’s suppose that we have a function whose values are known at the vertices of the mesh; the value at vertex $i$ is $f_i$. How can we “fill in” values at the other points of all the triangles in the mesh?

By analogy, we use barycentric coordinates. Consider a point $P$ in a triangle with vertices $v_0$, $v_1$, and $v_2$ (see Figure 9.2); we can define

$f(P) = c_0 f_0 + c_1 f_1 + c_2 f_2$    (9.7)

where $(c_0, c_1, c_2)$ are the barycentric coordinates of $P$ with respect to $v_0$, $v_1$, and $v_2$.

Once again, the interpolated function has some nice properties. First, the value at the vertex $v_i$ is just $f_i$; the value along the edge from $v_i$ to $v_j$ (assuming they are adjacent) depends only on $f_i$ and $f_j$; thus, for a point $q$ on such an edge, it doesn’t matter which of the two triangles sharing the edge from $v_i$ to $v_j$ is used to compute $f(q)$—the answer will be the same! Second, the value $f_i$ at vertex $v_i$ again influences other values only locally, that is, only on triangles that contain the vertex $v_i$. Third, the interpolated function is in fact continuous.

The remainder of this chapter investigates this idea of interpolating across faces, its relationship to barycentric coordinates, and some applications.

# ## 9.2 Code for Barycentric Interpolation

The discussion so far has been somewhat abstract; we’ll now write some code to implement these ideas. Let’s start with a simple task.

Input:

+   - A triangle mesh in the form of an $n \times 3$ table, `vtable`, of vertices
+   - A $k \times 3$ table, `ftable`, of triangular faces, where each row of `ftable` contains three indices into `vtable`