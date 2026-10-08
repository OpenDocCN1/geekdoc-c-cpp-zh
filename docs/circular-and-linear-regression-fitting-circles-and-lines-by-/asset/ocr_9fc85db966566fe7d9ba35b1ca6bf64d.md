(recall that for the Taubin method $\mathbf{N}$ is data-dependent, but only its “true” value $\widetilde{\mathbf{N}}$ matters, because $\eta = \overline{\sigma}_{P}(\sigma^{2})$).

The left-hand side of (7.24) consists of a linear part ($\widetilde{\mathbf{M}}\boldsymbol{\Delta_{1}}\mathbf{A}+\boldsymbol{\Delta_{1}}\mathbf{A}\widetilde{\mathbf{M}}$) and a quadratic part ($\widetilde{\mathbf{M}}\boldsymbol{\Delta_{2}}\mathbf{A}+\boldsymbol{\Delta_{1}}\mathbf{M}\boldsymbol{\Delta_{1}}\mathbf{A}+\boldsymbol{\Delta_{2}}\mathbf{M}\widetilde{\mathbf{A}}$). The right-hand side is quadratic. Separating linear and quadratic terms gives

$\widetilde{\mathbf{M}}\boldsymbol{\Delta_{1}}\mathbf{A}+n^{-1}\overline{\mathbf{X}^{T}}\boldsymbol{\Delta_{1}\mathbf{X}\widetilde{\mathbf{A}}}=\mathbf{0}$ (7.25)

and, again omitting terms $\mathcal{O}_{P}(\sigma^{3})$, 

$\widetilde{\mathbf{M}}\boldsymbol{\Delta_{2}}\mathbf{A}+\boldsymbol{\Delta_{1}}\mathbf{M}\boldsymbol{\Delta_{1}}\mathbf{A}+\boldsymbol{\Delta_{2}}\mathbf{M}\widetilde{\mathbf{A}}=\eta\widetilde{\mathbf{N}\widetilde{\mathbf{A}}}.$ (7.26)

Note that $\widetilde{\mathbf{M}}$ is a singular matrix (because $\widetilde{\mathbf{M}}\widetilde{\mathbf{A}}=\mathbf{0}$), but whenever there are at least three distinct true points, they determine a unique true circle, thus the kernel of $\widetilde{\mathbf{M}}$ is one-dimensional, and it coincides with the one-dimensional vector space $\mathrm{span}(\widetilde{\mathbf{A}})$. Also, since we set $\|\widetilde{\mathbf{A}}\|=1$, we see that

$1 = \|\widetilde{\mathbf{A}} + \boldsymbol{\Delta_{1}}\mathbf{A}\|^{2} = \|\widetilde{\mathbf{A}}\|^{2} + 2\widetilde{\mathbf{A}}^{T}\boldsymbol{\Delta_{1}}\mathbf{A} + \mathcal{O}_{P}(\sigma^{2})$,

hence $\widetilde{\mathbf{A}}^{T}\boldsymbol{\Delta_{1}}\mathbf{A} = 0$, i.e., $\boldsymbol{\Delta_{1}}\mathbf{A}$ is orthogonal to $\widetilde{\mathbf{A}}$. Thus we can write

$\boldsymbol{\Delta_{1}}\mathbf{A}=-n^{-1}\widetilde{\mathbf{M}^{-}}\overline{\mathbf{X}^{T}}\boldsymbol{\Delta_{1}\mathbf{X}\widetilde{\mathbf{A}}},$ (7.27)

where $\widetilde{\mathbf{M}^{-}}$ denotes the Moore-Penrose pseudoinverse. Note that $\mathbb{E}(\boldsymbol{\Delta_{1}}\mathbf{A}) = 0$.

# **7.4 Variance and bias of algebraic circle fits**

Here we use our previous error analysis to derive explicit formulas for the variance and bias of the algebraic circle fits in the parameters $A, B, C, D$. The natural geometric parameters $a, b, R$ will be treated in Section 7.6.

**Variance of algebraic circle fits.** The variance, to the leading order, is

$\begin{aligned} \mathbb{E}\left[\left(\boldsymbol{\Delta_{1}}\mathbf{A}\right)\left(\boldsymbol{\Delta_{1}}\mathbf{A}\right)^{T}\right]= & n^{-2}\widetilde{\mathbf{M}^{-}}\overline{\mathbf{X}^{T}}\mathbb{E}\left[\boldsymbol{\Delta_{1}\mathbf{X}\widetilde{\mathbf{A}}\widetilde{\mathbf{A}}^{T}\boldsymbol{\Delta_{1}\mathbf{X}^{T}\overline{\mathbf{X}}}}\right]\widetilde{\mathbf{M}^{-}} \text { } & =n^{-2}\widetilde{\mathbf{M}^{-}}\mathbb{E}\left[\left(\sum_{i}\widetilde{\mathbf{X}_{i}}\boldsymbol{\Delta_{1}\mathbf{X}_{i}^{T}}\right)\widetilde{\mathbf{A}}\widetilde{\mathbf{A}}^{T}\left(\sum_{j}\boldsymbol{\Delta_{1}\mathbf{X}_{j}^{T}\overline{\mathbf{X}_{j}^{T}}}\right)\right]\widetilde{\mathbf{M}^{-}}, \end{aligned}$ (7.28)

where

$\overline{\mathbf{X}_{i}}=\left[\begin{array}{c} \overline{z_{i}} \\ \overline{x_{i}} \\ \overline{y_{i}} \\ 1 \end{array}\right] \quad \text { and } \quad \boldsymbol{\Delta_{1}\mathbf{X}_{i}}=\left[\begin{array}{c} 2\overline{x_{i}\delta_{i}}+2\overline{y_{i}\varepsilon_{i}} \\ \delta_{i} \\ \varepsilon_{i} \\ 0 \end{array}\right]$

denote the columns of the matrices $\overline{\mathbf{X}^{T}}$ and $\boldsymbol{\Delta_{1}\mathbf{X}^{T}}$, respectively. Observe that

$\begin{array}{lll} \mathbb{E}\left[\left(\boldsymbol{\Delta_{1}\mathbf{X}_{i}}\right)\left(\boldsymbol{\Delta_{1}\mathbf{X}_{j}}\right)^{T}\right]=\left\{\begin{array}{ccc} 0 & \text { whenever } & i \neq j \\ \sigma^{2}\overline{\mathbf{T}_{i}} & \text { whenever } & i=j \end{array}\right. \end{array}$