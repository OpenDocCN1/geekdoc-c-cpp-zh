We can see this, in the case that the polygon is a triangle, by examining coordinates: If $P_i = (x_i, y_i, z_i)$ for $i = 0, 1, 2$, then $n_1$, the first entry of the cross product, is just

$$n_1 = (y_1 - y_0)(z_2 - z_1) - (y_2 - y_1)(z_1 - z_0). \tag{7.126}$$

The area formula for a plane polygon, Equation 7.124, applied to the projection of $P_0P_1P_2$ to the $yz$-plane, gives

$$A_{yz} = \frac{1}{2} \sum_{i=0}^{n} (y_i z_{i+1} - z_i y_{i+1}), \quad \text{so} \tag{7.127}$$
$$2A_{yz} = (y_0 z_1 - z_0 y_1) + (y_1 z_2 - z_1 y_2) + (y_2 z_0 - z_2 y_0). \tag{7.128}$$

The eight terms in the expansion of the expression for $n_1$ match the six terms in the expression for $2A_{yz}$ because two $y_i z_i$ terms have opposite signs and cancel. The computations for $n_2$ and $n_3$ are similar. Thus, the vector

$$\mathbf{a} = \begin{bmatrix} A_{yz} \\ A_{zx} \\ A_{xy} \end{bmatrix} \tag{7.129}$$

is twice the cross product; since half the length of the cross product is that triangle area, we see that the length of $\mathbf{a}$ is the triangle area.

The more general case follows by decomposing the polygon into a union of triangles.

The advantage of Plücker's formula as applied to polygons in space is that if there are small numerical errors in the coordinates of a single vertex, they have relatively little impact on the computed normal vector.

# 7.10.5 Signed Areas for More General Polygons

If we have a polygon $P_0P_1 \ldots P_n$ in a plane $S$ whose normal is the unit vector $\mathbf{n}$, we can find two orthogonal unit vectors $\mathbf{x}$ and $\mathbf{y}$ in $S$ such that $\mathbf{x}, \mathbf{y}, \mathbf{n}$ is positively oriented, that is, $\mathbf{n} = \mathbf{x} \times \mathbf{y}$. Choosing some point of the plane as the origin, we have a coordinate system. We can then write the coordinates of each $P_i$ in the $xy\mathbf{n}$-coordinate system; the third coordinate will be zero, so the coordinates of $P_i$ will be $(x_i, y_i, 0)$. We can apply the formula for a signed area to these coordinates. In the case of a triangle, if the signed area is positive (resp. negative), we say that the triangle is **positively** (resp. **negatively**) **oriented**. Notice, though, that if we had used $-\mathbf{n}$ instead of $\mathbf{n}$, the signs would have changed: The signed area, and the orientation of a triangle, are only defined relative to a plane-with-normal.

Just as in the case of the $xz$-plane, a triangle is positively oriented in a plane with normal $\mathbf{n}$ if, as we look from the tip of $\mathbf{n}$ toward the plane, the vertices of the triangle appear in counterclockwise order.

When we speak of the signed area of a polygon in the $xz$-plane, we mean that we're using a coordinate system in which the first basis vector is $[0\ 0\ 1]^T$, the second is $[1\ 0\ 0]^T$, and the normal vector is $[0\ 1\ 0]^T$; a parallel description applies to the $xy$- and $yz$-planes.