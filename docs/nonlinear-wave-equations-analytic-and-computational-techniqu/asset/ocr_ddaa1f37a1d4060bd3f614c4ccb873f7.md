and the DN method uses integration by parts to transform (3.6) into

(3.7) $$\mathbf{t}(k)=\int_{\partial\Omega} e^{i\bar{k}\bar{z}}(\Lambda_q-\Lambda_0)\psi(\cdot,k)\,dS(z),$$

where $\Lambda_q$ is the *Dirichlet-to-Neumann map* defined below. A rigorous derivation of formulas (3.6) and (3.7) was given by Nachman in [58].

The LS method requires numerical evaluation of the *complex geometrical optics solutions* $\psi(z,k)$. Numerically, it is better to solve the Lippmann-Schwinger equation for $\mu$

(3.8) $$\mu(z,k)=1-\int_{\Omega} g_k(z-w)q(w)\mu(w,k)\,dw.$$

A rigorous solvability analysis for equation (3.8) can be found in [56–58]. Here $g_k$ is the fundamental solution satisfying $(-\Delta-4ikd)g_k(z)=\delta(z)$. The origin of $g_k$ is Faddeev’s 1965 article [18]. Computationally, $g_1(z)$ can be evaluated using the Matlab expression “exp(-1i*z).*real(ex pint(-1i*z))/(2*pi);” The symmetry relation $g_k(z)=g_1(kz)$ extends this to all values $k\neq0$. Note that $g_k$ has a $\log k$ singularity when $k\to0$, causing numerical difficulties for $k$ near zero.

Equation (3.8) is defined in the whole plane $z\in\mathbb{R}^2$, so some kind of truncation is needed for practical computation. The first numerical computation of complex geometrical optics solutions was reported in [75] in the context of (3.8). That computation was used as a part of the first numerical implementation [76] of the $\bar{\partial}$ method for electrical impedance tomography. A more effective approach for computing $\mu$ is based on the periodization technique introduced by Gennadi Vainikko in [91]; see also [74, Section 10.5]. The adaptation of Vainikko’s method to equation (3.8) was first introduced in [50]. For more details see [51, Section 14.3].

Now let us turn to the DN method. This method has practical use in the $\bar{\partial}$ reconstruction method for electrical impedance tomography. (See [51] and the relevant references therein.) We first define the Dirichlet-to-Neumann map $\Lambda_q$ for the Dirichlet problem

(3.9) $$(-\Delta+q)u=0\text{ in }\Omega$$ $$u|_{\partial\Omega}=f.$$

If zero is not a Dirichlet eigenvalue of $-\Delta+q$ in $\Omega$, the problem (3.9) has a unique solution $u$ for given $f\in H^{1/2}(S^1)$, and we set

(3.10) $$\Lambda_q f=\left.\frac{\partial u}{\partial\nu}\right|_{\partial\Omega}$$

where $\partial/\partial\nu$ denotes differentiation with respect to the outward normal on $\partial\Omega$.

Formula (3.7) requires the trace $\psi(\cdot,k)|_{\partial\Omega}$. According to [58], the traces can be solved from the boundary integral equation

(3.11) $$\psi(z,k)|_{\partial\Omega}=e^{ikz}-\int_{\partial\Omega}G_k(z-w)(\Lambda_q-\Lambda_0)\psi(w,k)|_{\partial\Omega}\,dS(w),$$

if $k$ is not an exceptional point of $q$. Here $G_k(z):=e^{ikz}g_k(z)$ is Faddeev’s Green function for the Laplace operator. For details of the numerical solution of (3.11) see [51, Section 15.3].