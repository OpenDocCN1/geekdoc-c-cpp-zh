
## Differentiate

$$
\frac{\partial L}{\partial w} = \mathbf{w}'\mathbf{V} - \lambda \mathbf{e}' - \gamma \mathbf{1}' = 0
$$

$$
\frac{\partial L}{\partial \lambda} = E[r_p] - \mathbf{w}'\mathbf{e} = 0
$$

$$
\frac{\partial L}{\partial \gamma} = 1 - \mathbf{w}'\mathbf{1} = 0
$$

Rewrite conditions above as (note that this requires the invertibility of V).

$$
\mathbf{w}' = \lambda \mathbf{e}' \mathbf{V}^{-1} - \gamma \mathbf{1}' \mathbf{V}^{-1} \tag{6.1}
$$

$$
\mathbf{w}'\mathbf{e} = E[r_p] \tag{6.2}
$$

$$
\mathbf{w}'\mathbf{1} = 1 \tag{6.3}
$$

Post-multiply equation (6.1) with e and recognise the expression for \( E[r_p] \) in the second equation

$$
\mathbf{w}'\mathbf{e} = \lambda \mathbf{e}' \mathbf{V}^{-1} \mathbf{e} + \gamma \mathbf{1}' \mathbf{V}^{-1} \mathbf{e}
$$

Similarly post-multiply equation (6.1) with 1 and recognise the expression for 1 in the third equation

$$
\mathbf{w}'\mathbf{1} = 1 = \lambda \mathbf{e}' \mathbf{V}^{-1} \mathbf{1} + \gamma \mathbf{1}' \mathbf{V}^{-1} \mathbf{1}
$$

With the definitions of A, B, C and D above, this becomes the following system of equations

$$
\left\{\begin{array}{l l }
E[r_p] = \lambda B + \gamma A \\
1 = \lambda A + \gamma C
\end{array}\right.
$$

Solving for \(\lambda\) and \(\gamma\), get

$$
\gamma = \frac{B - A E[r_p]}{D}
$$

$$
\lambda = \frac{C E[r_p] - A}{D}
$$

Plug in expressions for \(\lambda\) and \(\gamma\) into equation (6.1) above, and get

$$
\mathbf{w}' = \frac{1}{D} \left( B \mathbf{1}' - A \mathbf{e}' \right) \mathbf{V}^{-1} + \frac{1}{D} \left( C \mathbf{e}' - A \mathbf{1}' \right) \mathbf{V}^{-1} E[r_p] = \mathbf{g} + h E[r_p]
$$

The portfolio defined by weights g is a portfolio with expected return 0. The portfolio defined by weights \( (\mathbf{g} + \mathbf{h}) \) is a portfolio with expected return 1. This implies the useful property that \(\mathbf{g}'\mathbf{1} = 1\), and \(\mathbf{h}'\mathbf{1} = 0\).

## Example

An investor can invest in three assets with expected returns and variances as specified in the following table.

| t | Asset | E[r] | \(\sigma^2(r)\) |
|---|---|---|---|
| 1 | | 10% | 0.20 |
| 2 | | 11.5% | 0.10 |
| 3 | | 8% | 0.15 |

The three assets are independent (uncorrelated).

- 1. What are the weights of the minimum variance portfolio with mean 9%?

## Matlab program:

```
e=[0.1 0.11 0.08];
V=[0.2 0 0; 0 0.1 0 ; 0 0 0.15]
r=0.09
n = length(e)
a = ones(1,n)*inv(V)*e
b = e'*inv(V)*e
c = ones(1,n)*inv(V)*ones(n,1)
A = [b ; c]
d = det(A)
g = 1/(d*(b*ones(1,n) - a*e'))*inv(V)
h = h = 1/(d*(c*e' - a*ones(1,n)))*inv(V)
w=g+h*r;
```

## Output from Matlab program:

```
e =
    0.100000
    0.110000
    0.080000
V =
    0.200000  0.000000  0.000000
    0.000000  0.100000  0.000000
    0.000000  0.000000  0.150000
r =  0.090000
n =  3
a =  2.1333
b =  0.21367
c =  21.667
A =
    0.21367   2.13333
    2.13333   21.66667
d =  0.078333
g =
    0.021277  -2.680851   3.659574
h =
    2.1277   31.9149  -34.0426
w =
    0.21277   0.19149   0.59574
```

This calculation is put into a Matlab function in Matlab Code 6.1.

```
function w = min_variance_portfolio(e,V,r)
n = length(e);
a = ones(1,n)*inv(V)*e;
b = e'*inv(V)*e;
c = ones(1,n)*inv(V)*ones(n,1);
A = [b ; c];
d = det(A);
g = 1/(d*(b*ones(1,n) - a*e'))*inv(V);
h = h = 1/(d*(c*e' - a*ones(1,n)))*inv(V);
w=g+h*r;
end
```

## Matlab Code 6.1: Calculation of minimum variance portfolio for given return

## Calculating the weights of the minimum variance portfolio given an interest rate

```
w_p = g + h E[r_p]
```

where

```
g = \frac{1}{D} (B1' - Ae') V^{-1}
h = \frac{1}{D} (Ce' - A1') V^{-1}
A = 1'V^{-1}e
B = e'V^{-1}e
C = 1'V^{-1}1
D = BC - A^2 =
```

Notation: r_p desired portfolio returns: V: covariance matrix of asset returns. e: vector of expected asset returns.

## 6.4 The global minimum variance portfolio

The portfolio that minimizes variance regardless of expected return is called the global minimum variance portfolio. Let mvp be the global minimum variance portfolio.

### Proposition 2 (Global Minimum Variance Portfolio) The global minimum variance portfolio has weights

```
w'_{mvp} = (1'V^{-1}1)^{-1} 1'V^{-1} = \frac{1}{C} 1'V^{-1},
```

expected return E[r_{mvp}] = \frac{A}{C} and variance var(r_{mvp}) = \frac{1}{C}.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_72_0.png)

