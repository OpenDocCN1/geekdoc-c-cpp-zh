and the eigenvector equation is

\(\frac{1}{N} \mathbf{V}^T \mathbf{V} \mathbf{w}_d = \lambda_d \mathbf{w}_d.\)

Multiplying through with \(\mathbf{V}\) it becomes

\(\frac{1}{N} (\mathbf{V} \mathbf{V}^T) \mathbf{V} \mathbf{w}_d = \lambda_d \mathbf{V} \mathbf{w}_d.\)

So \(\mathbf{V} \mathbf{w}_d\) is an eigenvector of \(\mathbf{V} \mathbf{V}^T / N\). If \(D > N\), instead of finding the \(K\) largest eigenvalues and eigenvectors of \(\mathbf{\Sigma}\), it is easier to find the \(K\) largest eigenvalues and eigenvectors of \(\mathbf{V} \mathbf{V}^T / N\) and then transform these eigenvectors back and normalize them. This makes sense, if the data lies in a subspace of much lower dimension which needs to be found.

# 7.2 Probabilistic View

It is helpful to think about the process which generates the data. The assumption is that \(\mathbf{v} \in \mathbb{R}^D\) is related to \(\mathbf{u} \in \mathbb{R}^K\) via a linear mapping. More formally we are trying to find a \(D \times K\) matrix \(\mathbf{W}\), which has full rank, and \(\mathbf{m} \in \mathbb{R}^D\), such that

\(\mathbf{v} = \mathbf{W} \mathbf{u} + \mathbf{m} + \boldsymbol{\epsilon}.\) (7.2)

We can assume that the columns of \(\mathbf{W}\) are orthogonal to each other. If not, orthogonal columns can be achieved by using for example the Gram-Schmidt algorithm in [12] and a suitable basis transformation in \(\mathbb{R}^K\). \(\boldsymbol{\epsilon}\) is normally distributed noise with zero mean and covariance matrix \(\sigma^2 \mathbf{I}\). This is known as an *isotropic* or *spherical covariance matrix*. The noise explains why the data samples do not exactly lie in a lower dimensional subspace. Further, we assume that \(\mathbf{u}\) follows a normal distribution with mean \(\bar{\mathbf{m}}\) and covariance matrix \(\mathbf{S}\).

If a more general distribution for \(\mathbf{u}\) is assumed, then the technique arising from this is known as *Independent Component Analysis (ICA)*. Such a more general distribution could be one which factorizes as

\(p(\mathbf{u}) = \prod_{k=1}^K p(u_k),\)

where each \(u_k\) follows the distribution given by

\(p(u_k) = \frac{2}{\pi(\exp(u_k) + \exp(-u_k))}.\)

This distribution has a larger kurtosis than the normal distribution, often displayed in real world applications. A thorough treatment of Independent Component Analysis is given in [23]. In this text, however, we continue to assume that \(\mathbf{u}\) has a normal distribution.

The linear transformation of a normally distributed variable is also normally distributed with mean \(\mathbf{m} + \mathbf{W} \bar{\mathbf{m}}\) and covariance matrix \(\mathbf{W} \mathbf{S} \mathbf{W}^T\). Since \(\mathbf{S}\) is symmetric, it can be diagonalized by an orthogonal matrix \(\mathbf{Q}\) such that \(\mathbf{S} = \mathbf{Q} \mathbf{D} \mathbf{Q}^T\), where \(\mathbf{D}\) is a diagonal matrix with positive entries, since \(\mathbf{S}\)