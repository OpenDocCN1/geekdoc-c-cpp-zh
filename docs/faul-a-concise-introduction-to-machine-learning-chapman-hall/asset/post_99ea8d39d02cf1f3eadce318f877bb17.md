
## 4.2 Projections onto Subspaces

Each sample has two features and we can write these as vectors.

$$\mathbf{v}_1 = \begin{pmatrix} v_{11} \\ v_{12} \end{pmatrix} \quad \text{and} \quad \mathbf{v}_2 = \begin{pmatrix} v_{21} \\ v_{22} \end{pmatrix}$$

The length of a vector is the square root of the sum of the squares of the coordinates.

$$\|\mathbf{v}_2\| = \sqrt{v_{21}^2 + v_{22}^2}.$$

This is also known as the Euclidean norm or $L_2$ norm. Between two vectors an inner product, also known as a scalar product or dot product can be defined:

$$\mathbf{v}_1 \bullet \mathbf{v}_2 = \langle \mathbf{v}_1, \mathbf{v}_2 \rangle = v_{11}v_{21} + v_{12}v_{22}.$$

More generally, this can be viewed as a matrix product between the transpose of the first vector and the second vector.

$$\mathbf{v}_1 \bullet \mathbf{v}_2 = \mathbf{v}_1^T \mathbf{v}_2 = \begin{pmatrix} v_{11} & v_{12} \end{pmatrix} \begin{pmatrix} v_{21} \\ v_{22} \end{pmatrix} = v_{11}v_{21} + v_{12}v_{22}.$$

A $1 \times 2$ matrix times a $2 \times 1$ matrix is a $1 \times 1$ matrix.

A common technique to reduce a higher dimensional problem to a lower dimensional one where it can be solved more easily. In particular, we reduce the two dimensional problem to a one-dimensional one by projecting onto a line going through 0 and in the direction of a vector $\mathbf{w}$. The formula of the projection of a vector $\mathbf{v}$ onto $\mathbf{w}$ is given by

$$\text{proj}_{\mathbf{w}}(\mathbf{v}) = \frac{\mathbf{w}^T \mathbf{v}}{\|\mathbf{w}\|^2} \mathbf{w}$$

Figure 4.2 illustrates this.

We then seek a separation threshold $b$, also known as bias such that for $\mathbf{v}$

- $\mathbf{w}^T \mathbf{v} < b \Rightarrow \mathbf{v} \in C_0$,
- $\mathbf{w}^T \mathbf{v} > b \Rightarrow \mathbf{v} \in C_1$.

In Figure 4.2 the bias happens to be 0 for $\mathbf{v}_1$ being in class $C_0$ and $\mathbf{v}_2$ being in class $C_1$.

The task is to find the direction $\mathbf{w}$ and separation threshold $b$. $\mathbf{w}$ is also known as the vector of weights. The line vertical to $\mathbf{w}$ through $b$ should separate the classes. In three dimensions, a plane separates the data, while in higher dimensions it is a hyperplane. Naively choosing the coordinate axes is unsuitable as Figure 4.3 shows. One idea could be to use the line through the sample means of each class and the midpoint between sample means as separation threshold. The sample mean of class $C_i$ is

$$\mu_i = \frac{1}{N_i} \sum_{\mathbf{v} \in C_i} \mathbf{v}, \quad i = 0, 1. \tag{4.1}$$

![](img/d3c00252180686426c9e63ab889b535b_112_0.png)

Figure 4.2: Projection of v1 and v2 onto w.

The line through the sample means is then parametrized by

$l(a) = \mu_0 + a(\mu_1 - \mu_0)$.

For $a \in [0, 1]$ we are on the line segment between the sample means and thus the midpoint is given when $a = 1/2$, hence $b = \frac{1}{2}(\mu_0 + \mu_1)$.

This approach is illustrated in Figure 4.4 where both the projection line and the separation line perpendicular to the projection line through the mid-point between sample means is shown. However, it fails to take into account the variance within each class, that is how much and in which way the samples differ from the mean. In Figure 4.4 we have also drawn the 95% confidence ellipses and their axes. This means that 95% of the samples lie within the ellipses.

Naively, one could move the separation threshold to the intersection of the confidence ellipses. However, this is subjective and a different value of the confidence, e.g. 99%, would move this point. Also, since the two ellipses have their axes at different angles, it means that the projections of samples of one class are more spread out than the projections of the samples of the other class.

The goal is to find a line of projection such that:

- The projected means of each class are as far apart as possible,
- The projected samples of each class are as close together as possible.

In the next section we see how Fisher tackled this problem.

![](img/d3c00252180686426c9e63ab889b535b_113_0.png)

Figure 4.3: Projection onto the coordinate axes.

## 4.3 Fisher's and Linear Discriminant Analysis

Recall, the sample mean of $C_i$ is

$$\mu_i = \frac{1}{N_i} \sum_{v \in C_i} v.$$

To take into account the variation of the samples, we define the *sample covariance* of $C_i$ as

