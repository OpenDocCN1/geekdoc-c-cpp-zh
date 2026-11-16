
The logarithm of the joint data likelihood is

$$\mathcal{L} = \log \prod_{n=1}^N p(\mathbf{v}_n, \mathbf{u}_n) = -\frac{1}{2} \sum_{n=1}^N \left[ (K+D) \log(2\pi) + \log(|\mathbf{D}|) + \mathbf{u}_n^T \mathbf{u}_n + (\mathbf{v}_n - \boldsymbol{\mu})^T \mathbf{D}^{-1} (\mathbf{v}_n - \boldsymbol{\mu}) - 2\mathbf{u}_n^T \mathbf{W}^T \mathbf{D}^{-1} (\mathbf{v}_n - \boldsymbol{\mu}) + \mathbf{u}_n^T \mathbf{W}^T \mathbf{D}^{-1} \mathbf{W} \mathbf{u}_n \right].$$

As before, we take the expectation with respect to the latent variables $\mathbf{u}_n$ which results in

$$\mathbb{E}[\mathcal{L}] = -\frac{1}{2} \sum_{n=1}^N \left[ (K+D) \log(2\pi) + \log(|\mathbf{D}|) + \text{tr}(\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]) + (\mathbf{v}_n - \boldsymbol{\mu})^T \mathbf{D}^{-1} (\mathbf{v}_n - \boldsymbol{\mu}) - 2\mathbb{E}[\mathbf{u}_n]^T \mathbf{W}^T \mathbf{D}^{-1} (\mathbf{v}_n - \boldsymbol{\mu}) + \text{tr}(\mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \mathbf{W}^T \mathbf{D}^{-1}) \right],$$

where the cyclic permutation property of the trace was used.

Differentiating this with respect to $\mathbf{W}$ using Appendices A.2.6 and A.2.9, gives

$$\frac{\partial}{\partial \mathbf{W}} \mathbb{E}[\mathcal{L}] = -\frac{1}{2} \sum_{n=1}^N \left[ -2 \mathbf{D}^{-1} (\mathbf{v}_n - \boldsymbol{\mu}) \mathbb{E}[\mathbf{u}_n]^T + 2 \mathbf{D}^{-1} \mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \right].$$

Setting this to zero, multiplying through with $\mathbf{D}$ from the left and solving for $\mathbf{W}$ results in the update formula

$$\mathbf{W}_{\text{new}} = \left[ \sum_{n=1}^N (\mathbf{v}_n - \boldsymbol{\mu}) \mathbb{E}[\mathbf{u}_n]^T \right] \left[ \sum_{n=1}^N \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \right]^{-1}, \quad (7.13)$$

which is exactly the same as before.

To differentiate with respect to $\mathbf{D}$, we first rewrite the expression for the expectation of the joint log likelihood using the cyclic permutation property of the trace,

$$\mathbb{E}[\mathcal{L}] = -\frac{1}{2} \sum_{n=1}^N \left[ (K+D) \log(2\pi) + \log(|\mathbf{D}|) + \text{tr}(\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]) + \text{tr} \left( [(\mathbf{v}_n - \boldsymbol{\mu})(\mathbf{v}_n - \boldsymbol{\mu})^T - 2(\mathbf{v}_n - \boldsymbol{\mu}) \mathbb{E}[\mathbf{u}_n]^T \mathbf{W}^T + \mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \mathbf{W}^T] \mathbf{D}^{-1} \right) \right].$$

This way we can use the derivative formulae in Appendices A.2.4, A.2.7 and A.2.10. The derivative with respect to D is therefore

$$\frac{\partial}{\partial \mathbf{D}} \mathbb{E}[\mathcal{L}] = -\frac{1}{2} \sum_{n=1}^N \left[ \frac{1}{|\mathbf{D}|} \mathbf{D}|\mathbf{D}|^{-1} \mathbf{D}^{-1} \text{diag}\left( (\mathbf{v}_n - \boldsymbol{\mu})(\mathbf{v}_n - \boldsymbol{\mu})^T \right. \right. \\
\left. \left. -2(\mathbf{v}_n - \boldsymbol{\mu}) \mathbb{E}[\mathbf{u}_n]^T \mathbf{W}^T + \mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \mathbf{W}^T \right] \mathbf{D}^{-1} \right].$$

Setting this to zero, multiplying through by D from both left and right and solving for D, gives the following update formula

$$\mathbf{D}_{\text{new}} = \text{diag}\left( \frac{1}{N} \sum_{n=1}^N (\mathbf{v}_n - \boldsymbol{\mu})(\mathbf{v}_n - \boldsymbol{\mu})^T \right. \\
\left. -2 \frac{1}{N} \sum_{n=1}^N (\mathbf{v}_n - \boldsymbol{\mu}) \mathbb{E}[\mathbf{u}_n]^T \mathbf{W}^T \right. \\
\left. + \frac{1}{N} \mathbf{W} \sum_{n=1}^N \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \mathbf{W}^T \right).$$

It is common to use the already updated W_new, when updating D_new. When inserting formula (7.13) into the left of the last line, the sum over E[u_n u_n^T], n=1,...,N, cancels with its inverse and the last line combines with the one above. Hence, the update formula is

