
dimensions for periodic problems as the lattice sums involved have an explicit analytical representation. However, in three dimensions, boundary integral methods are considerably more difficult to implement.

The overall goal of the present work is to understand the relative effectiveness and accuracy of each method for two-dimensional fluids. The CS, AFM and AFM* methods involve highly ill-conditioned intermediate calculations, so much of the paper focuses on whether accurate results can be obtained if multiple-precision arithmetic is employed in these intermediate calculations. In particular, for timestepping the water wave, it is important that the methods work if the input data is only known with limited accuracy — additional precision in intermediate calculations is permissible as long as the output is roughly as accurate as the input. Given the care required to obtain high accuracy in the present work, one must be cautious about using these methods in double-precision without carefully monitoring condition numbers and cancellation of digits.

An outline of the paper is as follows. In § 2, we briefly introduce the CS operator expansion, the AFM and AFM* nonlocal formulations, and the boundary integral and TFE representations of the DNO. In §3 we present comparisons of the first four of these methods for specific choices of the free surface η. Here we seek to quantify how accurate the CS, AFM and AFM* methods are. We assume the exact DNO is obtained from the boundary integral method, and, where suitable, perform computations using higher precision. Section 3.1 discusses the subtle cancellation properties associated with the series representation of Craig & Sulem. In §3.2, we present a specific example where the AFM* method (in its usual interpretation as a system of equations for the coefficients of a certain series) is guaranteed to fail, and other instances where AFM and AFM* successfully converge to the correct Neumann data. The subtle cancellation of the CS expansion is mirrored by the rapidly decaying singular values associated with the AFM/AFM* methods. This leads us to consider regularized versions of AFM/AFM* that involve oversampling the AFM basis functions to accurately approximate a Gram-Schmidt orthogonalization procedure via QR factorization or the singular value decomposition. In the SVD approach, we also investigate the use of a pseudo-inverse cutoff threshold. We find that the AFM basis functions can be more efficient at representing solutions than a Fourier basis, but with the drawback of poor conditioning. Finally, in §3.3, we discuss the behavior of all the methods on examples relevant to water waves.

## 2. Representations of the Dirichlet–Neumann operator

As mentioned in the introduction, the Dirichlet–Neumann operator plays an important role in the mathematical formulation of the motion of surface gravity waves. To efficiently compute the time-dependent motion, we require a fast and efficient means to solve Laplace’s equation, or alternatively, a direct method to compute the Dirichlet–Neumann operator. In this section, we outline five commonly used approaches. The first, due to Craig & Sulem [11], involves expanding the DNO in a Taylor series. The second, due to Ablowitz, Fokas and Musslimani [1], involves deriving a global relation between the Dirichlet and Neumann data that can be used as an integral equation to solve for the Neumann data. The third [2,12,25,28] is a dual variant of the second, formulated more directly. The fourth is a boundary integral collocation method [5,6,16,19,20,31,32]. And the fifth is the transformed field expansion method of Bruno & Reitich [7] and Nicholls & Reitich [23,24].

Similarly, proceeding to higher order, we obtain further terms in the expansion of the DNO. For instance,

$G_1 = D\eta D - G_0\eta G_0,$

$G_2 = -\frac{1}{2}\left(G_0\eta^2 D^2 - 2G_0\eta G_0\eta G_0 + D^2\eta^2 G_0\right),$

where $D = -i\partial_x$ and $G_0 = D\tanh(hD)$. Terms such as $\tanh(hD)$ are understood as pseudo differential operators, i.e. they are defined through associated Fourier multipliers. We remark that higher order terms of the Taylor expansion of $G$ involve increasingly higher order derivatives. Although the Taylor series of $G$ exists for $\eta$ with a limited (even finite) degree of smoothness, the formulas for $G_i(\eta)$ are not valid in such cases, or must be interpreted very carefully, as a whole, rather than as a sum of individual operators. Even when $\eta$ is real analytic, there is a delicate balance existing among the terms that leads to a high degree of cancellation [23]. This causes numerical difficulties in finite precision arithmetic. We explore the extent of these cancellations in arbitrary precision arithmetic in §3. Of course, many of these problems can be avoided by flattening the domain through a change of variables [7, 17, 23], or using boundary integral methods to compute the DNO [31, 32]. However, the original Craig–Sulem expansion remains of theoretical interest, and is the one most closely related to the AFM approach, discussed next.

### 2.2. AFM Implicit Representation.

Following [1, 2], we now derive the global relation of the Ablowitz–Fokas–Musslimani reformulation of the water-wave problem. The distinguishing feature of this reformulation is the implicit nonlocal characterization of the Dirichlet–Neumann operator. Solving the resulting integral equation gives the full DNO, effectively summing all the terms in the expansion of Craig & Sulem without having to compute them order by order.

As above, the functions

(2.2)

$\psi = \exp(ikx)\cosh(k(y+h))$

