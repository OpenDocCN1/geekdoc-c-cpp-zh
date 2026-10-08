
where

$$\tilde{\mathbf{T}}_{i}=\left[\begin{array}{cccc} 4 \tilde{z}_{i} & 2 \tilde{x}_{i} & 2 \tilde{y}_{i} & 0 \\ 2 \tilde{x}_{i} & 1 & 0 & 0 \\ 2 \tilde{y}_{i} & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right] .$$

Now we rewrite (7.28) as

$$\begin{aligned} \mathbb{E}\left[\left(\Delta_{1} \mathbf{A}\right)\left(\Delta_{1} \mathbf{A}\right)^{T}\right] & =n^{-2} \tilde{\mathbf{M}}^{\leftarrow}\left[\sum_{i, j} \tilde{\mathbf{X}}_{i} \tilde{\mathbf{A}}^{T} \mathbb{E}\left[\left(\Delta_{1} \mathbf{X}_{i} \Delta_{1} \mathbf{X}_{j}^{T}\right) \tilde{\mathbf{A}} \tilde{\mathbf{X}}_{j}^{T}\right] \tilde{\mathbf{M}}^{\rightarrow} \\ & =n^{-2} \sigma^{2} \tilde{\mathbf{M}}^{\leftarrow}\left[\sum_{i} \tilde{\mathbf{X}}_{i} \tilde{\mathbf{A}}^{T} \tilde{\mathbf{T}}_{i} \tilde{\mathbf{A}} \tilde{\mathbf{X}}_{i}^{T}\right] \tilde{\mathbf{M}}^{\rightarrow} \end{aligned}$$

Note that

$$\tilde{\mathbf{A}}^{T} \tilde{\mathbf{T}}_{i} \tilde{\mathbf{A}}=\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}=\tilde{B}^{2}+\tilde{C}^{2}-4 \tilde{A} \tilde{D}$$

for each $i$, hence

$$\sum_{i} \tilde{\mathbf{X}}_{i} \tilde{\mathbf{A}}^{T} \tilde{\mathbf{T}}_{i} \tilde{\mathbf{A}} \tilde{\mathbf{X}}_{i}^{T}=\sum_{i}\left(\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}\right) \tilde{\mathbf{X}}_{i} \tilde{\mathbf{X}}_{i}^{T}=n\left(\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}\right) \tilde{\mathbf{M}} .$$

This gives

$$\mathbb{E}\left[\left(\Delta_{1} \mathbf{A}\right)\left(\Delta_{1} \mathbf{A}\right)^{T}\right]=n^{-1} \sigma^{2} \tilde{\mathbf{M}}^{\leftarrow}\left(\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}\right) . \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad(7.29)$$

Remarkably, the variance of algebraic fits does not depend on the constraint matrix $\mathbf{N}$, hence all algebraic fits have the same variance (to the leading order). In Section 7.6 we will derive the variance of algebraic fits in the natural circle parameters $(a,b, R)$ and see that it coincides with the variance of the geometric fit (7.6).

### Bias of algebraic circle fits

Since $\mathbb{E}\left(\Delta_{1} \mathbf{A}\right)=0$, it will be enough to find $\mathbb{E}\left(\Delta_{2} \mathbf{A}\right)$, and this will be done via (7.26). First we can write, following (7.23)

$$\eta=\tilde{\eta}+\Delta_{1} \eta+\Delta_{2} \eta+\mathscr{O}_{P}\left(\sigma^{3}\right) .$$

Premultiplying (7.22) by $\tilde{\mathbf{A}}^{T}$ yields

$$\eta=\frac{\tilde{\mathbf{A}}^{T} \mathbf{M} \mathbf{A}}{\tilde{\mathbf{A}}^{T} \mathbf{N} \mathbf{A}}=\frac{\tilde{\mathbf{A}}^{T} \Delta_{2} \mathbf{M} \tilde{\mathbf{A}}+\tilde{\mathbf{A}}^{T} \Delta_{1} \mathbf{M} \Delta_{1} \mathbf{A}}{\tilde{\mathbf{A}}^{T} \tilde{\mathbf{N}} \tilde{\mathbf{A}}}+\mathscr{O}_{P}\left(\sigma^{3}\right) ,$$

in particular we see that $\tilde{\eta}=\Delta_{1} \eta=0$ and $\eta=\mathscr{O}_{P}\left(\sigma^{2}\right)$. Thus by (7.26)

$$\Delta_{2} \mathbf{A}=\tilde{\mathbf{M}}^{\leftarrow}\left(\frac{\tilde{\mathbf{A}}^{T} \mathbf{L}}{\tilde{\mathbf{A}}^{T} \tilde{\mathbf{N}} \tilde{\mathbf{A}}} \tilde{\mathbf{N} \tilde{\mathbf{A}}-\mathbf{L}}\right)+\mathscr{O}_{P}\left(\sigma^{3}\right), \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad(7.30)$$