$$\mathbf{D}_{\text{new}} = \frac{1}{N} \sum_{n=1}^N \text{diag} \left( (\mathbf{v}_n - \boldsymbol{\mu})(\mathbf{v}_n - \boldsymbol{\mu} - \mathbf{W}_{\text{new}} \mathbb{E}[\mathbf{u}_n])^T \right).$$

This can be viewed as the D-dimensional version of (7.12).

These updates depend on D and the previous W via the expectations, which are calculated in the E-step. To this end, the conditional probability distribution p(u|v) of the latent variable u given v has variance

$$\mathbf{\Sigma}_{\mathbf{u}|\mathbf{v}} = (\mathbf{W}^T \mathbf{D}^{-1} \mathbf{W} + \mathbf{I})^{-1},$$

which is independent of v, and mean

$$\boldsymbol{\mu}_{\mathbf{u}|\mathbf{v}} = \mathbf{\Sigma}_{\mathbf{u}|\mathbf{v}} \mathbf{W}^T \mathbf{D}^{-1} (\mathbf{v} - \boldsymbol{\mu}).$$

which depends on v. Therefore, the two calculations forming the E-step are

$$\mathbb{E}[\mathbf{u}_n] = \mathbf{\Sigma}_{\mathbf{u}|\mathbf{v}} \mathbf{W}^T \mathbf{D}^{-1} (\mathbf{v}_n - \boldsymbol{\mu})$$

and using (2.10)

$$\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] = \mathbf{\Sigma}_{\mathbf{u}|\mathbf{v}} + \mathbb{E}[\mathbf{u}_n] \mathbb{E}[\mathbf{u}_n]^T.$$

## 7.5 Kernel Principal Component Analysis

The previous three sections relied on the assumption that the data samples are related to latent variables in a lower dimensional space via a linear mapping as defined in (7.2). Geometrically, this means that the data lies close to a line, plane or hyperplane as illustrated in Figures 7.5 and 7.6. This assumption is, however, unrealistic in many practical applications.

The data samples may lie close to a K-dimensional manifold. A manifold is a set of points which locally resembles Euclidean space. An example for a two-dimensional manifold is the sphere. Flat-earthers succumb to the impression that locally the Earth does look flat. The sphere resembles a plane locally. Globally, however, it does not, because travelling continuously in one direction will return to the starting point. This is not possible on a plane. Figure 7.7a gives an example of data being close to the unit sphere. Lighter shaded data points lie behind the surface of the sphere.

It is possible to choose a mapping \(\phi : \mathbb{R}^D \rightarrow \mathbb{R}^D\) into a higher dimensional space such that the data then is linearly related to latent variables in a K-dimensional subspace. In Figure 7.7b, the data was first mapped to a four-dimensional space, by letting the fourth component be the sum of squares of the other three. Since the data lies approximately on the unit sphere, the fourth component will be close to one for all data samples. Thus the data lies on a hyperplane. After finding the first two principal components, the data is projected onto the plane given by these two principal components. This is shown in Figure 7.7b. That the two data sets are grouped towards the top or bottom, means that they can be separated along one principal component.

However, like in the kernel trick in Section 5.2, performing the mapping explicitly is avoided. Instead, all steps in the calculation use the kernel or kernel for short \(k : \mathbb{R}^D \times \mathbb{R}^D \rightarrow \mathbb{R}\) defined as

\(k(\mathbf{x}, \mathbf{y}) = \phi(\mathbf{x})^T \phi(\mathbf{y})\).

Let \(\mathbf{E}\) be the \(N \times N\) matrix with each entry being equal to one. This matrix can be used to mean centre a vector \(\mathbf{a}^T = (a_1, \dots, a_N)\) by

\(\mathbf{a}^T (\mathbf{I} - \frac{1}{N} \mathbf{E}) = \left( a_1 - \frac{1}{N} \sum_{n=1}^N a_n, \dots, a_N - \frac{1}{N} \sum_{n=1}^N a_n \right)\).

It can also be used to shift data samples so that their mean is zero. Let \(\phi(\mathbf{v}_1), \dots, \phi(\mathbf{v}_N) \in \mathbb{R}^D\) be the images under the mapping \(\phi\) of the data samples \(\mathbf{v}_1, \dots, \mathbf{v}_N \in \mathbb{R}^D\), which are known as the pre-images. Further, let \(\mathbf{\Phi}\) be the \(D \times N\) matrix whose columns are the vectors \(\phi(\mathbf{v}_1), \dots, \phi(\mathbf{v}_N)\), then

\(\mathbf{\Phi} (\mathbf{I} - \frac{1}{N} \mathbf{E}) = \left( \phi(\mathbf{v}_1) - \frac{1}{N} \sum_{n=1}^N \phi(\mathbf{v}_n), \dots, \phi(\mathbf{v}_N) - \frac{1}{N} \sum_{n=1}^N \phi(\mathbf{v}_n) \right)\),

since, for every element in each row of \(\mathbf{\Phi}\), we subtract the mean of that row of \(\mathbf{\Phi}\).

Recall that Principal Component Analysis calculates the covariance matrix \(\mathbf{\Sigma}\) of the data samples. In this context, it means the covariance matrix of the
