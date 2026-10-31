
$\rho_k=\rho_1(\phi_1^{k-1})$.

for $k\geq 2$. Now, in order to use **Equation 3.107** for $k=0$ and $1$ it is necessary to find $\psi_1$. For an ARMA(1,1), $\psi_1=\phi_1-\theta_1$ (see **Equation 3.116**). So **Equation 3.107** becomes

$$\begin{aligned}
\gamma_0&=\phi_1\gamma_1-\sigma_a^2\bigl(-1+\theta_1(\phi_1-\theta_1)\bigr),\\
\gamma_1&=\phi_1\gamma_0-\sigma_a^2\theta_1,
\end{aligned}\tag{3.111}$$

and $\gamma_k=\phi_1\gamma_{k-1}$, $k>1$. Solving **Equation 3.111** for $\gamma_0$ and $\gamma_1$ yields

$$\gamma_0=\frac{1-2\theta_1\phi_1+\theta_1^2}{1-\phi_1^2}\sigma_a^2$$

and

$$\gamma_1=\frac{(\phi_1-\theta_1)(1-\phi_1\theta_1)}{1-\phi_1^2}\sigma_a^2$$

so that

$$\rho_1=\frac{(\phi_1-\theta_1)(1-\phi_1\theta_1)}{1-2\phi_1\theta_1+\theta_1^2}.$$ \tag{3.112}

*The ARMA(1,1) model of Example 3.16 revisited:* Consider again the ARMA(1,1) model $(1-0.95B)X_t=(1-0.8B)a_t$ in **Equation 3.90**. From **Equation 3.112**, we obtain $\rho_1=0.3$, and from **Equation 3.110**, it follows that $\rho_k=0.3(0.95^{k-1})$ for $k\geq 2$. Note that while $\rho_1$ does not satisfy the linear homogeneous difference equation in **Equation 3.108**, it does satisfy **Equation 3.110** since $\rho_1=0.3(0.95^0)=0.3$.

## 2. ARMA(2,1) model

Consider the ARMA(2,1) model given by

(1 - φ1 B - φ2 B²) X_t = (1 - θ1 B) a_t.

For this model,

γ0 = [2 φ1 θ1 - (1 - φ2)(1 + θ1²)] / [(1 + φ2)(φ1² - (1 - φ2)²)] σ_a², (3.113)

and

γ1 = [(φ1 - θ1)(1 - φ1 θ1) + φ2² θ1] / [(1 + φ2)((1 - φ2)² - φ1²)] σ_a². (3.114)

For k > 1, γk can be obtained using the recursion γk = φ1 γk-1 + φ2 γk-2 given starting values γ0 and γ1.

## 3. ARMA(1,2) model

For the ARMA(1,2) model

(1 - φ1 B) X_t = (1 - θ1 B - θ2 B²) a_t.

it can be shown that

γ0 = [1 - 2 φ1 θ1 - 2 φ1 θ2 (φ1 - θ1) + θ1² + θ2²] / [1 - φ1²] σ_a²
γ1 = [(1 - θ2 - φ1² θ2 - φ1 θ1)(φ1 - θ1) + φ1 θ2²] / [1 - φ1²] σ_a²
and
γ2 = [φ1[(1 - θ2 - φ1² θ2 - φ1 θ1)(φ1 - θ1) + φ1 θ2²] - θ2 + φ1² θ2²] / [1 - φ1²] σ_a²

Again, the autocovariances for k > 2 can be found using the recursive formula γ_k = φ₁γ_{k-1}.

### 3.3.5 ψ-Weights of an ARMA(p,q)

We have shown that an ARMA(p,q) process can be expressed in the linear filter form, X_t = Σ_{k=0}^∞ ψ_k a_{t-k} In this section, we discuss calculation of the ψ-weights using three methods: (a) equating coefficients, (b) division, and (c) finding a general expression using Theorem 3.1.

- 1. Finding ψ-weights by equating coefficients: Since a stationary ARMA(p,q) process can be written in the form X_t = ψ(B)a_t where ψ(B)= φ^{-1}(B)θ(B), we have the relationship φ(B)ψ(B)=θ(B), or in the expanded form

(1 - φ₁B - ⋯ - φ_pB^p)(1 + ψ₁B + ψ₂B² + ⋯) = (1 - θ₁B - ⋯ - θ_qB^q). (3.115)

Equating the coefficients of B^j in Equation 3.115 displays the relationship among the φ's, θ's, and ψ's. In particular, equating coefficients of B^j yields

ψ₁ - φ₁ = -θ₁
ψ₂ - φ₁ψ₁ - φ₂ = -θ₂
⋮
ψ_j - φ₁ψ_{j-1} - φ₂ψ_{j-2} - ⋯ - φ_j = -θ_j, (3.116)

where ψ₀ = 1, θ_k = 0 for k > q, and φ_k = 0 for k > p. The equations in Equation 3.116 can be rearranged to provide a recursive scheme for calculating the ψ-weights. Namely,

ψ₁ = φ₁ - θ₁
ψ₂ = φ₁ψ₁ + φ₂ - θ₂
⋮
ψ_j = φ₁ψ_{j-1} + φ₂ψ_{j-2} + ⋯ + φ_j - θ_j, (3.117)

be left as an exercise (see Problem 3.31).

### 3.3.6 Approximating ARMA(p,q) Processes Using High-Order AR(p) Models