where

$$\mathbf{L}=\Delta_{2} \mathbf{M} \tilde{\mathbf{A}}+\Delta_{1} \mathbf{M} \Delta_{1} \mathbf{A} . \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad(7.31)$$

We note that (7.30) actually gives the component of $\Delta_2\mathbf{A}$ orthogonal to $\tilde{\mathbf{A}}$, but it is exactly what we need, because we set $\|\mathbf{A}\| = 1$. We can rewrite (7.31) as

where, according to (7.27),

$$\begin{aligned} \mathbf{R} & = \frac{1}{n}\bigg[\Delta_1\mathbf{X}^T\Delta_1\mathbf{X} + \hat{\mathbf{X}}^T\Delta_2\mathbf{X} + \Delta_2\mathbf{X}^T\hat{\mathbf{X}} \\ & \qquad \qquad - \frac{1}{n}(\hat{\mathbf{X}}^T\Delta_1\mathbf{X} + \Delta_1\mathbf{X}^T\hat{\mathbf{X}})\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}\bigg]. \end{aligned}$$

Thus the formula for the bias becomes

$$\mathbb{E}(\Delta_2\mathbf{A}) = \hat{\mathbf{M}}^{-}\begin{bmatrix} \tilde{\mathbf{A}}^T\mathbb{E}(\mathbf{R}\tilde{\mathbf{A}}) & \tilde{\mathbf{N}}\tilde{\mathbf{A}} - \mathbb{E}(\mathbf{R}\tilde{\mathbf{A}}) \\ \tilde{\mathbf{A}}^T\tilde{\mathbf{N}}\tilde{\mathbf{A}} \end{bmatrix} + \mathcal{O}(\sigma^4).$$

Next we find the mean value of (7.32), term by term. First,

$$\begin{aligned} \frac{1}{n}\mathbb{E}(\Delta_1\mathbf{X}^T\Delta_1\mathbf{X}) & = \frac{1}{n}\mathbb{E}\Big(\sum_i(\Delta_1\mathbf{X}_i)(\Delta_1\mathbf{X}_i)^T\Big) = \frac{\sigma^2}{n}\sum_i\tilde{\mathbf{T}}_i = \boldsymbol{\sigma}^2\tilde{\mathbf{T}}. \end{aligned}$$

Second, since $\mathbb{E}(\Delta_2\mathbf{X}_i) = (2\sigma^2, 0, 0, 0)^T$, we obtain

$$\begin{aligned} \frac{1}{n}\mathbb{E}(\hat{\mathbf{X}}^T\Delta_2\mathbf{X} + \Delta_2\mathbf{X}^T\hat{\mathbf{X}}) & = \frac{2\sigma^2}{n}\sum_i \begin{bmatrix} 2\tilde{z}_i & \tilde{x}_i & \tilde{y}_i & 1 \\ \tilde{x}_i & 0 & 0 & 0 \\ \tilde{y}_i & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 \end{bmatrix} = \boldsymbol{\sigma}^2(\tilde{\mathbf{T}} - \mathbf{P}). \end{aligned}$$

The above two terms combined constitute the essential bias, i.e.,

$$\mathbb{E}(\Delta_2\mathbf{A}) \overset{\mathrm{ess}}{=} \boldsymbol{\sigma}^2\hat{\mathbf{M}}^{-}\begin{bmatrix} \frac{\tilde{\mathbf{A}}^T(2\tilde{\mathbf{T}}-\mathbf{P})\tilde{\mathbf{A}}}{\tilde{\mathbf{A}}^T\tilde{\mathbf{N}}\tilde{\mathbf{A}}} & \tilde{\mathbf{N}}\tilde{\mathbf{A}} - (2\tilde{\mathbf{T}}-\mathbf{P})\tilde{\mathbf{A}} \end{bmatrix}.$$ 

### The entire $\mathcal{O}(\sigma^2)$ bias

We continue computing the mean value of (7.32):

$$\begin{aligned} \mathbb{E}(\hat{\mathbf{X}}^T\Delta_1\mathbf{X}\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}) & = \sum_i\mathbb{E}(\hat{\mathbf{X}}_i\Delta_1\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}_i\Delta_1\mathbf{X}_i^T) \ & = \sum_i\mathbb{E}(\hat{\mathbf{X}}_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\Delta_1\mathbf{X}_i\Delta_1\mathbf{X}_i^T) \ & = \boldsymbol{\sigma}^2\sum_i\hat{\mathbf{X}}_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\tilde{\mathbf{T}}_i. \end{aligned}$$

