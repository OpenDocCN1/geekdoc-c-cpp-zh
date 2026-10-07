The model-based estimator of the variance-covariance matrix of $\hat{eta}$ is $\left(\hat{\mathbf{D}}^	op\hat{\mathbf{V}}^{-1}\hat{\mathbf{D}}\right)^{-1}$. This is the GEE equivalent of the inverse of the Fisher information matrix that is often used in GLMs as an estimator of the covariance estimate of the maximum likelihood estimator of $\beta$. It is a consistent estimator of the covariance matrix of $\beta$ if the mean and the working correlation matrix are correctly specified. The "robust," empirical," or "sandwich" variance-covariance matrix is

$$\overline{	ext{Var}}(\hat{eta})} = \hat{\mathbf{H}}^	op\hat{\mathbf{G}}^{-1}\hat{\mathbf{H}}^{-1},$\ (9.4)

where $\hat{\mathbf{H}} = \left(\hat{\mathbf{D}}^	op\hat{\mathbf{V}}^{-1}\hat{\mathbf{D}}\right)$ and $\hat{\mathbf{G}} = \hat{\mathbf{D}}^	op\hat{\mathbf{V}}^{-1}(\hat{\mathbf{y}}-\hat{\mu})\hat{\mathbf{V}}^{-1}\hat{\mathbf{D}}$. The variance estimator (9.4) has the desirable property of being a consistent estimator of the covariance matrix of $\beta$, even if the working correlation matrix is misspecified. We refer to the "Details: GENMOD Procedure" of the SAS* documentation. For further information about robust variance estimate estimate the reader is referred to Liang and Zeger (1986), and Zeger and Liang (1988). Additional useful references are Zeger, Liang, and Albert (1988), Royall (1986), and White (1982). See also by Hardin and Hilbo (2003).

If $\mathbf{y}_j = (y_{j1}, y_{j2}, \dots, y_{jm_j})^\top$ represents a realization of the random vector $\mathbf{Y}_j = (Y_{j1}, Y_{j2}, \dots, Y_{jm_j})^\top$, the GENMOD procedure currently supports the following working correlation structures $R_j(\\alpha):$

| Working Correlation Structure | $R_j(\alpha)$ |
| :--- | :--- |
| Independent | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \ 0 & i \neq k \end{cases}$ |
| Exchangeable | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \ \alpha & i \neq k \end{cases}$ |
| Unstructured | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \ \alpha_{ik} & i \neq k \end{cases}$ |
| Autoregressive AR(1) | $\text{Corr}(Y_{ji}, Y_{j,i+t}) = \alpha^t$ $\text{for } t=0,1,2,\dots,m_j$ |
| m-dependent | $\text{Corr}(Y_{ji}, Y_{j,i+t}) = \begin{cases} 1 & t=0 \ \alpha_i & t=1,2,\dots,m ( (m \le m_j) \ 0 & t>m \end{cases}$ |
| Fixed | $\text{Corr}(Y_{ji}, Y_{jk}) = r_{ik}$ where $r_{ik}$ is the $(i,k)$-element of a constant, user-specified correlation matrix $R_0$ |