
where we used the fact that \((\mathbf{Dv}_i)^T \mathbf{Dv}_j = \lambda_i\), if \(i = j\) and zero otherwise. Thus the predictions are closest, if all eigenvectors with non-zero eigenvalues are used. Using the decomposition of \(\mathbf{t}\), we have

```
\((\mathbf{Dv}_i)^T \mathbf{t} = \sum_{k=1}^K a_k \mathbf{v}_i^T \mathbf{D}^T \mathbf{D} \mathbf{v}_k + \mathbf{v}_i^T \mathbf{D}^T \mathbf{a} = a_i \lambda_i,\)
```

where we again made use of the orthogonality. Inserting this into the distance between \(\mathbf{t}\) and \(\mathbf{f}\), we obtain

```
\(\|\mathbf{t} - \mathbf{f}\|^2 = \mathbf{t}^T \mathbf{t} - \sum_{i=1}^K a_i^2 \lambda_i.\)
```

If sparsity is required and not all eigenvectors can be used, those for which \(a_i^2 \lambda_i\) is largest should be chosen. However, this implicitly depends on the data \(\mathbf{t}\) via the coefficient \(a_i\), and can cause the model to not generalize well to unseen data. To avoid this, it is customary to choose the eigenvectors with the largest eigenvalues. It should be noted here that determining the eigenvectors and eigenvalues of a matrix is not a trivial matter in itself, especially if \(M\) is large.

Note that generating new regressors is equivalent to generating new features. These new features are linear combinations of the original features.

Principal component regression does not address the correlation with the regressand. The method presented in the next section does so.

## 8.9 Partial Least Squares

_Partial Least Squares (PLS)_ aims to maximize the correlation between regressors and regressand. This time a new set of regressors is generated iteratively as linear combinations of the original regressors; in the first iteration say

```
\(z_1 \mathbf{D}_1 + \dots + z_M \mathbf{D}_M = \mathbf{Dz}.\)
```

Without loss of generality, we can assume \(\|\mathbf{Dz}\| = 1\), since regressors are invariant to scaling.

The matrix \(\mathbf{D}^T \mathbf{t} \mathbf{t}^T \mathbf{D}\) is a symmetric, positive semi-definite \(M \times M\) matrix, since

```
\((\mathbf{D}^T \mathbf{t} \mathbf{t}^T \mathbf{D})^T = \mathbf{D}^T \mathbf{t} \mathbf{t}^T \mathbf{D} \text{ and } \mathbf{v}^T \mathbf{D}^T \mathbf{t} \mathbf{t}^T \mathbf{D} \mathbf{v} = (\mathbf{v}^T \mathbf{D}^T \mathbf{t})^2 \ge 0.\)
```

It has \(M\) non-negative eigenvalues and corresponding orthonormal eigenvectors \(\mathbf{v}_1, \dots, \mathbf{v}_M\), where the eigenvectors are ordered with regards to the corresponding eigenvalues from largest to smallest.

Now \(\mathbf{z} \in \mathbb{R}^M\), and thus can be expressed as a linear combination of these eigenvectors:

```
\(\mathbf{z} = \hat{z}_1 \mathbf{v}_1 + \dots + \hat{z}_M \mathbf{v}_M.\)
```

The square of the correlation between t and the new regressor Dz is

```
\left( \frac{t^T Dz}{||t|| ||Dz||} \right)^2 = \frac{1}{||t||^2} z^T D^T t t^T D z = \frac{1}{||t||^2} (\lambda_1 \hat{z}_1^2 + ... + \lambda_M \hat{z}_M^2).
```

This is maximal for \(\hat{z}_2 = ... = \hat{z}_M = 0\), since the length of z is fixed by the condition ||Dz|| = 1. Thus the first new regressor is t_1 = Dv_1 / ||Dv_1||. We know that Dv_1 != 0, since otherwise D^T t t^T D would only have zero eigenvalues, since \lambda_1 is the largest of the non-negative eigenvalues. Having generated t_1, we calculate,

```
D_1 = (I - t_1 t_1^T) D.
```