play a role, but now as dual functions rather than basis functions. From Green’s second identity, we have

$0 = \int_D \left(\psi(\phi_{xx}+\phi_{yy}) - \phi(\psi_{xx}+\psi_{yy})\right) dx\,dy,$

$= \int_{\partial D} \left(\psi\frac{\partial\phi}{\partial n} - \phi\frac{\partial\psi}{\partial n}\right) dS,$

$= \int_0^L \psi(x,\eta)\left[\phi_y(x,\eta) - \eta_x\phi_x(x,\eta)\right] dx - \int_0^L \phi(x,\eta)\left[\psi_y(x,\eta) - \eta_x\psi_x(x,\eta)\right] dx,$

(2.3)

$= \int_0^L \psi(x,\eta)\mathcal{N}(x)dx - \int_0^L \mathscr{D}(x)\left[\psi_y(x,\eta) - \eta_x\psi_x(x,\eta)\right] dx,$

where $\partial/\partial n$ is the normal derivative to the surface. Using the definition of $\psi$ and noting that

$e^{ikx}\left(k\sinh(k(\eta+h)) - ik\eta_x\cosh(k(\eta+h))\right) = -i\partial_x\left(e^{ikx}\sinh(k(\eta+h))\right),$

we obtain

(2.4) $\int_{0}^{L} e^{ikx} \cosh(k(\eta + h)) \mathscr{N}(x) \,dx = \int_{0}^{L} i e^{ikx} \sinh(k(\eta + h)) \partial_x \mathscr{D}(x) \,dx,$

which is the Ablowitz-Fokas-Musslimani (AFM) global relation [1] for Laplace’s equation. Note that the global relation thus obtained is but a rephrasing of Green’s identity. In [1], the authors obtain this expression in a different, but equivalent, manner. By a spectral collocation technique, this yields an algorithm in which approximate values $\mathscr{N}(x_j)$ are obtained on a grid $\{x_j\}_{j=0}^{M-1}$ by solving a linear system. In that case, (2.4) is enforced for wave numbers $|k| \le (2\pi/L)M/2$.

A third approach, due to Ablowitz & Haut [2], can be derived from (2.4) through a type of inverse Fourier transform. The resulting DNO algorithm boils down to solving

(2.5) $\sum_{k} \hat{\Psi}_k e^{ikx} \cosh(k(\eta + h)) = \mathscr{D}(x),$

for the expansion coefficients $\hat{\Psi}_k$, and then computing

(2.6) $\mathscr{N}(x) = -i \partial_x \left( \sum_{k} \hat{\Psi}_k e^{ikx} \sinh(k(\eta + h)) \right).$

For those functions $\mathscr{D}(x)$ that permit an expansion of the form (2.5), the normal derivative is expected (from term by term differentiation) to be of the form (2.6).

The operation of solving the integral equation (2.4) is the formal adjoint of solving the system (2.5), (2.6). Indeed, if the (conjugate of the) former is written $\mathscr{N} = (A^*)^{-1} B^* \partial_x \mathscr{D}$, then the latter becomes $\mathscr{N} = -\partial_x B A^{-1} \mathscr{D}$, which are consistent since G(\eta) is self-adjoint. Here

$A c = \sum_{k} c_k e^{ikx} \frac{\cosh(k(\eta(x) + h))}{w_k}, \quad (A^* f)_k = \int_{0}^{L} e^{-ikx} \frac{\cosh(k(\eta(x) + h))}{w_k} f(x) \,dx,$

(2.7) $B c = \sum_{k} c_k i e^{ikx} \frac{\sinh(k(\eta(x) + h))}{w_k}, \quad (B^* f)_k = \int_{0}^{L} e^{-ikx} \frac{\sinh(k(\eta(x) + h))}{i w_k} f(x) \,dx,$

and the weights w_k are chosen to make A and B bounded from $\ell^2(\mathbb{Z})$ to L^2(0,L). Formally, these weights cancel internally in the products $(A^*)^{-1} B^*$ and $B A^{-1}$. Indeed, the results are formally unchanged if both sides of (2.4) are multiplied by w_k^{-1}, or if the weights are absorbed into $\hat{\Psi}_k$ in (2.5), (2.6). These statements are only formal since A and A^* are not invertible.

### 2.3. Boundary Integral Method.

Whereas the AFM* method represents $\phi$ in the fluid as a superposition of basic solutions of the Laplace equation of the form e^{ky} e^{ikx}, the boundary integral method represents $\phi$ as a superposition of dipoles distributed along the surface,

$\phi(z) = \int_{-\infty}^{\infty} -\frac{\partial N}{\partial n_\zeta}(z, \zeta(\alpha)) \mu(\zeta(\alpha)) |\zeta'(\alpha)| \,d\alpha, \qquad N(z, \zeta) = \frac{1}{2\pi} \log |z - \zeta|.$
