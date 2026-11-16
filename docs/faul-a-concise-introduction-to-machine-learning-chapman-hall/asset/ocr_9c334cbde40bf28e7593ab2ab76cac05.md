Let $\phi : \mathbb{R}^M \to \mathbb{R}^{\hat{M}}$ be the mapping from the original $M$ dimensional feature space to the higher $\hat{M}$ dimensional feature space. We now apply the support vector machine to the data in this higher dimensional space; i.e. we need to maximize

$L(\boldsymbol{\alpha}) = \sum_{n=1}^N \alpha_n - \frac{1}{2} \sum_{i=1}^N \sum_{n=1}^N \alpha_i \alpha_n c_i c_n \left( 1 + \phi(\mathbf{v}_i)^T \phi(\mathbf{v}_n) \right).$

Let $k : \mathbb{R}^M \times \mathbb{R}^M \to \mathbb{R}$ be defined as

$k(\mathbf{x}, \mathbf{y}) = \phi(\mathbf{x})^T \phi(\mathbf{y}).$

This is known as the *kernel function* or *kernel* for short. Using this notation, the objective function to be maximized becomes

$L(\boldsymbol{\alpha}) = \sum_{n=1}^N \alpha_n - \frac{1}{2} \sum_{i=1}^N \sum_{n=1}^N \alpha_i \alpha_n c_i c_n \left( 1 + k(\mathbf{v}_i, \mathbf{v}_n) \right),$

subject to $\alpha_i \ge 0, i = 1, \dots, N$. The classification is according to the sign of

$-b + \sum_{n=1}^N \alpha_n c_n \phi(\mathbf{v}_n)^T \phi(\mathbf{v}) = -b + \sum_{n=1}^N \alpha_n c_n k(\mathbf{v}_n, \mathbf{v}).$

We see the mapping $\phi$ never has to be evaluated, only the kernel function $k$ in both the maximization and classification.

The kernel trick can be applied to all linear classification methods to separate data which is not linearly separable. All methods reduce to evaluations of the kernel function $k$.

The kernel function was derived from a higher dimensional inner product. In the previous chapter, we viewed the inner product as a measure of the relationship between different samples. A new sample is classified according to whether it is more related to the support vectors of one class than the other. The kernel function gives a numeric value describing the relationship between two samples.

Such functions describing relationships between samples can be constructed. A necessary and sufficient condition that such a function be suitable for our purposes is that the $N \times N$ matrix $\mathbf{K}$ with $(m, n)$ entry equal to $k(\mathbf{x}_m, \mathbf{x}_n)$ is positive semi-definite for any $N$ and for any set $\{\mathbf{x}_1, \dots, \mathbf{x}_N\}$. It is known as *Gram* or *Gramian matrix*. The constant function $k(\mathbf{x}, \mathbf{y}) = c$ for positive $c$ is a valid kernel, since then for any vector $\mathbf{v} = (v_1, \dots, v_n)^T$

$\mathbf{v}^T \mathbf{K} \mathbf{v} = c \left( \sum_{n=1}^N v_n \right)^2 \ge 0.$