We have discussed the fact that the stationary and invertible ARMA(p,q) model φ(B)X_t = θ(B)a_t can be written as the infinite-order AR process θ^{-1}(B)φ(B)X_t = a_t. Thus, an ARMA(p,q) model can often be well approximated using a high-order AR(p) model. For this reason, some time series analysts use the approach of always fitting AR models to data since parameter estimation and model identification tend to be more difficult when MA parameters are included in a model. On the other hand, some analysts prefer the ARMA(p,q) model since it often contains fewer parameters (is more parsimonious) than an AR model fit to the same data set. In this text, we will cover parameter estimation, forecasting, etc., in the generality provided by the ARMA(p,q) model. However, in practice, we will often restrict ourselves to AR(p) models.

An example of this trade-off between a parsimonious ARMA(p,q) model and a high-order AR(p) model is illustrated in Example 4.1, where theoretical justification is used to show that an ARMA(2,2) model is a good approximating model for harmonic signal-plus-noise data. However, in that example, we also show that an AR(7) model also works well as an approximating model.

## 3.4 Visualizing AR Components

Another useful tool for understanding the features of an AR(p) realization is the decomposition of the realization into additive components. Specifically, letting x_t denote a realization from an AR(p) model for which there are no repeated roots of the characteristic equation, then x_t can be written as x_t = x_t^{(1)} + x_t^{(2)} + ... + x_t^{(m)} where m, as given in Equation 3.76, is the number of real roots plus the number of complex conjugate pairs of roots of the characteristic equation. The jth additive component x_t^{(j)}

- Corresponds to the jth factor in the factor table
- Is a realization from an AR(1) model for first-order factors
- Is a realization from an ARMA(2,1) model for irreducible second-order factors

For example, consider the AR(3) model

$$(1 - \alpha_1 B)(1 - \beta_1 B - \beta_2 B^2) X_t = a_t, \qquad (3.120)$$

with one real root and one complex conjugate pair of roots (i.e., $m = 2$). The model in Equation 3.120 can be written in inverted form as

$$X_t = \frac{1}{(1 - \alpha_1 B)(1 - \beta_1 B - \beta_2 B^2)} a_t, \qquad (3.121)$$

Recalling that operators can be inverted using properties of the corresponding algebraic quantities, we use partial fractions to write

$$\frac{1}{(1 - \alpha_1 z)(1 - \beta_1 z - \beta_2 z^2)} = \frac{A}{1 - \alpha_1 z} + \frac{C_1 + C_2 z}{1 - \beta_1 z - \beta_2 z^2}, \qquad (3.122)$$

from which we obtain

$$X_t = \frac{1}{(1 - \alpha_1 B)(1 - \beta_1 B - \beta_2 B^2)} a_t \qquad (3.123)$$
$$= \left(\frac{A}{1 - \alpha_1 B} + \frac{C_1 + C_2 B}{1 - \beta_1 B - \beta_2 B^2}\right) a_t$$
$$= \left(\frac{A}{1 - \alpha_1 B}\right) a_t + \left(\frac{C_1 + C_2 B}{1 - \beta_1 B - \beta_2 B^2}\right) a_t,$$

for real constants $A$, $C_1$, and $C_2$. Letting $X_t^{(1)} = (A / 1 - \alpha_1 B) a_t$ and $X_t^{(2)} = (C_1 + C_2 B / 1 - \beta_1 B - \beta_2 B^2) a_t$, it follows that $(1 - \alpha_1 B) X_t^{(1)} = A a_t$ and $(1 - \beta_1 B - \beta_2 B^2) X_t^{(2)} = (C_1 + C_2 B) a_t = (1 + (C_2 / C_1) B)(C_1 a_t)$. That is, $x_t^{(1)}$ is a realization from an AR(1) process where the AR factor is the first factor in the factored form of Equation 3.120, and $x_t^{(2)}$ is a realization from an ARMA(2,1) process where the AR factor is the second-order factor in the factored form of

[Equation 3.120.](#) In Example 10.14, we discuss the use of state-space formulation to actually construct these components. The important point to be made here is that each component corresponds to a row in the factor table. See also West (1997).

### EXAMPLE 3.20: ADDITIVE COMPONENTS OF THE AR(3) MODEL IN [EQUATION 3.73](#)

As an example, consider the AR(3) model $X_t - 2.55X_{t-1} + 2.42X_{t-2} - 0.855X_{t-3} = a_t$ previously given in [Equation 3.73](#) which, in factored form is $(1 - 0.95B)(1 - 1.6B + 0.9B^2)X_t = a_t$. It was pointed out earlier that realizations from this model have a wandering behavior produced by the positive real root ($f = 0$) and cyclic behavior with frequency $f = 0.09$ (i.e., periods of about 11) because of the complex conjugate roots. The factor table for this model is given in [Table 3.1](#). [Figure 3.26](#) shows the realization given previously in [Figure 3.16a](#) along with the additive ARMA(2,1) and AR(1) components obtained using the state-space approach to be discussed in [Section 10.6.7](#).

![](img/a0e0259119deb8c7b41dfd4f664e541d_190_0.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_190_1.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_190_2.png)

## FIGURE 3.26

Realization and additive components for the AR(3) model in Equation 3.76 whose factor table is given in Table 3.1. (a) Realization. (b) Component 1: f = 0.09. (c) Component 2: f = 0.

We note the following:

- The ARMA(2,1) component in Figure 3.26b contains the pseudo-cyclic portion of the realization associated with the complex conjugate root listed in the first row of the factor table in Table 3.1.
- The wandering behavior in the realization associated with the positive real root listed on the second row of the factor table in