$$\Sigma_i = \frac{1}{N_i} \sum_{v \in C_i} (v - \mu_i)(v - \mu_i)^T. \tag{4.2}$$

The last expression in the above is an *outer product*. In two dimensions it is defined between two vectors $\mathbf{v}_1$ and $\mathbf{v}_2$ as

$$\mathbf{v}_1 \mathbf{v}_2^T = \begin{pmatrix} v_{11} \\ v_{12} \end{pmatrix} (v_{21} \ v_{22}) = \begin{pmatrix} v_{11}v_{21} & v_{11}v_{22} \\ v_{12}v_{21} & v_{12}v_{22} \end{pmatrix}$$

It can be viewed as a matrix product. A $2 \times 1$ matrix times a $1 \times 2$ matrix is a $2 \times 2$ matrix.

If $M$ is the number of features (in our example $M = 2$), then $\mu_i$ is a vector with $M$ elements and the $j^{th}$ entry is the mean of the $j^{th}$ feature of samples in class $C_i$. On the other hand, $\Sigma_i$ is an $M \times M$ matrix. The $(j, j)$ diagonal entry is the variance of the $j^{th}$ feature of samples in class $C_i$. The variance describes how spread the values of a feature are. The $(j, k)$ off-diagonal entry

![](img/d3c00252180686426c9e63ab889b535b_114_0.png)

Figure 4.4: Separation by line and 95 vertical to the connection between the sample means and 95% confidence ellipses.

is the covariance between the $j^{th}$ and $k^{th}$ feature of samples in class $C_i$. The covariance describes how much different features influence each other. The covariance matrix is in general *positive definite*, since

$$\vec{v}^T \Sigma \vec{v} = \frac{1}{N_i} \sum_{v \in C_i} \vec{v}^T (v - \mu_i) (v - \mu_i)^T \vec{v} = \frac{1}{N_i} \sum_{v \in C_i} [(v - \mu_i)^T \vec{v}]^2 \ge 0.$$

It is unlikely that the sum of squares equals zero, since this means that all samples shifted by the mean lie in a space orthogonal to $\vec{v}$. In this case, one of the dimensions of the feature space is redundant, and dimensionality reduction should be performed first. Positive definiteness implies that the matrix is non-singular and can be inverted, a property which we will use later.

Let $\mathbf{w}$ be the direction of the line of projection. The location of the line of projection can be neglected, since it cancels in the calculations. The mean of the projected samples in class $C_i$ is given by $\mathbf{w}^T \mu_i$, while the variance of the projected samples in class $C_i$ is given by $\mathbf{w}^T \Sigma_i \mathbf{w}$. We seek $\mathbf{w}$ such that

$$\|\mathbf{w}^T \mu_0 - \mathbf{w}^T \mu_1\|^2 = \mathbf{w}^T (\mu_0 - \mu_1) (\mu_0 - \mu_1)^T \mathbf{w}$$

is as large as possible. That is the projected means are as far apart as possible. This is known as the *between-class scatter* of the projected samples. At the same time, we want

$$\mathbf{w}^T \Sigma_0 \mathbf{w} + \mathbf{w}^T \Sigma_1 \mathbf{w} = \mathbf{w}^T (\Sigma_0 + \Sigma_1) \mathbf{w}$$

![](img/d3c00252180686426c9e63ab889b535b_115_0.png)

Figure 4.5: Fisher's Discriminant Analysis.

as small as possible, since then the projected samples are close to the projected mean. This is known as the *within-class scatter* of the projected samples. Depending on $\mathbf{w}$, Fisher defined the separation $\mathbf{w}$ achieves by

$$s(\mathbf{w}) = \frac{\mathbf{w}^T(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)^T\mathbf{w}}{\mathbf{w}^T(\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w}}.$$

This function needs to be maximized. Or in other words, we maximize the ratio of the variance between projected classes to the variance within projected classes.

The function s(w) takes its maximum, where the *gradient* vector vanishes. The gradient $\nabla s(\mathbf{w})$ is the vector formed by the derivatives of s(w) with respect to each of the components of $\mathbf{w}$. Using the quotient rule of differentiation, the formula given in Appendix A.2.3 and the symmetry of covariance matrices and outer products, the gradient is given by

$$2 \frac{(\mathbf{w}^T(\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w})(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)^T\mathbf{w} - ((\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)^T\mathbf{w})^2(\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w}}{(\mathbf{w}^T(\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w})^2} = 2 \frac{(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)^T\mathbf{w}}{\mathbf{w}^T(\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w}}(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1) - 2 \left( \frac{(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)^T\mathbf{w}}{\mathbf{w}^T(\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w}} \right)^2 (\boldsymbol{\Sigma}_0 + \boldsymbol{\Sigma}_1)\mathbf{w}.$$

Setting this to zero and rearranging, we arrive at:

$$\mathbf{w} = \frac{\mathbf{w}^T(\Sigma_0 + \Sigma_1)\mathbf{w}}{(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)^T\mathbf{w}}(\Sigma_0 + \Sigma_1)^{-1}(\boldsymbol{\mu}_0 - \boldsymbol{\mu}_1)$$
