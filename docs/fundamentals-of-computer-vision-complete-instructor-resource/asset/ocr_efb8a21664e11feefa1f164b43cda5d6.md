![](bbox=[0.18, 0.11, 0.48, 0.33])

distance by \(d_l(\mathbf{n})\):

```
d_l(\mathbf{n}) = \mathbf{n}^T \mathbf{x}_l. \quad (10.42)
```

To find the best fitting straight line, minimize the sum of the squared perpendicular distances,

```
\epsilon = \sum_{l=1}^m d_l^2(\mathbf{n}) = \sum_{l=1}^m (\mathbf{n}^T \mathbf{x}_l)^2 = \sum_{l=1}^m (\mathbf{n}^T \mathbf{x}_l)(\mathbf{x}_l^T \mathbf{n}) = \mathbf{n}^T \left( \sum_{l=1}^m \mathbf{x}_l \mathbf{x}_l^T \right) \mathbf{n} \quad (10.43)
```

subject to the constraint that \(\mathbf{n}\) is a unit vector,

```
\mathbf{n}^T \mathbf{n} = 1. \quad (10.44)
```

Performing the constrained minimization using a Lagrange multiplier requires minimizing

```
\mathbf{n}^T \left( \sum_{l=1}^m \mathbf{x}_l \mathbf{x}_l^T \right) \mathbf{n} - \lambda (\mathbf{n}^T \mathbf{n} - 1). \quad (10.45)
```

Defining \(S = \sum_{l=1}^m \mathbf{x}_l \mathbf{x}_l^T\), differentiate as

```
\frac{\partial \epsilon}{\partial \mathbf{n}} \left( \mathbf{n}^T S \mathbf{n} - \lambda (\mathbf{n}^T \mathbf{n} - 1) \right). \quad (10.46)
```

Differentiating the quadratic form \(\mathbf{n}^T S \mathbf{n}\), we get \(2S\mathbf{n}\), and setting the derivative to zero results in

```
2S\mathbf{n} - 2\lambda \mathbf{n} = 0 \quad (10.47)
```

which is the same eigenvalue problem mentioned earlier. Thus we may state: The best fitting straight line passes through the mean of the set of data points, and will lie in the direction corresponding to the major eigenvector of the covariance of the set.

We have now seen two different ways to find the straight line that best fits the data: The method of least squares described in section 5.4.2, if applied to fitting a line rather than a plane, minimizes the vertical distance from the data points to the line. The method described in this section minimizes the perpendicular distance described by Eq. 10.43. The