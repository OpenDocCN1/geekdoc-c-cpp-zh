
where
\[
\mathcal{S}_\kappa = \sinh(\kappa(\eta_0 + h)),\quad \mathcal{C}_\kappa = \cosh(\kappa(\eta_0 + h)).
\]

As before, since the problem does not depend on \(y\) or \(t\) explicitly, we use separation of variables to decompose \(\eta_1(x,y,t)\) and \(q_1(x,y,t)\) as in (3.3). Using this decomposition, we obtain

\[
\left\langle\!\left\langle e^{-i\vec{k}\cdot\mathbf{x}}e^{i\rho y}\left(i\tilde{\eta}_{1,t}\mathcal{C}_\kappa - i c\eta_{0,x}\tilde{\eta}_1\mathcal{S}_\kappa - i c\tilde{\eta}_{1,x}\mathcal{C}_\kappa - \frac{1}{\kappa}\left(k_x\tilde{q}_{1,x}+i k_y\rho\tilde{q}_1\right)\mathcal{S}_\kappa - k_x q_{0,x}\tilde{\eta}_1\mathcal{C}_\kappa\right)\right\rangle\!\right\rangle = 0,
\]

Since our new integrand depends on \(y\) only through \(e^{i(\rho-k_y)y}\), we eliminate the integration with respect to \(y\) completely. Calculating the average value along the \(y\) direction results in

\[
\lim_{M\to\infty}\frac{1}{M}\int_{-M/2}^{M/2} e^{-i(k_y-\rho)y}\,dy
= \lim_{M\to\infty}\frac{2}{M(k_y-\rho)}\sin\left(\frac{M(k_y-\rho)}{2}\right).
\]

Taking the limit as \(M\to\infty\), the contribution is identically zero if \(k_y\neq\rho\). Otherwise, if \(k_y=\rho\), the contribution from the integral is unity. Thus, the linearization of the nonlocal equation simplifies to

\[
\left\langle e^{-i k_x x}\left(i\lambda\tilde{\eta}_1\mathcal{C}_\kappa - i c\tilde{\eta}_{1,x}\mathcal{C}_\kappa - \eta_{0,x}c\kappa\tilde{\eta}_1\mathcal{S}_\kappa - \frac{1}{\kappa}\left(k_x\tilde{q}_{1,x}+i\rho^2\tilde{q}_1\right)\mathcal{S}_\kappa - k_x q_{0,x}\tilde{\eta}_1\mathcal{C}_\kappa\right)\right\rangle = 0,
\tag{3.5}
\]

where now \(\kappa = \sqrt{k_x^2+\rho^2}\) and
\[
\langle f\rangle = \lim_{M\to\infty}\frac{1}{M}\int_{-M/2}^{M/2} f(x)\,dx.
\]

It should be noted that if we set \(\rho=0\), the above equation reduces to the expression for the one-dimensional surface case presented elsewhere [DO].

Having linearized the equations about the traveling wave solution, we have the following generalized eigenvalue problem:

\[
\tag{3.6}
\lambda\tilde{q}_1 - c\tilde{q}_{1,x} + q_{0,x}\tilde{q}_{1,x} + g\tilde{\eta}_1
- f\left(\lambda\tilde{\eta}_1 + \tilde{\eta}_{1,x}(q_{0,x}-c) + \eta_{0,x}\tilde{q}_{1,x} - \eta_{0,x}f\tilde{\eta}_{1,x}\right) = 0,
\]

\[
\tag{3.7}
\lambda\left\langle e^{-i k_x x}\left(i\tilde{\eta}_1\mathcal{C}_\kappa\right)\right\rangle
= \left\langle e^{-i k_x x}\left(i c\tilde{\eta}_{1,x}\mathcal{C}_\kappa + i\eta_{0,x}c\kappa\tilde{\eta}_1\mathcal{S}_\kappa + \frac{1}{\kappa}\left(k_x\tilde{q}_{1,x}+i\rho^2\tilde{q}_1\right)\mathcal{S}_\kappa + k_x q_{0,x}\tilde{\eta}_1\mathcal{C}_\kappa\right)\right\rangle.
\]

Equations (3.6) and (3.7) are valid for \((k_x,\rho)\in\mathbb{R}^2-\{(0,0)\}\), and can be rewritten compactly as

\[
\tag{3.8}
\lambda\mathcal{L}_1U(x)=\mathcal{L}_2U(x)
\]

where \(\mathcal{L}_1\) and \(\mathcal{L}_2\) are \(2\times2\) matrices of linear operators that depend on \(\rho\), and whose entries are easily read off from (3.6) and (3.7).

Since the time dependence of the perturbation depends exponentially on \(\lambda\), we can determine information about the stability of the underlying traveling wave by determining the solutions of this generalized eigenvalue problem. If any solutions \(U(x)\) exist for which the corresponding \(\lambda\) has a positive real part, the linear approximation of the solution grows exponentially in time and the perturbed solution will diverge from the stationary solution in the linear approximation. With this intuition in mind, the concept of spectral stability, as applicable to the generalized eigenvalue problem (3.8), is defined as

