
Thus, the first three conserved quantities are

\[
s_0=\int_{\mathbb{R}^2} q(z)\,dz,
\]
\[
s_1=\int_{\mathbb{R}^2}\frac{1}{4}q(z)(\bar\partial^{-1}q)(z)\,dz,
\]
\[
s_2=\int_{\mathbb{R}^2}\left(\frac{1}{4}q(z)v(z)-\frac{1}{16}q\,\bar\partial^{-1}\!\left(q\,\bar\partial^{-1}q\right)\!(z)\right)dz,
\]

where with \(z=x+iy\) and \(\zeta=\zeta_1+i\zeta_2\),

\[
(\bar\partial^{-1}q)(z)=\frac{1}{\pi}\int_{\mathbb{R}^2}\frac{q(\zeta)\,d\zeta}{z-\zeta}.
\]

## 3. Inverse Scattering via Manakov Triples

In this section we develop the inverse scattering method to solve the Cauchy problem for the Novikov-Veselov (NV) equation at zero energy

\[
q_\tau=2\operatorname{Re}\!\left(\partial^3 q-\frac{3}{4}\partial(uq)\right),\qquad
\bar\partial u=\partial q,\qquad
q|_{\tau=0}=q_0
\]

for smooth Cauchy data \(q_0\) of conductivity type (see Definition 3.2). Note that our convention for the NV equation differs slightly from (1.1); the form used here is more convenient for the zero-energy inverse scattering formalism. This section should be regarded as expository and the material here is undoubtedly “well known to the experts” (see the original paper of Manakov [48] and see e.g. Boiti, Leon, Manna, and Pempinelli [9] for the NV equation), although we give an essentially self-contained and mathematically rigorous presentation. An extension of these ideas to broader classes of potentials will appear in [54], [55], and [69].

In this section, we draw on previous work of Lassas, Mueller, and Siltanen [44], Lassas, Mueller, Siltanen, and Stahel [45], and Perry [67], particularly for mapping properties of the scattering transform and its inverse on the space of smooth functions of conductivity type as defined below. The main ingredient in our analysis (as contrasted to [44,45,67]) is the systematic use of the Manakov triple representation for the NV equation.

To describe the Manakov triple representation, suppose that \(q\) is a smooth function of \(z\) and \(\tau\). Suppose that there is a smooth function \(u(z,\tau)\) with the property that \(\bar\partial u=\partial q\) (existence of such a function for suitable classes of \(q\) can be deduced from properties of the Beurling transform; see the Appendix). Define¹

\[
L=\partial\bar\partial-\frac{q}{4},
\tag{3.2}
\]

\[
A=\partial^3+\bar\partial^3-\frac{3}{4}\left(u\partial+\bar u\,\bar\partial\right),
\tag{3.3}
\]

\[
B=\frac{3}{4}\left(\partial u+\bar\partial\bar u\right),
\tag{3.4}
\]

and the DN method uses integration by parts to transform (3.6) into

\[
\mathbf{t}(k)=\int_{\partial\Omega}e^{i\bar{k}\bar{z}}(\Lambda_q-\Lambda_0)\psi(\cdot,k)\,dS(z),
\tag{3.7}
\]

where \(\Lambda_q\) is the *Dirichlet-to-Neumann map* defined below. A rigorous derivation of formulas (3.6) and (3.7) was given by Nachman in [58].

The LS method requires numerical evaluation of the *complex geometrical optics solutions* \(\psi(z,k)\). Numerically, it is better to solve the Lippmann-Schwinger equation for \(\mu\)

\[
\mu(z,k)=1-\int_{\Omega}g_k(z-w)q(w)\mu(w,k)\,dw.
\tag{3.8}
\]

A rigorous solvability analysis for equation (3.8) can be found in [56–58]. Here \(g_k\) is the fundamental solution satisfying \((-\Delta-4ik\partial)g_k(z)=\delta(z)\). The origin of \(g_k\) is Faddeev’s 1965 article [18]. Computationally, \(g_1(z)\) can be evaluated using the Matlab expression `exp(-1i*z).*real(expint(-1i*z))/(2*pi);` The symmetry relation \(g_k(z)=g_1(kz)\) extends this to all values \(k\neq0\). Note that \(g_k\) has a \(\log k\) singularity when \(k\to0\), causing numerical difficulties for \(k\) near zero.

