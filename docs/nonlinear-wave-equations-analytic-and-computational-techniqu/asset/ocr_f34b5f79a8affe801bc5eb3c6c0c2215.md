(20) \(\int_{0}^{2\pi} e^{-ikx} \left[i \cosh(k(\eta + h))f(x) - \sinh(k(\eta + h))\mathcal{H}(\eta, D)\{f(x)\}\right] dx = 0,\)

where $k \in \mathbb{Z}$.

The operator $\mathcal{H}(\eta)\{f\}$ may either be numerically determined from the above expression or expressed as a Taylor series expansion about $\eta = 0$ (see [9, 13] for more details). Alternately, one may use standard solvers for Laplace’s equation to determine $\mathcal{H}(\eta)\{f\}$. Here we briefly outline the Taylor series of the operator expanded about the zero-amplitude solution $\eta = 0$.

To determine a Taylor series expression for $\mathcal{H}(\eta, D)$, we assume that $\mathcal{H}(\eta, D)$ has a series representation in $\eta$ of the form

\(\mathcal{H}(\eta, D)\{f\} = \sum_{j=0}^{\infty} \mathcal{H}_j(\eta, D)\{f\},\)

where each $\mathcal{H}_j(\eta, D)$ is homogeneous of order $j$ in $\eta$, i.e. $\mathcal{H}_j(\lambda \eta, D) = \lambda^j \mathcal{H}_j(\eta, D)$. A calculation similar to the one presented in [2] allows us to determine the following recursive relationship for $\mathcal{H}_j(\eta, D)$ in terms of lower-order terms:

(21) \(\int_{0}^{2\pi} e^{-ikx} \mathcal{H}_j(\eta, D)\{f\} dx = i \int_{0}^{2\pi} e^{-ikx} \frac{(k\eta)^j}{j!} \left[ \begin{array}{c} \coth(kh); \quad j \text{ even} \\ 1; \quad j \text{ odd} \end{array} \right] f dx - \int_{0}^{2\pi} e^{-ikx} \sum_{m=1}^{j} \left( \mathcal{H}_{j-m}(\eta)\{f\} \frac{(k\eta)^m}{m!} \left[ \begin{array}{c} 1; \quad m \text{ even} \\ \coth(kh); \quad m \text{ odd} \end{array} \right] \right) dx.\)

In the above, we have used the brackets [ ] as a conditional multiplier at the appropriate index of summation. Thus, for a suitable function $f(x)$, we can determine $\mathcal{H}(\eta)\{f\}$ through either (20) or (21).

REMARK 2. From the relationship given by (21), it is clear that $\mathcal{H}(\eta)$ is a linear operator acting on $f(x)$. Specifically, $\mathcal{H}(\eta)\{f + g\} = \mathcal{H}(\eta)\{f\} + \mathcal{H}(\eta)\{g\}$, and $\mathcal{H}(\eta)\{\alpha f\} = \alpha \mathcal{H}(\eta)\{f\}$ for any scalar $\alpha$. Of course, the operator $\mathcal{H}(\eta)$ may be defined abstractly through the solution of the boundary-value problem (17-19). Using standard techniques it is possible to show this operator acts linearly on the Neumann condition, much as the classical Dirichlet-to-Neumann operator is proved a bounded linear operator [5].

# 4.2. Relating the surface and the wave-speed.

Returning to the problem of interest, assume that $(q_x, \eta, c)$ is a solution set to Equations (2-5) and the quantity $-c\eta_x$ is the normal derivative of the potential due to (4). Recalling that $q_x$ is the tangential derivative of the velocity potential at the free-surface, we have

(22) \(\mathcal{H}(\eta)\{-c\eta_x\} = q_x.\)

Substituting $q_x = \mathcal{H}(\eta)\{-c\eta_x\}$ into the Bernoulli equation at the free-surface given by (7), we find

(23) \(-c\mathcal{H}(\eta)\{-c\eta_x\} + \frac{1}{2} \left(\mathcal{H}(\eta)\{-c\eta_x\}\right)^2 + g\eta - \frac{1}{2} \frac{\eta_x^2 \left(\mathcal{H}(\eta)\{-c\eta_x\} - c\right)^2}{1 + \eta_x^2} = 0.\)