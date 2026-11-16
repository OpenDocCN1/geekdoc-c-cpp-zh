
solving the linear system

$$
\begin{pmatrix} M & A^H \\ A & 0 \end{pmatrix} \begin{pmatrix} f \\ \lambda \end{pmatrix} = \begin{pmatrix} 0 \\ q \end{pmatrix},
$$

where \((\cdot)^H\) stands for the conjugate transpose matrix, and the matrix \(M \in \mathbb{C}^{n \times n}\) is given by \(E^H E\). Let \(B \in \mathbb{C}^{n+p \times n+p}\) be the block matrix on the left-hand side of (7.23). Let the block matrix \(B^{-1} = (\cdot \ T)\) be the inverse of \(B\), with \(T \in \mathbb{C}^{n \times p}\), then the solution to (7.22) is given by \(f = Tq\). The matrix \(T\) represents a linear transformation that maps the user-prescribed target positions of the P2P handles \(q\) to the (unknown) target cage vertices \(f_\ell\). Computing \(T\) boils down to evaluating \(B\) and inverting it. Evaluating \(B\) is embarrassingly parallel and can be computed efficiently using modern GPUs. Since \(B\) is typically small, the time for inverting it is often short and the typical runtime for computing \(T\) for a complicated shape is less than a second. More importantly, this computation is done once in preprocessing.

In a typical deformation application, the barycentric coordinates are also evaluated in a preprocessing step on a set of \(m\) points inside \(\Omega\) on which we want to evaluate the barycentric map. Let \(C \in \mathbb{C}^{m \times n}\) be a matrix of Cauchy coordinates evaluated at these points, then during interaction with the system, the only computation that is done is that of the vector \(d \in \mathbb{C}^{m \times 1}\) of deformed points, which is given by the matrix-vector multiplication \(d = Cf\). Since \(f = Tq\), we have \(d = Pq\), where \(P = CT\) is in \(\mathbb{C}^{m \times p}\). The matrix \(P\) can be computed in preprocessing as well, hence during interaction we only need to compute the multiplication \(Pq\), which is more efficient than \(Cf\) since the number of P2P handles \(p\) is typically much smaller than the number of vertices in the cage \(n\).

Finally, the columns of \(P\) can be interpreted as a special type of complex barycentric coordinates, where the vertices of the cage in the barycentric map are substituted with the P2P handles. We call them the P2P-Cauchy coordinates. Calling them barycentric coordinates is justified by the fact that they have constant precision (7.1) and linear precision (7.2). Figure 7.6 shows two examples of image deformation made with the P2P-Cauchy coordinates. An alternative derivation of P2P coordinates can be done by substituting the equality constraints of (7.20) with soft constraints [415]. This results in a smoother deformation at the expense of only approximating the P2P handles.

It is important to note that the quality of variational coordinates like the Szegő and P2P-Cauchy coordinates can be dramatically improved at the expense of longer preprocessing times. Whereas the discrete Cauchy transform always produces holomorphic functions, in contrast to the smooth Cauchy transform (7.8), the discrete transform only spans a finite-dimensional subspace of holomorphic functions. As the number of cage vertices increases, the subspace becomes richer. A simple way to enrich this subspace is to insert "virtual" vertices along the cage edges without altering the geometry of the cage. Typically, the cage is up-sampled as uniformly as possible such that the total number of vertices is at least 200. A non-uniform sampling strategy is also possible, and the actual number of vertices depends on the complexity of the shape and the intended effect.

![](img/4913dd83a2a14bc205a0a92cce102c82_147_0.png)

Figure 7.6 Deformation with P2P-Cauchy coordinates. The P2P handles are depicted by cyan disks. See color insert.

## 7.4 CONFORMAL MAPS

A common mistake is to identify holomorphic functions with planar conformal maps. While a planar conformal map can be expressed as a holomorphic function, the converse is not always true. A holomorphic function \( f : \Omega \rightarrow \mathbb{C} \) is conformal only if its first complex derivative \( f' \) is nonvanishing everywhere in the domain. If \( f \) is holomorphic and \( f'(z_0) = 0 \) for a point \( z_0 \in \Omega \), then angles between intersecting curves at \( z_0 \) are not preserved. Furthermore, the isometric distortion induced by the map is infinite at the singular point \( z_0 \), and high in its vicinity. The turning number of the image of the boundary curve increases, and the map is not locally injective at \( z_0 \). For planar shape deformation, we are mostly interested in locally injective maps with low distortion and artifacts like these should be avoided.

