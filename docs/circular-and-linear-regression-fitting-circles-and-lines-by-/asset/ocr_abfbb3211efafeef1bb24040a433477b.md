are \(n+3\) independent parameters: three principal ones \((a, b, R)\) and one “latent” parameter for each data point.

First we specify the coordinates of the true points by

$$\tilde{x}_{i}=\tilde{\boldsymbol{a}}+\tilde{R} \cos \varphi_{i}, \quad \tilde{y}_{i}=\tilde{\boldsymbol{a}}+\tilde{R} \sin \varphi_{i}$$

where \(\varphi_{1}, \ldots, \varphi_{n}\) are the latent parameters (recall that we have used this formalism in Section 4.8). Now, under our standard assumptions (Cartesian functional model described in Section 6.1), the log-likelihood function is

$$\ln L=\text { const }-\frac{1}{2 \sigma^{2}} \sum_{i=1}^{n}\left(x_{i}-\tilde{x}_{i}\right)^{2}+\left(y_{i}-\tilde{y}_{i}\right)^{2}. \qquad(7.12)$$

According to the classical Cramer-Rao theorem, the covariance matrix of unbiased parameter estimators is bounded below by

$$\operatorname{Cov}\left(\hat{a}, \hat{b}, \hat{R}, \hat{\varphi}_{1}, \ldots, \hat{\varphi}_{n}\right) \geq \mathbf{F}^{-1},$$

where **F** is the Fisher information matrix, **F** \(=\)\(\)-**E**\((**H**\)), and **H** denotes the Hessian matrix consisting of the second order partial derivatives of \(\ln L\) with respect to the parameters.

Computing the second order partial derivatives of \((7.12)\) with respect to \(a, b, R\), and \(\varphi_{1}, \ldots, \varphi_{n}\) is a routine exercise which we omit. Taking their expected values (and using the obvious relations \(\mathbb{E}\left(x_{i}\right)=\tilde{x}_{i}\) and \(\mathbb{E}\left(y_{i}\right)=\tilde{y}_{i}\) gives the following results (where we suppress the common factor \(\sigma^{-2}\) for brevity)

$$\begin{aligned} & \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a^{2}}\right]=-n, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial b^{2}}\right]=-n, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial R^{2}}\right]=-n, \\ & \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a \partial R}\right]=-\sum \cos \varphi_{i}, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a \partial b}\right]=0, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial b \partial R}\right]=-\sum \sin \varphi_{i}, \\ & \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a \partial \varphi_{i}}\right]=R \sin \varphi_{i}, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial b \partial \varphi_{i}}\right]=-R \cos \varphi_{i}, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial R \partial \varphi_{i}}\right]=0, \end{aligned}$$

and lastly

$$\mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial \varphi_{i} \partial \varphi_{j}}\right]=-R^{2} \delta_{i j},$$

where \(\delta_{i j}\) denotes the Kronecker delta symbol. The Fisher information matrix now can be written as

$$\mathbf{F}=\boldsymbol{\sigma}^{-2}\left[\begin{array}{cc} \mathbf{K} & \mathbf{L}^{T} \\ \mathbf{L} & R^{2} \mathbf{I}_{n} \end{array}\right],$$

where

$$\mathbf{K}=\left[\begin{array}{ccc} n & 0 & \sum \cos \varphi_{i} \\ 0 & n & \sum \sin \varphi_{i} \\ \sum \cos \varphi_{i} & \sum \sin \varphi_{i} & n \end{array}\right]$$