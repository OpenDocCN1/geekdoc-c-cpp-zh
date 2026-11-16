
```matlab
load fisheriris;
% extract two attributes
pl = meas(:,3); % petal length
pw = meas(:,4); % petal width
figure;
h1 = gscatter(pl, pw, species,'rgb','os');
legend('Setosa','Versicolor','Virginica','Location','best')
hold on
X = [pl,pw];
cls = ClassificationDiscriminant.fit(X,species,...
    'DiscrimType','quadratic');
% plot the classification boundaries
% retrieve the coefficients for the quadratic boundary between
% the first and second class (setosa and versicolor).
c = cls.Coeffs(1,2).Const;
l = cls.Coeffs(1,2).Linear;
q = cls.Coeffs(1,2).Quadratic;
% plot the curve c + [x1,x2]'*l + [x1,x2]*q*[x1,x2]' = 0;
F = @(x1,x2) c + l(1,1).*x1 + l(1,2).*x2 + q(1,1).*x1.^2 + ...
    (q(1,2)+q(2,1)).*x1.*x2 + q(2,2).*x2.^2;
h2 = ezplot(F,[.9 7.1 0 1]);
set(h2, 'Color', 'k');
% retrieve the coefficients for the quadratic boundary between
% the first and third class (versicolor and virginica).
c = cls.Coeffs(2,3).Const;
l = cls.Coeffs(2,3).Linear;
q = cls.Coeffs(2,3).Quadratic;
% plot the curve c + [x1,x2]'*l + [x1,x2]*q*[x1,x2]' = 0;
F = @(x1,x2) c + l(1,1).*x1 + l(1,2).*x2 + q(1,1).*x1.^2 + ...
    (q(1,2)+q(2,1)).*x1.*x2 + q(2,2).*x2.^2;
h3 = ezplot(F,[.5 7.0 0 2.5]);
set(h3, 'Color', 'k');
xlabel('Petal length');
ylabel('Petal width');
axis([0 8 0 3]);
title('');
```

Listing 5.1: Quadratic Discriminant Analysis.

![](img/d3c00252180686426c9e63ab889b535b_132_0.png)

Figure 5.1: Quadratic Discriminant Analysis.

This is exactly the equation of the line in the Linear Discriminant Analysis. In the following section, we look at the Quadratic Discriminant Analysis from a different angle by introducing artificial features and extending the feature space this way.

## 5.2 Kernel Trick

In the quadratic

$$v^T A v + v^T b + c = 0$$

the matrix A is symmetric, since A is the difference of covariance matrices which are symmetric. Assuming M = 2 and writing

$$A = \begin{pmatrix} A_{11} & A_{12} \\ A_{12} & A_{22} \end{pmatrix}, \quad b = \begin{pmatrix} b_1 \\ b_2 \end{pmatrix},$$

the boundary equation can be written as

$$A_{11} v_1^2 + 2 A_{12} v_1 v_2 + A_{22} v_2^2 + b_1 v_1 + b_2 v_2 + c = 0.$$

Now we can rearrange this as

$$( A_{11} \quad 2A_{12} \quad A_{22} \quad b_1 \quad b_2 ) \begin{pmatrix} v_1^2 \\ v_1 v_2 \\ v_2^2 \\ v_1 \\ v_2 \end{pmatrix} + c = 0.$$

![](img/d3c00252180686426c9e63ab889b535b_133_0.png)

![](img/d3c00252180686426c9e63ab889b535b_133_1.png)

Figure 5.2: Linearly inseparable data and their transformation to a higher dimensional space.

Letting $\mathbf{w}^T = ( A_{11} \quad 2A_{12} \quad A_{22} \quad b_1 \quad b_2 )$ and $\tilde{\mathbf{v}} = \begin{pmatrix} v_1^2 \\ v_1 v_2 \\ v_2^2 \\ v_1 \\ v_2 \end{pmatrix}$, this describes a linear boundary in a five-dimensional feature space

$$\mathbf{w}^T \tilde{\mathbf{v}} + c = 0.$$

In other words, we have augmented the feature space by three artificial features

- $v_1^2$
- $v_1 v_2$
- $v_2^2$

This is known as the *kernel trick*. The features are transformed to a higher dimensional feature space where the classes are linearly separable. We will see below that in practice this transformation is never performed.

Figure 5.2 shows artificial data, which cannot be separated by a line, and their transformation to a higher dimensional space, where they can be separated by a plane. We set $v_3 = \sqrt{v_1^2 + v_2^2}$, and the plane lies at $v_3 = 1$. Going back to two dimensions, $v_3^2 = v_1^2 + v_2^2 = 1$ is the unit circle in the $v_1, v_2$-plane.

