
**Input:**

- An \(n \times 1\) table, `fntable`, of function values at the vertices of the mesh
- A point \(P\) of the mesh, expressed by giving the index, \(t\), of the triangle in which the point lies, and its barycentric coordinates \(\alpha, \beta, \gamma\) in that triangle

**Output:**

- The value of the interpolated function at \(P\)

The first thing to realize is that only the \(t\)th row of `ftable` is relevant to our problem: The point \(P\) lies in the \(t\)th triangle; the other triangles might as well not exist. If the \(t\)th triangle has vertex indices \(i_0\), \(i_1\), and \(i_2\), then only those entries in `vtable` matter. With this in mind, our code is quite simple:

```c
double meshinterp(double[,] vtable, int[,] ftable,
   double[] fntable, int t, double alpha, double beta, double gamma)
{
  int i0 = ftable[t, 0];
  int i1 = ftable[t, 1];
  int i2 = ftable[t, 2];
  double fn0 = fntable[i0];
  double fn1 = fntable[i1];
  double fn2 = fntable[i2];
  return alpha*fn0 + beta*fn1 + gamma*fn2;
}
```

Now suppose that \(P\) is given differently: We are given the coordinates of \(P\) in 3-space rather than the barycentric coordinates, and we are given the index \(t\) of the triangle to which \(P\) belongs, and we need to find the barycentric coordinates \(\alpha\), \(\beta\), and \(\gamma\). If we say that the vertices of the triangle \(t\) are \(A\), \(B\), and \(C\), we want to have

\[
\alpha A_x + \beta B_x + \gamma C_x = P_x \tag{9.8}
\]

where the subscript \(x\) indicates the first coordinate of a point; we must also satisfy the same equations for \(y\) and \(z\). But there’s one more equation that has to hold: \(\alpha + \beta + \gamma = 1\). We can rewrite that in a form that’s analogous to the others:

\[
\alpha 1 + \beta 1 + \gamma 1 = 1. \tag{9.9}
\]

Now our system of equations becomes

\[
\begin{bmatrix} A_x & B_x & C_x \\ A_y & B_y & C_y \\ A_z & B_z & C_z \\ 1 & 1 & 1 \end{bmatrix}\begin{bmatrix}\alpha\\\beta\\\gamma\end{bmatrix}=\begin{bmatrix}P_x\\P_y\\P_z\\1\end{bmatrix}. \tag{9.10}
\]

There’s really no solution here except to directly solve the system of equations. The problem is that we have four equations in three unknowns, and most solvers want to work with square matrices rather than rectangular ones. (Section 7.9.2 presented an alternative approach to this problem using some precomputation, but that precomputation amounts to doing much of the work of solving the system of equations.)

The good news is that the four equations are in fact redundant: The fact that \(P\) is given to us as a point of the triangle ensures that if we simply solve the first three equations, the fourth will hold. That assurance, however, is purely mathematical—computationally, it may happen that small errors creep in. There are several viable approaches.

- Express \(P\) as a convex combination of *four* points of \(\mathbb{R}^4\): the three already written and a fourth, with coordinates \(n_x, n_y, n_z\), and 0, where \(\mathbf{n}\) is the normal vector to the triangle. The expression will have a fourth coefficient, \(\delta\), in the solution, representing the degree to which \(P\) is not in the plane of \(A\), \(B\), and \(C\). We ignore this and scale up the computed \(\alpha, \beta,\) and \(\gamma\) accordingly, using \(\alpha/(1-\delta)\), \(\beta/(1-\delta)\), and \(\gamma/(1-\delta)\) as the barycentric coordinates. This is a good solution (in the sense that if the numerical error in \(P\) is entirely in the \(\mathbf{n}\) direction, the method produces the correct result), but it requires solving a \(4 \times 4\) system of equations.
- Delete the fourth row of the system in Equation 9.10; adjust \(\alpha, \beta,\) and \(\gamma\) to sum to one by dividing each by \(\alpha + \beta + \gamma\). This reduces the problem to a \(3 \times 3\) system, but it lacks the promise of correctness for normal-only errors.
- Use the pseudoinverse to solve the overconstrained system (see Section 10.3.9). This has the advantage that it’s already part of many numerical linear algebra systems, and that it works even when the triangle is degenerate (i.e., the three points are collinear), in the sense that if \(P\) lies in the triangle, then the method produces numbers \(\alpha, \beta,\) and \(\gamma\) with \(\alpha A + \beta B + \gamma C = P\), even though the solution in this case is not unique. Better still, if \(P\) is not in the plane of \(A, B,\) and \(C\), the solution returned will have the property that \(\alpha A + \beta B + \gamma C\) is the point in the plane of \(A, B,\) and \(C\) that’s closest to \(P\). This is therefore the ideal.

