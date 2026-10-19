
## 23.4 Finite-Element (Not Difference) Methods, 1D

In an FEM, the domain in which the PDE is solved is split into finite subdomains, called *elements*, and a *trial solution* to the PDE in each subdomain is hypothesized. Then the parameters of the trial solution are adjusted to obtain a *best fit* (in the sense of Chapter 7) to the exact solution. Essentially, this approach converts a given PDE into an integral equation known as the *weak* or *variational* form (“weak” because there is no longer the requirement that the second derivative of the solution exists). A trial solution on each element is then postulated, and this leads to the numerically intensive work of finding the best values for the parameters in the trial solution, and in matching up the various trial solutions from different subdomains.

In general, an FEM solution follows six steps (Li, 2014):

- 1. Derivation of a *weak form* of the PDE. This is equivalent to a least-squares minimization of the integral of the difference between the approximate and exact solutions.
- 2. Discretization of the computational domains.
- 3. Generation of interpolating or trial functions.
- 4. Conversion of the “weak form” integral equation into a set of linear equations.
- 5. Implementation of the boundary conditions.
- 6. Solution of the resulting linear system of equations.

### 23.4.1 Weak Form of PDE

Finite-difference methods yield an approximate solution of an approximate PDE. Finite-element methods yield the best possible global agreement between an approximate solution and the exact solution. We start the FEM with the differential equation we want to solve,

\[
-\frac{d^2U(x)}{dx^2}=4\pi\rho(x). \tag{23.4}
\]

We form an integral of the product of the exact solution \(U(x)\) and the approximate solution or *trial solution* \(\Phi(x)\) over the solution domain. This will be used as a measure of overall agreement between the two solutions. We assume that the trial solution vanishes at the endpoints, \(\Phi(a)=\Phi(b)=0\) (we satisfy general boundary conditions later). We next multiply both sides of the differential equation (23.4) by \(\Phi\) and integrate by parts from \(a\) to \(b\):

\[
-\frac{d^2U(x)}{dx^2}\Phi(x)=4\pi\rho(x)\Phi(x), \tag{23.5}
\]

\[
-\int_a^b dx\,\frac{d^2U(x)}{dx^2}\Phi(x)=\int_a^b dx\,4\pi\rho(x)\Phi(x). \tag{23.6}
\]

Integration by parts gives

\[
-\frac{dU(x)}{dx}\Phi(x)\Big|_a^b+\int_a^b dx\,\frac{dU(x)}{dx}\Phi'(x)=\int_a^b dx\,4\pi\rho(x)\Phi(x). \tag{23.7}
\]

\[
\Rightarrow\quad \int_a^b dx\,\frac{dU(x)}{dx}\Phi'(x)=\int_a^b dx\,4\pi\rho(x)\Phi(x). \tag{23.8}
\]

Equation 23.8 is the weak form of the PDE, “weak” in the sense that it does not require the existence of the second derivative of \(U\), or the continuity of \(\rho\). Because the approximate and exact solutions are related by the integral of their difference over the entire domain, the algorithm provides the global best agreement between the two.

### 23.4.2 Galerkin Spectral Decomposition

The approximate solution to the weak PDE proceeds via three steps. First, we split the full domain of the PDE into subdomains called elements, then we find approximate solutions within each element, and finally we match the elemental solutions onto each other. For our 1D problem, the subdomain elements are straight lines of equal length, while for the 2D problem to be considered soon, the elements are triangles (Figure 23.4).

The critical step in the FEM is the expansion of the solution \(U\) in terms of a set of basis functions \(\phi_i\):

\[
U(x)\simeq\sum_{j=0}^{N-1}\alpha_j\phi_j(x). \tag{23.9}
\]

Even when the basis functions are not sines or cosines, this expansion is still called a spectral decomposition. We will choose \(\phi_i\)’s that are convenient for computation, and so the solution reduces to determining the unknown expansion coefficients \(\alpha_j\). Later, in order to satisfy the boundary conditions, we will add an additional term to this expansion.

Considerable study has gone into determining the effectiveness of different basis functions \(\phi_i\) that are used to represent the solution on the finite elements. If the sizes of the finite elements are made sufficiently small, then good accuracy is obtained with simple piecewise-continuous basis functions \(\phi_i\). For our 1D problem, we use finite elements that are line segments between \(x_i\) and \(x_{i+1}\), and we use basis functions, representing the solution on each line segment, that have the form of triangle or “hats” between \(x_{i-1}\) and \(x_{i+1}\) (Figure 23.2). We also require that each basis function equals 1 at the \(x_i\) vertex, \(\phi_i(x_i)=1\):

\[
\phi_i(x)=
\begin{cases}
0, & x<x_{i-1}\ \text{or}\ x>x_{i+1},\\[2pt]
\dfrac{x-x_{i-1}}{h_{i-1}}, & x_{i-1}\le x\le x_i,\\[4pt]
\dfrac{x_{i+1}-x}{h_i}, & x_i\le x\le x_{i+1},
\end{cases}
\qquad (h_i=x_{i+1}-x_i). \tag{23.10}
\]