### Note

```
D_1 v_1 = (I - t_1 t_1^T) D v_1 = (I - t_1 t_1^T) D v_1 = (I - t_1 t_1^T) ||D v_1|| t_1 = ||D v_1|| (1 - ||t_1||^2) t_1 = 0.
```

This implies that the rank of D_1 is less than the rank of D, because a vector (v_1) which previously was not mapped to zero, now is mapped to zero.

Now, let v_2 with ||v_2|| = 1 be the eigenvector corresponding to the largest eigenvalue of D_1^T t t^T D_1. The second new regressor is t_2 = D_1 v_2 normalized such that ||t_2|| = 1. Again the correlation is maximal.

```
D_2 = (I - t_2 t_2^T) D_1,
```

and the process continues until D_r is a null matrix, i.e. its rank is zero. This will be achieved, since D_j maps v_j to zero, but D_{j-1} v_j is non-zero, and hence rank(D_j) <= rank(D_{j-1}) - 1.

PLS can be used for multivariate regression; that is the regressand has multiple components and measuring at x_1, ..., x_N gives rise to a matrix t with N rows. However, this is beyond this text. More information can be found in [20].

## 8.10 Regularization

Recall, we are trying to find suitable coefficients c minimizing ||t - Dc||^2 while avoiding unnecessary complexity which leads to over-fitting. This is achieved by introducing a penalty term \Omega(c) and minimizing

```
\frac{1}{2} ||t - Dc||^2 + \lambda \Omega(c),
```

where \Omega(c) >= 0 for all c and \Omega(0) = 0.

The penalty \Omega(c) is also known as the entropy measure. The parameter \lambda controls the trade-off between fitting the data and reducing complexity and has to be chosen well. Often, a model is obtained for different choices of \lambda, and the goodness of the model is assessed on a validation set. Note that if

$\lambda = 0$, we obtain the ordinary least squares solution, while if $\lambda = \infty, \mathbf{c} = 0$. The zero vector of coefficients is the least complex one. For $\lambda$ in between these two extremes, we are balancing between fitting a linear model and keeping the model complexity small. Note that we still explore the same model space as before, but the inclusion of $\Omega(\mathbf{c})$ gives preference to certain areas of the model space. The parameter $\lambda$ controls how strong this preference is.

In the following, norms which are different to the Euclidean norm ($L_2$ norm) are distinguished by subscripts. The choices for $\Omega(\mathbf{c})$ are numerous:

| $\Omega(\mathbf{c})$ | Regression method |
| :--- | :--- |
| $\|\mathbf{c}\|_0 = \text{number of nonzero elements in } \mathbf{c}$ | $L_0$ regularization |
| $\|\mathbf{c}\|_1 = \sum_{m=1}^M |c_m|$ | $L_1$ regularization Least Absolute Shrinkage and Selection Operator (LASSO) |
| $\frac{1}{2}\|\mathbf{c}\|^2 = \frac{1}{2} \sum_{m=1}^M c_m^2$ | $L_2$ regularization Ridge regression |
| $\lambda\|\mathbf{c}\|_1 + \frac{1-\lambda}{2}\|\mathbf{c}\|^2$ | Elastic net regularization |

$L_0$ regularization is an NP-hard problem. This means there is no known algorithm to solve this in polynomial time. The aim of $L_0$ regularization is to arrive at a sparse vector of coefficients, i.e. a vector where many entries are zero. That is only a few components of $\mathbf{c}$ are non-zero. If it is known that $\mathbf{c}$ is 1-sparse, i.e. only one component is non-zero, we have $\binom{M}{1}$ possibilities and each needs to be checked whether it is the minimum. Similarly, if we know $\mathbf{c}$ is $k$-sparse, $\binom{M}{k}$ possibilities need to be checked. However, we do not know beforehand how many components are non-zero. Hence, all $M$ possible values for $k$ need to be checked. The resulting complexity is

\(\sum_{k=1}^M \binom{M}{k} = 2^M - 1.\)