## DEFINITION 3.1 (Spectral Stability)

A one-dimensional periodic traveling wave solution \((\eta_0(x), q_0(x), c)\) of Equations 2.7 and 2.8 (and thus of the Euler equations) is spectrally stable with respect to two-dimensional perturbations parameterized by \(\rho\) if no element of the spectrum for the generalized eigenvalue problem 3.8 has strictly positive real part.

In order to use this definition, we recall the definition of the spectrum of the generalized eigenvalue problem.

## DEFINITION 3.2 (Spectrum of the Generalized Eigenvalue Problem)

The spectrum of the generalized eigenvalue problem \(\lambda\mathcal{L}_1U(x)=\mathcal{L}_2U(x)\) is given by

\[
\tag{3.9}
\sigma(\mathcal{L}_2,\mathcal{L}_1)=\{\lambda\in\mathbb{C}:\|U(x)\|<\infty\},
\]

where \(U(x)\) solves \(\lambda\mathcal{L}_1U(x)=\mathcal{L}_2U(x)\).

In order to examine spectral stability or instability, we need to locate the spectrum of the generalized eigenvalue problem 3.8. By definition of the spectrum, we determine those values of \(\lambda\in\mathbb{C}\) for which Equation 3.8 has bounded solutions. Since the coefficient functions of Equation (3.8) are periodic in \(x\) with period \(L_1\), we decompose the perturbations further using Floquet’s Theorem, see for instance Ref. [DK06]. Thus, both \(\tilde{q}_1(x)\) and \(\tilde{\eta}_1(x)\) can be written as

\[
\tilde{q}_1(x)=e^{i\mu x}\bar{q}_1(x),\qquad
\tilde{\eta}_1(x)=e^{i\mu x}\bar{\eta}_1(x),
\]

where \(\mu\in[-\pi/L_1,\pi/L_1)\) and \(\bar{q}_1\) and \(\bar{\eta}_1\) are \(2\pi\)-periodic functions.

Substituting the Floquet decomposition into the eigenvalue problem yields

\[
\begin{aligned}
\lambda(\bar{q}_1-f\bar{\eta}_1)
&= c(i\mu+\partial_x)\bar{q}_1-q_{0,x}(i\mu+\partial_x)\bar{q}_1-g\bar{\eta}_1 \\
&\quad + f\big((q_{0,x}-c)(i\mu+\partial_x)\bar{\eta}_1+\eta_{0,x}(i\mu+\partial_x)\bar{q}_1-\eta_{0,x}f(i\mu+\partial_x)\bar{\eta}_1\big),\\[2pt]
\lambda\Bigl\langle e^{i(\mu-k_x)x}\left(i\bar{\eta}_1\mathcal{C}_\kappa\right)\Bigr\rangle
&= \Bigl\langle e^{i(\mu-k_x)x}\Bigl(ic\mathcal{C}_\kappa(i\mu+\partial_x)\bar{\eta}_1+i\eta_{0,x}c\kappa\bar{\eta}_1\mathcal{S}_\kappa \\
&\qquad+\frac{1}{\kappa}\left(k_x(i\mu+\partial_x)+i\rho^2\right)\bar{q}_1\mathcal{S}_\kappa+k_xq_{0,x}\bar{\eta}_1\mathcal{C}_\kappa\Bigr)\Bigr\rangle=0.
\end{aligned}
\tag{3.10}
\]

We represent the \(2\pi\)-periodic portion of the eigenfunctions \(\bar{q}_1\) and \(\bar{\eta}_1\) by their Fourier series. In other words,

\[
\bar{q}_1(x)=\sum_{m=-\infty}^{\infty}\hat{Q}_m e^{imx},\qquad
\bar{\eta}_1(x)=\sum_{m=-\infty}^{\infty}\hat{N}_m e^{imx}.
\]

Additionally, we represent the periodic variable coefficient functions by their Fourier series as well. Substituting the series representations into the Floquet decomposition, we are able to determine a bi-infinite matrix eigenvalue problem, where the eigenvectors are the Fourier coefficients \(\hat{Q}_j\) and \(\hat{N}_j\) for \(j\in\{0,\pm1,\pm2,\ldots\}\). The Fourier decomposition proceeds in a straightforward manner for the local equation. Substituting the Fourier expansions into the local equation, we obtain

\[
\tag{3.12}
\lambda\left(\sum_{m=-\infty}^{\infty}\hat{F}_{3,n-m}\hat{N}_m-\hat{Q}_n\right)
= -g\hat{N}_n+\sum_{m=-\infty}^{\infty}(i\mu+im)\hat{F}_{1,n-m}\hat{N}_m
+\sum_{m=-\infty}^{\infty}\hat{F}_{2,n-m}(i\mu+im)\hat{Q}_m,
\]