Equation (3.8) is defined in the whole plane \(z\in\mathbb{R}^2\), so some kind of truncation is needed for practical computation. The first numerical computation of complex geometrical optics solutions was reported in [75] in the context of (3.8). That computation was used as a part of the first numerical implementation [76] of the \(\bar\partial\) method for electrical impedance tomography. A more effective approach for computing \(\mu\) is based on the periodization technique introduced by Gennadi Vainikko in [91]; see also [74, Section 10.5]. The adaptation of Vainikko’s method to equation (3.8) was first introduced in [50]. For more details see [51, Section 14.3].

Now let us turn to the DN method. This method has practical use in the \(\bar\partial\) reconstruction method for electrical impedance tomography. (See [51] and the relevant references therein.) We first define the Dirichlet-to-Neumann map \(\Lambda_q\) for the Dirichlet problem

\[
(-\Delta+q)u=0\ \text{in}\ \Omega,\qquad u|_{\partial\Omega}=f.
\tag{3.9}
\]

If zero is not a Dirichlet eigenvalue of \(-\Delta+q\) in \(\Omega\), the problem (3.9) has a unique solution \(u\) for given \(f\in H^{1/2}(S^1)\), and we set

\[
\Lambda_q f=\left.\frac{\partial u}{\partial\nu}\right|_{\partial\Omega},
\tag{3.10}
\]

where \(\partial/\partial\nu\) denotes differentiation with respect to the outward normal on \(\partial\Omega\).

Formula (3.7) requires the trace \(\psi(\cdot,k)|_{\partial\Omega}\). According to [58], the traces can be solved from the boundary integral equation

\[
\psi(z,k)|_{\partial\Omega}=e^{ikz}-\int_{\partial\Omega}G_k(z-w)(\Lambda_q-\Lambda_0)\psi(w,k)|_{\partial\Omega}\,dS(w),
\tag{3.11}
\]

if \(k\) is not an exceptional point of \(q\). Here \(G_k(z):=e^{ikz}g_k(z)\) is Faddeev’s Green function for the Laplace operator. For details of the numerical solution of (3.11) see [51, Section 15.3].

### 3.3. The Inverse Scattering Map

It turns out the NCGO solutions \(\mu(z,k)\) also solve a \(\bar\partial\)-problem in the \(k\) variable determined by \(\mathbf{t}(k)\). Letting

\[
\mathbf{t}^\sharp(k)=\frac{\mathbf{t}(k)}{4\pi\bar{k}},
\]

we have, for any \(p>2\):

**Lemma 3.5.** Suppose that \(q\) is a smooth potential of conductivity type, and let \(\mu(z,k)\) be the corresponding NCGO solutions. Then:

\[
\bar\partial_k\mu(z,k)=e_{-k}\mathbf{t}^\sharp(k)\overline{\mu(z,\bar{k})},
\qquad
\mu(z,\cdot)-1\in L^p(\mathbb{C}).
\]

Moreover, \(q(z)\) is recovered from \(\mathbf{t}\) and \(\mu(z,k)\) by the formula

\[
q(z)=\frac{4i}{\pi}\bar\partial_z\left(\int e_{-k}(z)\mathbf{t}^\sharp(k)\overline{\mu(z,k)}\,dk\right).
\]

**Remark 3.6.** This equation has at most one solution for each \(z\), provided only that \(\mathbf{t}^\sharp\in L^2\), by a standard uniqueness theorem for the \(\bar\partial\)-problem (see Brown-Uhlmann [11], Corollary 3.11).

The fact that \(\mu(z,k)\) obeys a \(\bar\partial\)-equation in the \(k\)-variable also implies a large-\(k\) asymptotic expansion for \(\mu(z,k)\).

**Lemma 3.7.** Suppose that \(q\) is a smooth potential of conductivity type, and let \(\mu(z,k)\) be the corresponding NCGO solution. Then

\[
\mu(z,k)\sim 1+\sum_{\ell\ge0}\frac{c_\ell(z)}{k^{\ell+1}},
\]

where

\[
c_0=-\frac{i}{4}\bar\partial^{-1}q,
\]

\[
c_1=-\frac14\partial\bar\partial^{-1}q+\frac{1}{16}\bar\partial^{-1}\!\left(q\,\bar\partial^{-1}q\right),
\]

and the remaining \(c_j\) are determined by the recurrence

\[
i\bar\partial c_{j+1}=\left(\frac{q}{4}-\partial\bar\partial\right)c_j.
\]