To formalize this approach, recall that the Support Vector Machine classifies according to the sign of

$-b + \sum_{n=1}^N \alpha_n c_n \mathbf{v}_n^T \mathbf{v}_i$

where the bias $b$ is given by $- \sum_{n=1}^N \alpha_n c_n$ and where $c_i = \pm 1$ is the class label of sample $\mathbf{v}_i$. The $\alpha_i \ge 0$ for $i = 1, \dots, N$ maximize the function

$L(\boldsymbol{\alpha}) = \sum_{n=1}^N \alpha_n - \frac{1}{2} \sum_{i=1}^N \sum_{n=1}^N \alpha_i \alpha_n c_i c_n (1 + \mathbf{v}_i^T \mathbf{v}_n)$.

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

$$\mathbf{v}^T \mathbf{K} \mathbf{v} = c \left( \sum_{n=1}^N v_n \right)^2 \ge 0.$$

We also have positive semi-definiteness of K, if the kernel function is defined via an inner product in a higher dimensional space, because then

$$\mathbf{v}^T \mathbf{Kv} = \sum_{m,n=1}^N v_m \phi(\mathbf{x}_m)^T \phi(\mathbf{x}_n) v_n = \left( \sum_{m=1}^N v_m \phi(\mathbf{x}_m) \right)^T \left( \sum_{n=1}^N v_n \phi(\mathbf{x}_n) \right) = \| \sum_{n=1}^N v_n \phi(\mathbf{x}_n) \|^2 \ge 0.$$

Therefore the inner product itself is a valid kernel.

If A is a symmetric, positive semi-definite, \(M \times M\) matrix, then the function defined by

$$k(\mathbf{x}, \mathbf{y}) = \mathbf{x}^T \mathbf{Ay}$$

is a valid kernel function, since in this case

$$\mathbf{v}^T \mathbf{Kv} = \sum_{m,n=1}^N v_m \mathbf{x}_m^T \mathbf{A} \mathbf{x}_n v_n = \left( \sum_{m=1}^N v_m \mathbf{x}_m \right)^T \mathbf{A} \left( \sum_{n=1}^N v_n \mathbf{x}_n \right) \ge 0.$$

Similarly, if \(f : \mathbb{R}^M \to \mathbb{R}\) is any function and \(k : \mathbb{R}^M \times \mathbb{R}^M \to \mathbb{R}\) is a valid kernel, then

$$\sum_{m,n=1}^N v_m f(\mathbf{x}_m) k(\mathbf{x}_m, \mathbf{x}_n) f(\mathbf{x}_n) v_n = \mathbf{w}^T K \mathbf{w} \ge 0, \quad (5.1)$$

where \(\mathbf{w} = ((f(\mathbf{x}_1)v_1, \dots, f(\mathbf{x}_N)v_N)^T\). Therefore, the function defined by \(f(\mathbf{x})k(\mathbf{x}, \mathbf{y})f(\mathbf{y})\) is a kernel function.

Multiplying a valid kernel by a positive constant is obviously a kernel, as is the sum of two valid kernels. Also, the product of two valid kernels is a kernel. Let \(\{\mathbf{x}_1, \dots, \mathbf{x}_N\}\) be an arbitrary set. Let \(\mathbf{K}\) denote the Gram matrix of the product of kernels. Since the Gram matrices of the two kernels, which are the factors, are symmetric and positive semi-definite, they can be written as products \(\mathbf{A}^T \mathbf{A}\) and \(\mathbf{B}^T \mathbf{B}\) respectively. Thus, their \((m, n)\) entries are given by

$$\sum_{i=1}^N A_{mi} A_{ni} \quad \text{and} \quad \sum_{j=1}^N B_{mj} B_{nj}$$

respectively. Now, for an arbitrary vector \(\mathbf{v} = (v_1, \dots, v_n)^T\),

$$\mathbf{v}^T \mathbf{Kv} = \sum_{m,n=1}^N v_m K_{mn} v_n = \sum_{m,n=1}^N v_m \left( \sum_{i=1}^N A_{mi} A_{ni} \right) \left( \sum_{j=1}^N B_{mj} B_{nj} \right) v_n = \sum_{i,j=1}^N \left( \sum_{m=1}^N v_m A_{mi} B_{mj} \right) \left( \sum_{n=1}^N v_n A_{ni} B_{nj} \right) = \sum_{i,j=1}^N \left( \sum_{m=1}^N v_m A_{mi} B_{mj} \right)^2 \ge 0.$$
