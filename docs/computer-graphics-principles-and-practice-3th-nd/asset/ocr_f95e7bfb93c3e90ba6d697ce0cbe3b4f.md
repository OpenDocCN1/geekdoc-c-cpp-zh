barycentric coordinates in that triangle and use these to place it in the mesh \(M'\), treating the vertex \(v_s\) as the location for both \(v_s\) and \(v_t\) in \(M'\).

We can now outline almost the entire progressive meshes algorithm (see Listing 25.2).

# Listing 25.2: The core of Hoppe’s progressive meshes algorithm.

```
```text
Input: a mesh M = M^n with n vertices, and a set of points X distributed on M.
Output: A sequence of meshes M^n, M^{n-1}, ..., M^0, where M^k has k vertices, approximating the
        original mesh M.

E ← ∞
for each edge e of M:
    compute the cost of optimal collapse of edge
    insert (edge, cost) into a priority queue, Q
for k = n down to 1:
    extract the lowest-cost edge e from Q
    collapse e in M^k to get M^{k−1}
    for each edge e' that meets e:
        compute a new optimal collapse of e' and its cost
        update the priority of e' in Q to the new cost
```
```

One final detail remains: the spring constant, \(\kappa\). Hoppe defines the ratio \(r\) of the number of points in the neighborhood of the edge to the number of faces in the neighborhood, and then sets \(\kappa = 10^{-2}\) if \(r < 4\), \(\kappa = 10^{-4}\) if \(4 \leq r < 8\), and \(\kappa = 10^{-8}\) if \(r \geq 8\).

The algorithm, as described so far, shows how to simplify a mesh while considering its geometric structure. But meshes often have other attributes, specified on a per-vertex level, such as color, material, etc. Some of these attributes, like color, lie in continuous spaces, where it makes sense to measure differences and to compute averages. Others, like material, can be considered to be more discrete—you’re either on the metal part of the engagement ring or on the diamond; there’s no halfway point between these materials. The first group consists of the **scalar attributes** and the second group consists of the **discrete attributes**.

To assign a scalar attribute to a vertex that results from an edge collapse, we try to pick a value with the property that for each point \(x_i \in X\) on the original surface, with corresponding point \(b_i\) on the simplified mesh, the scalar value \(s(x_i)\) and the corresponding value \(s(b_i)\) (which may have to be interpolated from values at nearby vertices) are as close as possible. More explicitly, we choose a scalar value at the new vertex to minimize

\[E_{\mathrm{scalar}}(V) = \sum_i \|s(x_i) - s(b_i)\|^2.\tag{25.8}\]

Even scalar attributes can require special handling: Consider a cube in which each face is given a different color. At each vertex, there are three color attributes, one for each face corner at the vertex, instead of just one; a complete implementation of the algorithm must address this “distinguished-corner” situation as well.

For discrete attributes like material, Hoppe characterizes an edge as **sharp** if it’s a boundary edge, its two adjacent edges have different discrete attributes, or its adjacent corners have different discrete attributes, in the sense of the preceding paragraph. The set of sharp edges on the mesh form “discontinuity” curves between regions of constant discrete attributes (or between faces that meet with distinguished corners). Hoppe then either disallows or penalizes the collapse of any