Since the size of the problem, $M$, appears in the exponent, the complexity is exponential. The time to find the solution increases exponentially with the size of the input. We encounter a different method to get a sparse solution when looking at Bayesian Learning in Section 8.13.

The $L_0$ regularization is related to the Bayesian Information Criterion (BIC) and the Akaike Information Criterion (AIC). These criteria are used to select the model structure, $k$ being the model parameter to be selected. For more information see [9].

The \( L_1 \) regularization has the disadvantage that in the case of perfect multicollinearity there is not a unique minimum, but a continuum of minima. For example, if two columns \( \mathbf{d}_i \) and \( \mathbf{d}_j \) are the same and \( c_i \) and \( c_j \) are nonzero coefficients in the minimal solution, then for any \( a \in [0, 1] \) replacing \( c_i \) by \( a(c_i + c_j) \) and replacing \( c_j \) by \( (1-a)(c_i + c_j) \) are also minimal.

If the columns of \( \mathbf{D} \) are orthogonal, then they are orthonormal, since we assume they are standardized. This means \( \mathbf{D}^T\mathbf{D} \) is the identity matrix. In this case, the solution to \( L_1 \) regularization can be found by *soft thresholding*. We minimize

\(\frac{1}{2}\|\mathbf{t} - \mathbf{Dc}\|^2 + \lambda\|\mathbf{c}\|_1 = \frac{1}{2}\mathbf{t}^T\mathbf{t} - \mathbf{c}^T\mathbf{D}^T\mathbf{t} + \frac{1}{2}\mathbf{c}^T\mathbf{c} + \lambda\|\mathbf{c}\|_1.\)

Since \( \mathbf{t}^T\mathbf{t} \) is independent of the variables of interest, the first term can be dropped. Furthermore, let \( \mathbf{c}^{\text{OLS}} \) be the ordinary least squares solution

\(\mathbf{c}^{\text{OLS}} = (\mathbf{D}^T\mathbf{D})^{-1}\mathbf{D}^T\mathbf{t} = \mathbf{D}^T\mathbf{t}.\)

Hence the minimization is equivalent to minimizing

\(-\mathbf{c}^T\mathbf{c}^{\text{OLS}} + \frac{1}{2}\mathbf{c}^T\mathbf{c} + \lambda\|\mathbf{c}\|_1 = \sum_{m=1}^M -c_m c_m^{\text{OLS}} + \frac{1}{2}c_m^2 + \lambda|c_m|,\)

where each summand can be minimized individually. That is, for each \( m \), we minimize

\(-c_m c_m^{\text{OLS}} + \frac{1}{2}c_m^2 + \lambda|c_m| = -c_m c_m^{\text{OLS}} + \frac{1}{2}c_m^2 + \lambda \text{sgn}(c_m)c_m,\)

where

\(\text{sgn}(c_m) = \begin{cases} +1 & \text{if } c_m > 0, \\ 0 & \text{if } c_m = 0, \\ -1 & \text{if } c_m < 0. \end{cases}\)

If \( c_m^{\text{OLS}} = 0 \), then \( c_m = 0 \) is minimal. Otherwise, the minimal \( c_m \) has to have the same sign as \( c_m^{\text{OLS}} \), since otherwise the sign could be flipped and a smaller value could be achieved. Thus, it is equivalent to minimize

\(-c_m c_m^{\text{OLS}} + \frac{1}{2}c_m^2 + \lambda \text{sgn}(c_m^{\text{OLS}})c_m.\)

Differentiating with respect to \( c_m \) and setting to zero gives

\(c_m = c_m^{\text{OLS}} - \lambda \text{sgn}(c_m^{\text{OLS}}) = \text{sgn}(c_m^{\text{OLS}})(|c_m^{\text{OLS}}| - \lambda).\)

To ensure that \( c_m \) has the same sign as \( c_m^{\text{OLS}} \), we set \( c_m = 0 \), if \( |c_m^{\text{OLS}}| < \lambda \). This effectively prunes the corresponding basis function. For \( \lambda = 0 \), we recover the ordinary least squares solution. If \( \lambda \) is chosen too large, all coefficients are set to zero.
