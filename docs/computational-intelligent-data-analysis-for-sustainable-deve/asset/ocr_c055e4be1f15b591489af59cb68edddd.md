with sizes

$$\begin{bmatrix}1\times 1 & 1\times m \\ m\times 1 & m\times m\end{bmatrix} \tag{10A.4}$$

Then, the distribution of $y$ conditional on $\mathbf{x}=\mathbf{x}_k$ is multivariate normal with [19]

$$\underline{\mu}_{y\mid x_k}=\mu_y+\Sigma_{yx}\Sigma_{xx}^{-1}(\mathbf{x}_k-\mu_x) \tag{10A.5}$$

and covariance matrix

$$\underline{\sigma}_{y\mid x_k}=\Sigma_{yy}-\Sigma_{yx}\Sigma_{xx}^{-1}\Sigma_{xy} \tag{10A.6}$$