### 7.4.1 Log derivative construction

As we saw in the previous sections, generating holomorphic maps is quite simple, but unfortunately, conformal maps do not form a linear subspace and are harder to control. If \( f \) is Cauchy's barycentric map represented as \( f(z) = \sum_{i=1}^n C_i(z)f_i \), the additional condition \( |f'(z_0)| > 0 \) that guarantees that \( f \) is conformal at \( z_0 \) is a non-convex constraint. Non-convex constraints pose a great challenge for numerical optimization and cannot be enforced efficiently in general. We can address this difficulty by parameterizing the space of conformal maps, by using alternative variables. On a simply connected domain \( \Omega \in \mathbb{C} \), there is a one-to-one correspondence between the space of conformal maps and the space of holomorphic maps [241, 417]. If \( f \) is conformal, it is also holomorphic. The derivative of a holomorphic map is holomorphic, meaning that if \( f \) is conformal, then \( l(z) = \log(f'(z)) \) is holomorphic. With this observation in hand, we represent our conformal map based on the holomorphic function \( l \). No special non-convex constraints on $l$ are needed. We proceed by designing a holomorphic function $l$ according to some criteria, and for each such $l$, a unique corresponding conformal map is reconstructed. The reconstruction process is the key to success and is described as follows. First, we compute the function $e^{(l)}$, which is holomorphic since the complex exponent is, and composition of holomorphic functions is holomorphic. Such a holomorphic function is nonvanishing by construction since $|e^{(l(z))}| = e^{l(z)} \neq 0$. We interpret $e^{(l)}$ as the (nonvanishing) derivative of our (unknown) conformal map, and compute its antiderivative to finally recover the map $f$. This is possible since on a simply connected domain, holomorphic functions are integrable and their antiderivative is also holomorphic.

With these observations in hand, the problem of computing a conformal map becomes that of computing a meaningful holomorphic function $l$ followed by a reconstruction step. Recalling the discussion on the derivative of holomorphic functions in Section 7.2.1, and the definition of the complex logarithm, we have that the function $l$ encodes the amount of local scale and rotation in its real and imaginary parts, respectively,

$$
l(z) = \log(f'(z)) = \ln(|f'(z)|) + i \arg f'(z).
$$

We discretize the function $l$ as

$$
l(z) = \sum_{i=1}^n D_i(z)l_i, \quad (7.24)
$$

with the basis functions

$$
D_i(z) = \frac{1}{2\pi i} \gamma_{l_i}^{\text{Cauchy}}(z) = \frac{1}{2\pi i} \text{Log}\left(\frac{B_{i+1}(z)}{B_i(z)}\right).
$$

Other choices for discretization are possible, including higher order approximations [417], but this simple choice suffices for the sake of discussion. The coefficients $l_i$ in (7.24) can be interpreted as the piecewise constant values of $\log(f'(z))$ on the edges of the cage and our goal is to estimate them from the data provided by the user, that is, the shape of the target cage. Our simple choice is to aim at designing a conformal map $f$ that acts as a (different) similarity transformation on each edge. Given the unique similarity $S_i$ from (7.9) that maps the source edge to the target edge, the derivative is given by $S(z) = \hat{e}_t / \hat{e}_i$ and we use $l_i = \log(\hat{e}_t / \hat{e}_i)$.

When computing $l_i$ in practice, care should be taken when evaluating the complex logarithm, which is a multi-valued function. Standard C++/MATLAB software implementations only produce the single-valued principal branch, and using it independently on each edge may lead to wrong assignment for the imaginary part that encodes the rotation of the edge in radians. Instead, we suggest the following strategy to recover the correct angles. The rotation of the first edge is computed as $l_1 = \text{Log}(\hat{e}_1 / e_1)$, where Log is the standard principal branch implementation with imaginary values in the range $(-\pi, \pi]$. To compute the subsequent $l_i$, we first compute the difference of corner vertex angles between the source and target cages,

$$
d_i = \text{Log}\left(\frac{\hat{e}_t}{\hat{e}_{i-1}}\right) - \text{Log}\left(\frac{e_i}{e_{i-1}}\right),
