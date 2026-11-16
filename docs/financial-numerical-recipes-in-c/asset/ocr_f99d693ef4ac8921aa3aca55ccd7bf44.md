and covariance matrix V:

\(\mathbf{V} = \begin{bmatrix} \sigma(r_1, r_1) & \sigma(r_1, r_2) & \dots \\ \sigma(r_2, r_1) & \sigma(r_2, r_2) & \dots \\ \vdots & & \\ \sigma(r_n, r_1) & & \dots & \sigma(r_n, r_n) \end{bmatrix}\)

The covariance matrix V is assumed to be invertible.

A portfolio \(\rho\) is defined by a set of weights w invested in the risky assets.

\(\mathbf{w} = \begin{bmatrix} \omega_1 \\ \omega_2 \\ \vdots \\ \omega_n \end{bmatrix}\)

where \(w_i\) is the fraction of the investors wealth invested in asset \(i\). Note that the weights sum to one.

The expected return on a portfolio is calculated as

\(E[r_p] = \mathbf{w}'\mathbf{e}\)

and the variance of the portfolio is

\(\sigma^2(r_p) = \mathbf{w}'\mathbf{Vw}\)

# Example

An investor can invest in three assets with expected returns and variances as specified in the following table.

| t | Asset | E[r] | \(\sigma^2(r)\) |
|---|---|---|---|
| 1 | | 10% | 0.20 |
| 2 | | 11.5% | 0.10 |
| 3 | | 8% | 0.15 |

The three assets are independent (uncorrelated).

+   1. Determine the expected return and standard deviation of an equally weighted portfolio of the three assets

```
Matlab program:
e=[0.1 0.11 0.08]
V=[0.2 0.0 0.0; 0.0 0.1 0 ; 0 0 0.15]
w=1/3*[1 1 1]
er = w*e'
sigma=sqrt(w*V*w*')
Output from Matlab program:
e =
 0.10000 0.11000 0.08000
V =
 0.20000 0.00000 0.00000
 0.00000 0.10000 0.00000
 0.00000 0.00000 0.15000
w =
 0.33333 0.33333 0.33333
er = 0.096667
sigma = 0.22361
```