Similarly, we have

$$\mathbb{E}(\Delta_1\mathbf{X}^T\hat{\mathbf{X}}\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}) = \boldsymbol{\sigma}^2\sum_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}_i\tilde{\mathbf{T}}_i.$$

Thus the entire bias is given by

$$\mathbb{E}(\Delta_{2}\mathbf{A}) = \boldsymbol{\sigma}^{2}\mathbf{\widetilde{M}}-\left[\begin{array}{c}\widetilde{\mathbf{A}}^{T}\widetilde{\mathbf{H}}^{*}\widetilde{\mathbf{A}}\\ \widetilde{\mathbf{A}}^{T}\mathbf{N}\widetilde{\mathbf{A}}\end{array}\right. \widetilde{\mathbf{N}}\widetilde{\mathbf{A}}-\widetilde{\mathbf{H}}^{*}\widetilde{\mathbf{A}}\right]+\mathcal{O}\left(\sigma^{4}\right),\tag{7.39}$$

where

$$\mathbf{H}^{*}=2\mathbf{T}-\mathbf{P}+\frac{1}{n^{2}}\sum_{i}\left[\mathbf{X}_{i}\mathbf{X}_{i}^{T}\mathbf{M}^{-}\mathbf{T}_{i}+\mathbf{T}_{i}\mathbf{M}^{-}\mathbf{X}_{i}\mathbf{X}_{i}^{T}+\mathbf{X}_{i}^{T}\mathbf{M}^{-}\mathbf{X}_{i}\mathbf{T}_{i}\right].\tag{7.40}$$

We added the term $\mathbf{T}_{i}\mathbf{M}^{-}\mathbf{X}_{i}\mathbf{X}_{i}^{T}$ for the sole purpose of keeping $\mathbf{H}^{*}$ a symmetric matrix; its symmetry will be essential in the future. The added term does not affect (7.39), because $\mathbf{X}_{i}^{T}\widetilde{\mathbf{A}}=0$ for every $i=1,\ldots, n$.

### A simpler formula for the essential bias

Next we simplify the formula (7.36) for the essential bias. Note that

$$\widetilde{\mathbf{T}}_{i}\widetilde{\mathbf{A}}=\mathbf{P}\widetilde{\mathbf{A}}+2\widetilde{\mathbf{A}}\widetilde{\mathbf{X}}_{i}$$

for every $i=1,\ldots, n$, hence

$$\widetilde{\mathbf{T}}\widetilde{\mathbf{A}}=\mathbf{P}\widetilde{\mathbf{A}}+2\widetilde{\mathbf{A}}n^{-1}\sum_{i}\widetilde{\mathbf{X}}_{i}$$

and therefore $\widetilde{\mathbf{A}}^{T}\widetilde{\mathbf{T}}\widetilde{\mathbf{A}}=\widetilde{\mathbf{A}}^{T}\mathbf{P}\widetilde{\mathbf{A}}$. We also have

$$(2\widetilde{\mathbf{T}}-\mathbf{P})\widetilde{\mathbf{A}}=\mathbf{P}\widetilde{\mathbf{A}}+4\widetilde{\mathbf{A}}n^{-1}\sum_{i}\widetilde{\mathbf{X}}_{i}.$$

Also note that the vector $n^{-1}\sum_{i}\widetilde{\mathbf{X}}_{i}$ coincides with the last column of the matrix $\widetilde{\mathbf{M}}$, hence

$$n^{-1}\widetilde{\mathbf{M}}-\sum_{i}\widetilde{\mathbf{X}}_{i}=[0,0,0,1]^{T}.$$ 

Summarizing the above facts we reduce (7.36) to

$$\mathbb{E}(\Delta_{2}\mathbf{A})^{\mathrm{ess}}=\boldsymbol{\sigma}^{2}\mathbf{\widetilde{M}}-\left[\begin{array}{c}\widetilde{\mathbf{A}}^{T}\mathbf{P}\widetilde{\mathbf{A}}\\ \widetilde{\mathbf{A}}^{T}\widetilde{\mathbf{N}}\widetilde{\mathbf{A}}\end{array}\right. \widetilde{\mathbf{N}}\widetilde{\mathbf{A}}-\mathbf{P}\widetilde{\mathbf{A}}\right]-4\sigma^{2}\widetilde{\mathbf{A}}\left[0,0,0,1\right]^{T}.\tag{7.41}$$

## 7.5 Comparison of algebraic circle fits

**Bias of the Pratt and Taubin fits.** We have seen that all the algebraic fits have the same asymptotic variance (7.29). We will see below that their asymptotic variance coincides with that of the geometric circle fit. Thus the difference between all our circle fits should be traced to the higher order terms, especially to their essential biases.