![](img/bccda43674e4a93dee81c749eba8d2f7_564_0.png)

Because this choice means that each basis function equals 0 or 1 at the nodes,

\[
\phi_i(x_j)=\delta_{ij}, \tag{23.11}
\]

the values of the expansion coefficients \(\alpha_i\) must equal the values of the (still unknown) solution at the nodes:

\[
U(x_i)\simeq\sum_{j=0}^{N-1}\alpha_j\phi_j(x_i)=\alpha_i\phi_i(x_i)=\alpha_i, \tag{23.12}
\]

\[
\Rightarrow\quad U(x)\simeq\sum_{j=0}^{N-1}U(x_j)\phi_j(x). \tag{23.13}
\]

Equation 23.13 makes it clear that the expansion in terms of basis functions is essentially an interpolation between the actual solution at the nodes.

#### 23.4.2.1 Solution via Linear Equations

Because the basis functions \(\phi_i\) in (23.9) are known, solving for \(U(x)\) involves determining the coefficients \(\alpha_j\), which, as we just said, are the unknown values of the true solution \(U(x)\) on the nodes. We determine those values by substituting the expansions for \(U(x)\) and \(\Phi(x)\) into the weak form of the PDE (23.8). This converts the integral equation into a set of simultaneous linear equations. As discussed in Chapter 6, there is a standard matrix form for a set of linear equations,

\[
A\,y=b. \tag{23.14}
\]

Our equations fit that, with \(y\) a vector of unknowns, and where we still need to specify the known stiffness matrix \(A\) and the known load vector \(b\). To that end, we substitute the expansion \(U(x)\simeq\sum_{j=0}^{N-1}\alpha_j\phi_j(x)\) into the weak form (23.8) to obtain:

\[
\int_a^b dx\,\frac{d}{dx}\left(\sum_{j=0}^{N-1}\alpha_j\phi_j(x)\right)\frac{d\Phi}{dx}
=
\int_a^b dx\,4\pi\rho(x)\Phi(x).
\]

By successively selecting \(\Phi(x)=\phi_0,\phi_1,\ldots,\phi_{N-1}\), we obtain \(N\) simultaneous linear equations for the unknown \(\alpha_j\)’s:

\[
\int_a^b dx\,\frac{d}{dx}\left(\sum_{j=0}^{N-1}\alpha_j\phi_j(x)\right)\frac{d\phi_i}{dx}
=
\int_a^b dx\,4\pi\rho(x)\phi_i(x),
\qquad i=0,\ldots,N-1. \tag{23.15}
\]

We factor out the unknown \(\alpha_j\)’s and write the equations out explicitly:

\[
\begin{aligned}
\alpha_0\int_a^b \phi_0'\phi_0'\,dx
+\alpha_1\int_a^b \phi_0'\phi_1'\,dx
+\cdots
+\alpha_{N-1}\int_a^b \phi_0'\phi_{N-1}'\,dx
&=\int_a^b 4\pi\rho\,\phi_0\,dx,\\
\alpha_0\int_a^b \phi_1'\phi_0'\,dx
+\alpha_1\int_a^b \phi_1'\phi_1'\,dx
+\cdots
+\alpha_{N-1}\int_a^b \phi_1'\phi_{N-1}'\,dx
&=\int_a^b 4\pi\rho\,\phi_1\,dx,\\
&\vdots\\
\alpha_0\int_a^b \phi_{N-1}'\phi_0'\,dx
+\alpha_1\int_a^b \phi_{N-1}'\phi_1'\,dx
+\cdots
+\alpha_{N-1}\int_a^b \phi_{N-1}'\phi_{N-1}'\,dx
&=\int_a^b 4\pi\rho\,\phi_{N-1}\,dx.
\end{aligned}
\]

Because we have chosen the \(\phi_i\)’s to be the simple hat functions, the derivatives are easy to evaluate analytically (for other bases they can be carried out numerically):

\[
\frac{d\phi_i}{dx}=
\begin{cases}
0, & x<x_{i-1}\ \text{or}\ x>x_{i+1},\\[2pt]
\dfrac{1}{h_{i-1}}, & x_{i-1}\le x\le x_i,\\[4pt]
-\dfrac{1}{h_i}, & x_i\le x\le x_{i+1},
\end{cases}
\qquad
\frac{d\phi_{i+1}}{dx}=
\begin{cases}
0, & x<x_i\ \text{or}\ x>x_{i+2},\\[2pt]
\dfrac{1}{h_i}, & x_i\le x\le x_{i+1},\\[4pt]
-\dfrac{1}{h_{i+1}}, & x_{i+1}\le x\le x_{i+2}.
\end{cases}
\tag{23.16}
\]

The integrations are now fairly simple:

\[
\int_{x_{i-1}}^{x_{i+1}} dx\,(\phi_i')^2
=\int_{x_{i-1}}^{x_i} dx\,\frac{1}{h_{i-1}^2}
+\int_{x_i}^{x_{i+1}} dx\,\frac{1}{h_i^2}
=\frac{1}{h_{i-1}}+\frac{1}{h_i}, \tag{23.17}
\]

\[
\int_{x_{i-1}}^{x_{i+1}} dx\,\phi_i'\phi_{i+1}'
=\int_{x_{i-1}}^{x_{i+1}} dx\,\phi_{i+1}'\phi_i'
=\int_{x_i}^{x_{i+1}} dx\left(-\frac{1}{h_i^2}\right)
=-\frac{1}{h_i}, \tag{23.18}
\]

\[
\int_{x_{i-1}}^{x_{i+2}} dx\,(\phi_{i+1}')^2
=\int_{x_i}^{x_{i+1}} dx\,\frac{1}{h_i^2}
+\int_{x_{i+1}}^{x_{i+2}} dx\,\frac{1}{h_{i+1}^2}
=\frac{1}{h_i}+\frac{1}{h_{i+1}}. \tag{23.19}
\]

We rewrite these equations in the standard matrix form (23.14) with \(y\) constructed from the unknown \(\alpha_j\)’s, and the tridiagonal stiffness matrix \(A\) constructed from the integrals over the derivatives:

\[
y=
\begin{bmatrix}
\alpha_0\\[2pt]
\alpha_1\\[2pt]
\vdots\\[2pt]
\alpha_{N-1}
\end{bmatrix},\qquad
b=
\begin{bmatrix}
\int_{x_0}^{x_1} dx\,4\pi\rho(x)\phi_0(x)\\[2pt]
\int_{x_1}^{x_2} dx\,4\pi\rho(x)\phi_1(x)\\[2pt]
\vdots\\[2pt]
\int_{x_{N-1}}^{x_N} dx\,4\pi\rho(x)\phi_{N-1}(x)
\end{bmatrix}
\tag{23.20}
\]

\[
A=
\begin{bmatrix}
\dfrac{1}{h_0}+\dfrac{1}{h_1} & -\dfrac{1}{h_1} & 0 & \cdots & 0\\[6pt]
-\dfrac{1}{h_1} & \dfrac{1}{h_1}+\dfrac{1}{h_2} & -\dfrac{1}{h_2} & \cdots & 0\\[6pt]
0 & -\dfrac{1}{h_2} & \dfrac{1}{h_2}+\dfrac{1}{h_3} & \cdots & 0\\[6pt]
\vdots & \vdots & \ddots & \ddots & \vdots\\[4pt]
0 & 0 & \cdots & -\dfrac{1}{h_{N-2}} & \dfrac{1}{h_{N-2}}+\dfrac{1}{h_{N-1}}
\end{bmatrix}.
\tag{23.21}
\]

The elements in \(A\) are just combinations of inverse step sizes and so do not change for different charge densities \(\rho(x)\). This is part of what makes FEM so efficient once set up. The elements in \(b\) do change for different \(\rho\)’s, but the required integrals can be performed analytically or with Gaussian quadrature (Chapter 5). Once \(A\) and \(b\) are computed, highly efficient methods from a linear algebra package are used to solve the matrix equations for \(y\), and thus the expansion coefficients \(\alpha_j\).

#### 23.4.2.2 Dirichlet Boundary Conditions

Because the basis functions vanish at the endpoints, a solution expanded in them must also vanish there. This will not do in general, and so we must add to our general solution \(U(x)\) a particular solution \(U_a\phi_0(x)\) that satisfies the boundary conditions (Li, 2014):

\[
U(x)=\sum_{j=0}^{N-1}\alpha_j\phi_j(x)+U_a\phi_0(x)
\quad \text{(satisfies boundary conditions)}, \tag{23.22}
\]

where \(U_a=U(x_a)\). We substitute \(U(x)-U_a\phi_0(x)\) into the weak form of the PDE to obtain \((N+1)\) simultaneous equations, still of the form \(Ay=b\), but now with

\[
A=
\begin{bmatrix}
A_{0,0} & \cdots & A_{0,N-1} & 0\\[2pt]
\vdots & & \vdots & \vdots\\[2pt]
A_{N-1,0} & \cdots & A_{N-1,N-1} & 0\\[2pt]
0 & \cdots & 0 & 1
\end{bmatrix},\qquad
b'=
\begin{bmatrix}
b_0-A_{0,0}U_a\\[2pt]
\vdots\\[2pt]
b_{N-1}-A_{N-1,0}U_a\\[2pt]
U_a
\end{bmatrix}.
\tag{23.23}
\]

This is equivalent to adding a unit element to \(A\) and adding a new load vector element:

\[
b_i'=b_i-A_{i,0}U_a,\quad i=0,\ldots,N-1,\qquad b_N'=U_a. \tag{23.24}
\]