So the restated problem looks like this:

**Input:**

- A triangle mesh in the form of an \(n \times 3\) table, `vtable`, of vertices
- A \(k \times 3\) table, `ftable`, of triangles, where each row of `ftable` contains three indices into `vtable`
- A point \(P\) of the mesh, expressed by giving the index, \(t\), of the triangle in which the point lies, and its coordinates in 3-space

**Output:**

- The value of the barycentric coordinates of \(P\) with respect to the vertices of the \(t\)th triangle

And our revised solution is this:

```c
double[3] barycentricCoordinates(double[,] vtable,
    int[,] ftable, int t, double p[3])
{
    int i0 = ftable[t, 0];
    int i1 = ftable[t, 1];
    int i2 = ftable[t, 2];
    double[,] m = new double[4, 3];
    for (int j = 0; j < 3; j++) {
        for (int i = 0; i < 3; i++) {
            m[i, j] = vtable[ftable[t, j], i];
        }
        m[3, j] = 1;
    }
    double[,] k = pseudoInverse(m);
    return matrixVectorProduct(k, p);
}
```

Here we’ve assumed the existence of a matrix-vector product procedure and a pseudoinverse procedure, as provided by most numerical packages. The two procedures above can be combined, of course, to produce the function value at a point \(P\) that’s specified in \(xyz\)-coordinates.

**Input:**

- A triangle mesh in the form of an \(n \times 3\) table, `vtable`, of vertices
- A \(k \times 3\) table, `ftable`, of triangles, where each row of `ftable` contains three indices into `vtable`
- An \(n \times 1\) table, `fntable`, of function values at the vertices of the mesh
- A point \(P\) of the mesh, expressed by giving the index, \(t\), of the triangle in which the point lies, and its coordinates in 3-space

**Output:**

- The value of the function defined by the function table at the point \(P\)

```c
double meshinterp2(double[,] vtable, int[,] ftable, double[] fntable,
                   int t, double p[3])
{
    double[] barycentricCoords =
        barycentricCoordinates(vtable, ftable, t, p);
    return meshinterp(vtable, ftable, fntable, t,
        barycentricCoords[0], barycentricCoords[1], barycentricCoords[2]);
}
```

Of course, the same idea can be applied to the ray-intersect-triangle code of Section 7.9.2, where we first computed the barycentric coordinates \((\alpha,\beta,\gamma)\) of the ray-triangle intersection point \(Q\) with respect to the triangle \(ABC\), and then computed the point \(Q\) itself as the barycentric weighted average of \(A\), \(B\), and \(C\). If instead we had function values \(f_A, f_B\), and \(f_C\) at those points, we could have computed the value at \(Q\) as \(f_Q = \alpha f_A + \beta f_B + \gamma f_C\). Notice that this means we can compute the interpolated function value \(f_Q\) at the intersection point without ever computing the intersection point itself!

Computing barycentric coordinates \((\alpha,\beta,\gamma)\) for a point \(P\) of a triangle \(ABC\), where \(A,B,C \in \mathbb{R}^2\), is somewhat simpler than the corresponding problem in 3-space (see Figure 9.3). We know that the lines of constant \(\alpha\) are parallel to \(BC\). If we let \(\mathbf{n}=(C-B)^\perp\), then the function defined by \(f(P)=(P-B)\cdot\mathbf{n}\) is also constant on lines parallel to \(B-C\). Scaling this down by \(f(A)\) gives us the function we need: It’s zero on line \(BC\), and it’s one at \(A\). So we let

\[
g:\mathbb{R}^2\to\mathbb{R}:P\mapsto\frac{(P-B)\cdot\mathbf{n}}{(A-B)\cdot\mathbf{n}},\qquad (9.11)
\]

and the value of \(g(P)\) is just \(\alpha\). A similar computation works for \(\beta\) and \(\gamma\).

The resultant code looks like this:

```c
double[3] barycenter2D(Point P, Point A, Point B, Point C)
{
    double[] result = new double[3];
    result[0] = helper(P, A, B, C);
    result[1] = helper(P, B, C, A);
    result[2] = helper(P, C, A, B);
    return result;
}
```
