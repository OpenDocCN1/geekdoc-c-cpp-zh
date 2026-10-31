
We let N_t ~ N(0, 1) denote noise that is uncorrelated with both V_t and W_t. Consequently,

σ²_W* = { 0.75, if t ≠ 2, 5
          1.75, if t = 2, 5. }

The missing values are estimated using the Kalman iteration to calculate X̂_t^t, X̂_t^{t-1}, Γ_t^t, and Γ_t^{t-1}, t = 1, ..., 75; and then for t = 75, 74, ..., 2,1, the smoothing iterations are used to calculate the values for X̂_2^{75} and X̂_5^{75} which are the desired estimates. In Table 10.2, we show the revised version of Table 10.1 when y_2 and y_5 are missing. As expected, it can be seen that X̂_2^2 and X̂_2^{75} are associated with higher mean-squared errors than for the cases with available data on Y_t.

**Using R:** The results in Table 10.2 were obtained using the kalman.miss.wge function in tswge. This function is based on a call to ksmooth1 from the astsa package in CRAN. The kalman.miss.wge function is a univariate simplification designed to perform analyses such as the predicting, filtering, and smoothing in missing data settings such as that considered in Example 10.12. For discussion of the statements used to create the data in Table 10.2, see Appendix 10B.

## 10.6.6 Parameter Estimation

Let Θ denote the vector of parameters to be estimated in the state-space model specified in Equations 10.48 and 10.49. It will be convenient for us to write the likelihood function L(Θ ; Y_1, ..., Y_n) (conditional on Y_0) as L(Θ ; Y_1, ..., Y_n) = Π_{t=1}^n f_t(Y_t | Y_{t-1}, ..., Y_1), where f_t(Y_t | y_{t-1}, ..., y_1) is the conditional density of Y_t, given that Y_j = y_j, j = 1, ..., t-1 (and conditional that Y_0 = y_0). Calculation of the likelihood is complicated but can be made more tractable if the V_t and W_t are jointly normally distributed and uncorrelated and if the initial state X_0 ~ MVN(μ_0, Γ_0). The innovations, I_t, are calculated where

I_t = Y_t - G_t X̂_t^{t-1},   (10.60)

and

$$\Gamma_{I_t} \equiv \operatorname{Var}[I_t] = \operatorname{Var}\left[\boldsymbol{G}_t\left(\boldsymbol{X}_t - \hat{\boldsymbol{X}}_t^{t-1}\right) + \boldsymbol{W}_t\right]$$ $$= \boldsymbol{G}_t \boldsymbol{\Gamma}_t^{t-1} \boldsymbol{G}_t' + \boldsymbol{\Gamma}_W.$$ \tag{10.61}

(see also proof of Kalman prediction and filtering in Appendix 10A). Based on the aforementioned normality assumptions, the likelihood can be written as