for \(n\in\mathbb{Z}\setminus\{0\}\), where the coefficients \(\hat{F}_{j,n}\) are given by the following expressions:

\[
\hat{F}_{1,n}=\int_0^{L_1} e^{-2in\pi x/L_1} f(\eta_0,q_0)(q_{0,x}-c-\eta_{0,x}f(\eta_0,q_0))\,dx,
\]
\[
\hat{F}_{2,n}=\int_0^{L_1} e^{-2in\pi x/L_1} (q_{0,x}-c-\eta_{0,x}f(\eta_0,q_0))\,dx,
\]
\[
\hat{F}_{3,n}=\int_0^{L_1} e^{-2in\pi x/L_1} f(\eta_0,q_0)\,dx.
\]

For the nonlocal equation, we employ a similar strategy as used elsewhere [DO]. There are two slight differences. First, the hyperbolic sine and cosine terms depend on \(\kappa=\sqrt{k_x^2+\rho^2}\) instead of \(k_x\) directly. Second, there is an additional term depending on the perturbation of the velocity potential and on \(\rho\). Substituting the Fourier series into the nonlocal equation and representing all variable coefficients by their Fourier series representation, we have

\[
\tag{3.13}
\sum_{j=-\infty}^{\infty}\sum_{m=-\infty}^{\infty}
\left[
\left(\hat{G}_{1,j}^{(k_x)}+ic(i\mu+im)\hat{G}_{2,j}^{(k_x)}\right)\hat{N}_m
+\left(\frac{k_x}{\kappa}(i\mu+im)+\frac{i\rho^2}{\kappa}\right)\hat{G}_{3,j}^{(k_x)}\hat{Q}_m
\right]\langle E_{jm}\rangle
=i\lambda \sum_{j=-\infty}^{\infty}\sum_{m=-\infty}^{\infty}\hat{G}_{2,j}^{(k_x)}\hat{N}_m\langle E_{jm}\rangle.
\]

where

\[
\hat{G}_{1,n}^{(k_x)} = \int_0^{L_1} e^{-2in\pi x/L_1}\left(i\kappa c\eta_{0,x}\mathcal{S}_\kappa+k_x q_{0,x}\mathcal{C}_\kappa\right)dx,
\]
\[
\hat{G}_{2,n}^{(k_x)} = \int_0^{L_1} e^{-2in\pi x/L_1}\mathcal{C}_\kappa\,dx,
\]
\[
\hat{G}_{3,n}^{(k_x)} = \int_0^{L_1} e^{-2in\pi x/L_1}\mathcal{S}_\kappa\,dx.
\]

Each term in the double infinite sum contains the average value of

\[
E_{jm}=\exp\left[i x\left(\mu-k_x+m+j\right)\right].
\]

This average value is identically zero unless the quantity \(\mu-k_x+m+j\) is zero so that \(\langle E_{jm}\rangle=1\). In other words, the contribution from the integral is identically zero unless

\[
k_x=\mu+n,
\]

for some integer \(n\). Thus, the only contribution in the integral equation occurs when \(k_x\) is a shift of the original dual lattice. This allows us to collapse the double infinite sum to a single infinite sum given by

\[
\tag{3.14}
\begin{aligned}
&\sum_{m=-\infty}^{\infty}\left(\hat{G}_{1,n-m}^{(k(\mu))}+ic(i\mu+im)\hat{G}_{2,n-m}^{(k(\mu))}\right)\hat{N}_m\\
&\qquad+\sum_{m=-\infty}^{\infty}\left(\frac{k(\mu)}{\kappa}(i\mu+im)+\frac{i\rho^2}{\kappa}\right)\hat{G}_{3,n-m}^{(k(\mu))}\hat{Q}_m\\
&= i\lambda\sum_{m=-\infty}^{\infty}\hat{G}_{2,n-m}^{(k(\mu))}\hat{N}_m
\end{aligned}
\]

where \(k(\mu)=\mu+n\). The above equation holds for all \(n\in\mathbb{Z}\).

Combining the above equation with (3.12) yields a generalized bi-infinite eigenvalue problem for the spectrum of the linearized operator about the stationary traveling wave solutions. We define the quantity \(\hat{\mathbf{X}}\) as the bi-infinite vector of Fourier coefficients \(\hat{Q}_j\) and \(\hat{N}_j\) for all \(j\in\mathbb{Z}\):

\[
\hat{\mathbf{X}}=[\ldots,\hat{N}_{-1},\hat{N}_0,\hat{N}_1,\ldots,\hat{Q}_{-1},\hat{Q}_0,\hat{Q}_1,\ldots]^T.
\]

With this notation, we rewrite the generalized eigenvalue problem as

\[
\begin{bmatrix} A(\mu) & B(\mu) \\ C(\mu,\rho) & D(\mu,\rho) \end{bmatrix}\hat{\mathbf{X}}
=
\lambda
\begin{bmatrix} -I & S(\mu) \\ 0 & V(\mu,\rho) \end{bmatrix}\hat{\mathbf{X}}.
\]