**Proof.** The coefficients in the asymptotic expansion may be computed recursively from the equation \(\bar\partial(\partial+ik)\mu=(q/4)\mu\) once the existence of the asymptotic expansion is established. To do so, note that

\[
\mu(z,k)=1+\frac{1}{\pi}\int_{\mathbb{C}}\frac{1}{k-\kappa}e_{-\kappa}\mathbf{t}^\sharp(\kappa)\overline{\mu(z,\kappa)}\,dm(\kappa).
\]

Writing

\[
(k-\kappa)^{-1}=k^{-1}\sum_{j=0}^{N}(\kappa/k)^j+(\kappa/k)^{N+1}\frac{1}{k-\kappa},
\]

we obtain an expansion of the desired form with

\[
c_j(z)=\frac{1}{\pi}\int\kappa^j e_{-\kappa}\mathbf{t}^\sharp(\kappa)\overline{\mu(z,\kappa)}\,dm(\kappa),
\]

and remainder

\[
\frac{1}{\pi}k^{-(N+1)}\int\frac{\kappa^{N+1}}{k-\kappa}e_{-\kappa}\mathbf{t}^\sharp(\kappa)\overline{\mu(z,\kappa)}\,dm(\kappa).
\]

Finally to obtain explicit formulae for the \(c_j\), we substitute the expansion (3.15) into (2.11) to obtain

\[
i\bar\partial c_0=\frac14 q,
\]

and the recurrence (3.18) from which (3.17) follows.

Motivated by these results, suppose given \(\mathbf{t}^\sharp\in\mathcal{S}(\mathbb{C})\) and let \(\mu(z,k)\) be the unique solution to (3.13). Define \(q\) by the reconstruction formula (3.14). Then the solution \(\mu\) of (3.13) obeys the partial differential equation

\[
\bar\partial(\partial+ik)\mu=\frac{q}{4}\mu,\qquad \lim_{|z|\to\infty}\mu(z,\cdot)-1=0.
\]

**Definition 3.8.** The map \(\mathcal{Q}:\mathbf{t}\to q\) defined by (3.13) and (3.14) is called the inverse scattering map.

We conclude this subsection by obtaining a full asymptotic expansion for \(\mu(z,k)\) which encodes relations between \(s\) and \(\mathbf{t}\).

**Lemma 3.9.** Suppose that \(q\) is a smooth potential of conductivity type, and let \(\mathbf{t}^\sharp\) be given by (3.12). Then the expansion

\[
\mu(z,k)\underset{|z|\to\infty}{\sim}1+\sum_{\ell\ge0}\left(\frac{a_\ell}{z^{\ell+1}}+e_{-k}\frac{b_\ell}{\bar z^{\ell+1}}\right)
\tag{3.19}
\]

holds, where:

\[
a_0=-i\bar\partial_k^{-1}\!\left(|\mathbf{t}^\sharp|^2\right),\qquad
b_0=i\mathbf{t}^\sharp,
\]

and the subsequent \(a_\ell,b_\ell\) are determined by the recurrence relations

\[
\bar\partial_k a_\ell=\mathbf{t}^\sharp\overline{b_\ell},\qquad
b_{\ell+1}=i\bar a_\ell\mathbf{t}^\sharp-i\bar\partial_k b_\ell.
\]

**Proof.** The existence of an expansion of the form (3.19) was already established in Lemma 2.1. To compute the coefficients, we substitute the asymptotic series into (3.13).

**Remark 3.10.** Comparing Lemmas 2.1 and 3.9, we see that

\[
s(k)=4\pi k\bar\partial_k^{-1}\!\left(|\mathbf{t}^\sharp|^2\right).
\]

### 3.4. Computation of Inverse Scattering Transforms

The first step in the computation of the inverse scattering map is to solve the \(\bar\partial\) equation

\[
\bar\partial_k\mu_\tau(z,k)=\frac{\mathbf{t}_\tau(k)}{4\pi\bar{k}}e_{-k}(z)\overline{\mu_\tau(z,k)}
\tag{3.20}
\]

with a fixed parameter \(z\in\mathbb{R}^2\) and requiring large \(|k|\) asymptotics \(\mu_\tau(z,\cdot)-1\in L^\infty\cap L^r(\mathbb{C})\) for some \(2<r<\infty\). Since \(q_0(z)\) is compactly supported and of conductivity type, by [44] the scattering transform \(\mathbf{t}_\tau(k)\) is in the Schwartz class,