$$L(\boldsymbol{\Theta}; Y_1, \ldots, Y_n) = \frac{1}{(2\pi)^{n/2}}\left(\prod_{t=1}^{n} |\boldsymbol{\Gamma}_{I_t}|\right)^{-1/2} \exp\left[-\frac{1}{2}\sum_{t=1}^{n} I_t' \boldsymbol{\Gamma}_{I_t}^{-1} I_t\right].$$ \tag{10.62}

Numerical maximization procedures are used to find the ML estimates from Equation 10.62. Shumway and Stoffer (1982, 2010) discuss the use of Newton–Raphson and expectation maximization (EM) algorithms for performing this maximization.

## 10.6.7 Using State-Space Methods to Find Additive Components of a Univariate AR Realization

In Section 3.4, we discussed the decomposition of an AR realization into additive components, $x_t = x_t^{(1)} + \cdots + x_t^{(m)}$, where $m$ is the number of rows in the factor table. That is, $m$ is equal to the number of real roots and pairs of complex conjugate roots of the characteristic equation. In that section, we gave a partial fractions derivation to show that the additive components are realizations from an AR(1) model for real roots and an ARMA (2,1) model for complex conjugate roots. We showed that in each case the system frequency associated with row $j$ of the factor table is the system frequency inherent in the AR(1) or ARMA(2,1) model that corresponds to the $j$th component. However, the derivation in Section 10.3.4 did not lead to a method of calculation. In this example, we consider a state-space formulation of this problem, and in addition to showing that the components are AR(1) and ARMA(2,1) as before, the state-space approach also provides a simple method for calculating these components.

In Example 10.10, we gave a set of state-space equations for a univariate, zero-mean AR($p$) process $Y_t = \phi_1 Y_{t-1} + \cdots + \phi_p Y_{t-p} + a_t$. The state and observation equations were seen to be

$\boldsymbol{X}_t = \boldsymbol{\Phi}\ \boldsymbol{X}_{t-1} + \boldsymbol{V}_t \quad\text{(state equation)},$
$\boldsymbol{Y}_t = (0\ 0\ \dots\ 1)\boldsymbol{X}_t \quad\text{(observation equation)},$

where
$\boldsymbol{X}_t = \begin{pmatrix} Y_{t-p+1}\\ Y_{t-p+2}\\ \vdots\\ Y_t \end{pmatrix},\quad \boldsymbol{\Phi}= \begin{pmatrix}0&1&0&\dots&0\\0&0&1&\dots&0\\\vdots&\vdots&\vdots&&\vdots\\0&0&0&\dots&1\\\phi_p&\phi_{p-1}&\phi_{p-2}&\dots&\phi_1\end{pmatrix},\quad \boldsymbol{V}_t = \begin{pmatrix}0\\0\\\vdots\\0\\a_t\end{pmatrix}$

In this case, $v = p$, $w = 1$, and $\mathbf{W}_t = \mathbf{0}$, and we assume $a_t \sim N(0,\sigma_a^2)$. In the following, we will assume that the eigenvalues of $\boldsymbol{\Phi}$ are distinct. These eigenvalues are $1/r_1$, $1/r_2$, ..., $1/r_p$ where $r_1$, ..., $r_p$ are the roots of the characteristic equation $\phi(z)=1-\phi_1 z-\phi_2 z^2-\dots-\phi_p z^p=0$. The eigenvector corresponding to $1/r_j$ can be chosen to be $\boldsymbol{u}'_j = (r_j^{p-1}\ r_j^{p-2}\ \dots\ r_j\ 1)$, and we have $\boldsymbol{\Phi}=U D U^{-1}$ where $\boldsymbol{U}=[\boldsymbol{u}_1\ \boldsymbol{u}_2\ \dots\ \boldsymbol{u}_p]$ and

$\boldsymbol{D}= \operatorname{diag}\left(\frac{1}{r_1}\ \frac{1}{r_2}\ \dots\ \frac{1}{r_p}\right)$

that is, a diagonal matrix with the listed elements along the diagonal. Note that due to the choice of eigenvectors, the last row of $\mathbf{U}$ is a vector of 1s. For our purposes, we arrange $\mathbf{D}$ (and $\mathbf{U}$) so that $|r_1| \ge |r_2| \ge \dots$

Defining $\boldsymbol{\Psi}_t = \boldsymbol{U}^{-1}\boldsymbol{X}_t$ (i.e., $\boldsymbol{X}_t = \boldsymbol{U}\boldsymbol{\Psi}_t$), the state-space model can be rewritten so that the rows of $\mathbf{U}^{-1}$ provide the filter coefficients needed to calculate the components.

### 10.6.7.1 Revised State-Space Model

State Equation: $\boldsymbol{X}_t = \boldsymbol{\Phi}\ \boldsymbol{X}_{t-1} + \boldsymbol{V}_t$ becomes $\boldsymbol{X}_t = (\boldsymbol{U}\boldsymbol{D}\boldsymbol{U}^{-1})(\boldsymbol{U}\boldsymbol{\Psi}_{t-1}) + \boldsymbol{V}_t$, that is, $\boldsymbol{U}\boldsymbol{\Psi}_t = \boldsymbol{U}\boldsymbol{D}\boldsymbol{\Psi}_{t-1} + \boldsymbol{V}_t$, so that
$\boldsymbol{\Psi}_t = \boldsymbol{D}\boldsymbol{\Psi}_{t-1} + \boldsymbol{U}^{-1}\boldsymbol{V}_t$ (new state equation). (10.63)

Observation Equation: In this case $\boldsymbol{Y}_t = (0\ 0\ \dots\ 0\ 1)\ \boldsymbol{X}_t$ becomes $\boldsymbol{Y}_t = (0\ 0\ \dots\ 0\ 1)\ \boldsymbol{U}\boldsymbol{\Psi}_t$, that is, (10.64)

$x_t^{(1)} = (-3.52\;\;5.26\;\;-2.16)\begin{pmatrix}x_{t-2}\\x_{t-1}\\x_t\end{pmatrix},$

for $t = 3, \dots, 200$. From the third row of $\mathbf{U}^{-1}$, we obtain

$x_t^{(2)} = (3.52\;\;-5.61\;\;3.15)\begin{pmatrix}x_{t-2}\\x_{t-1}\\x_t\end{pmatrix},$

The components $x_t^{(1)}$ and $x_t^{(2)}$ were shown in Figure 3.24 where it can be seen that $x_t^{(1)}$ captures the pseudo-cyclic behavior with periods of about 11 (1/0.09) units while $x_t^{(2)}$ depicts the wandering behavior associated with the positive real root.

**Using R:** Decompositions of AR realizations can be obtained using the tswge function `factor.comp.wge`. The computations shown in Example 10.14 and the decompositions shown in Figure 3.26 are based on the true model parameters associated with the AR(3) realization shown in Figure 3.16. The function `factor.comp.wge` fits an AR(p) model of specified order and plots the original series and decompositions. The following commands will produce plots similar to those shown in Figure 3.26 (except that they are based on the ML estimates:

```
data(fig3.16a)
factor.comp.wge(fig3.16a,p = 3,ncomp = 2)
```

## Appendix 10A: Derivation of State-Space Results

### 10A.1 Proof of Kalman Recursion for Prediction and Filtering

From probability theory, it is known that if $Y_1, \dots, Y_s,\ X_t$ are univariate random variables that are jointly normal, then the best linear predictor of $X_t$ in the mean-square sense based on $Y_1, Y_2, \dots, Y_s$ is the conditional expectation $E[X_t | Y_1, \dots, Y_s]$. That is, $E[X_t | Y_1, \dots, Y_s]$ is linear in the $Y'_j$s, call it $E[X_t | Y'_1, \dots, Y'_s] = \sum_{j=1}^s a_j Y_j$, and among all linear