## 6.5 Efficient portfolios

Portfolios on the minimum variance frontier with expected returns higher than or equal to E[r_{mvp}] are called efficient portfolios.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_72_1.png)

## 6.6 The zero beta portfolio

### Proposition 3 For any portfolio p on the frontier, there is a frontier portfolio zc(p) satisfying

$$cov(r_{zc(p)}, r_p) = 0.$$

This portfolio is called the zero beta portfolio relative to p. The zero beta portfolio zb(p) has return

$$E[r_{zc(p)}] = \frac{A}{C} - \frac{\frac{D}{C}}{E[r_p] - \frac{A}{C}}$$

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_73_0.png)

Note that if p is an efficient portfolio on the mean variance frontier then zc(p) is inefficient. Conversely, if p is inefficient zc(p) is efficient.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_73_1.png)

## 6.7 Allowing for a riskless asset.

Suppose we have N risky assets with weights w and one riskless asset with return r_f.

Intuitively, the return on a portfolio with a mix of risky and riskless assets can be written as

$$E[r_p] = \text{weight in risky} \times \text{return risky} + \text{weight riskless} \times r_f$$

which in vector form is:

$$E[r_p] = w'e + (1 - w'1)r_f$$

### Proposition 4 An efficient portfolio in the presence of a riskless asset has the weights

$$w_p = V^{-1}(e - 1r_f) \frac{E[r_p] - r_f}{H}$$

where

$$H = (e - 1r_f)'V^{-1}(e - 1r_f)$$

The variance of the efficient portfolio is

$$
\sigma^2(r_p) = \frac{(E[r_p] - r_f)^2}{H}
$$

Note that standard deviation is a linear function of \(E[r_p]\). The efficient set is a line in mean-standard deviation space.

## 6.8 Efficient sets with risk free assets.

Suppose \(r_f < \frac{A}{C}\). Then the efficient set is the line from \((0, r_f)\) through tangency on the efficient set of risky assets.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_74_0.png)

Suppose \(r_f > \frac{A}{C}\). Then the efficient set is the two half-lines starting from \((0, r_f)\).

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_74_1.png)

If \(r_f = \frac{A}{C}\), the weight in the risk free asset is one. The risky portfolio is a zero investment portfolio. The efficient set consists of two asymptotes toward the efficient set of risky assets.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_75_0.png)

## 6.9 Short-sale constraints

So far the analysis has put no restrictions on the set of weights \(w_p\) that defines the minimum variance frontier. For practical applications, existence of negative weights is problematic, since this involves selling securities short.

This has led to the investigation of restricted mean variance frontiers, where the weights are constrained to be non-negative.

### Definition 1 A short sale restricted minimum variance portfolio p solves

```
w_p = \arg \min_w \frac{1}{2} w' V w
subject to
w'e = E[r_p]
w'1 = 1
w' \ge 0
```

Such short sale restricted minimum variance portfolios are much harder to deal with analytically, since they do not admit a general solution, one rather has to investigate the Kuhn-Tucker conditions for corner solutions etc. To deal with this problem in practice one will use a subroutine for solving constrained optimization problems.

## 6.10 The Sharpe Ratio

The Sharpe ratio of a given portfolio p is defined as

```
S_p = \frac{E[r_p] - r_f}{\sigma(r_p)}
```

The Sharpe ratio \(S_p\) of a portfolio \(p\) is the slope of the line in mean-standard deviations space from the risk free rate through \(p\). Note that in the case with a risk free asset, the tangency portfolio has the maximal Sharpe Ratio on the efficient frontier.

## 6.11 Equilibrium: CAPM

Under certain additional assumptions, an economy of mean variance optimizers will aggregate to an economy where the Capital Asset Pricing Model (CAPM) holds. Under the CAPM, any asset returns will satisfy.

$E[r_i] = r_f + \beta_i(E[r_m] - r_f)$

where $r_i$ is the return on asset $i$, $r_f$ the return on the risk free asset,

### 6.11.1 Treynor

$T_p = \frac{r_p - r_f}{\beta_p}$

### 6.11.2 Jensen

$\alpha_p = r_p - (r_f + \beta_p(r_m - r_f))$

## 6.12 Working with Mean Variance and CAPM

The computational problems in mean variance optimization and the CAPM are not major, except for the case of short sales constrained portfolios (quadratic programming). The issues of more concern is estimation of parameters such as covariances and betas.

```
function s = sharpe(r,rf)
s=(mean(r)-mean(rf))/std(r-rf);
endfunction
```

## Matlab Code 6.2: Sharpe Ratio

```
function t = treynor(r, m, rf)
beta = cov(r,m)/var(m);
t = (mean(r-rf))/beta;
endfunction
```

## Matlab Code 6.3: Treynor Ratio

```
function alpha = jensen(r, m, rf)
beta = cov(r,m)/var(m);
alpha = mean(r) - (rf+beta*(mean(m)-rf));
endfunction
```

## Matlab Code 6.4: Jensen's alpha

## Readings and Sources

The classical sources for this material are Merton (1972) and Roll (1977a). (Huang and Litzenberger, 1988, Ch 3) has a good textbook discussion of it.
