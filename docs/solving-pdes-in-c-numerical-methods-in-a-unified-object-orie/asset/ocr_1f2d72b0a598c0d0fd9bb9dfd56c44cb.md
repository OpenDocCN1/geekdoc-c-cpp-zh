# Chapter 27. Application in Nonlinear Optics

Consider a general tetrahedron $t$ in the three-dimensional Cartesian space, with vertices (or corners) denoted by $\vec{k}$, $\vec{m}$, and $\vec{n}$:

$$t = (\vec{k}, \vec{m}, \vec{n}).$$

where the order of vertices in this notation is determined arbitrarily in advance. With this notation, the reference tetrahedron is presented as

$$T = ((0,0,0),(1,0,0),(0,1,0),(0,0,1)).$$

Let $S_t$ be the $3 \times 3$ matrix whose columns are the three-dimensional vectors leading from $\vec{k}$ to the three other corners of $t$:

$$S_t \equiv (\vec{l} - \vec{k} | \vec{m} - \vec{k} | \vec{n} - \vec{k}).$$

With this notation,

$$S_T = I$$

is the $3 \times 3$ identity matrix.

Let us use the matrix $S_t$ to define a mapping from $T$ onto $t$:

$$D_t \left( \begin{pmatrix} x \\ y \\ z \end{pmatrix} \right) \equiv \vec{k} + S_t \left( \begin{pmatrix} x \\ y \\ z \end{pmatrix} \right).$$

Indeed, the corners of the reference tetrahedron $T$ are mapped onto the corresponding corners of $t$:

$$D_t \left( \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix} \right) = \vec{k}$$

$$D_t \left( \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} \right) = \vec{l}$$

$$D_t \left( \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} \right) = \vec{m}$$

$$D_t \left( \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix} \right) = \vec{n}.$$

Clearly, the inverse mapping maps $t$ back onto $T$:

$$D_t^{-1} \left( \begin{pmatrix} x \\ y \\ z \end{pmatrix} \right) = S_t^{-1} \left( \begin{pmatrix} x \\ y \\ z \end{pmatrix} - \vec{k} \right).$$

Below we use this mapping to define the coefficient matrix for the finite-element scheme.