# 328 Temporal Difference Methods

The random variable $\mathcal{D}_{n+1}$ is the temporal difference introduced in Section 9.3; using the definition (9.26), we have simplified notation via

$\mathcal{D}_{n+1} = \mathcal{D}_{n+1}^	heta$.

The proofs of Theorem 9.7 and Proposition 9.8 are postponed to Section 9.9.2.

**Theorem 7.9** Suppose that $	heta^*$ solves (9.35), where the expectation is in steady state, and the eligibility vector is defined using TD(\lambda)$ with linear function approximation (9.27). The solution has the following interpretation for two choices of $\lambda$:

+   (i) $\lambda = 0$: In the notation of (9.19),

$\mathbb{E}[\mathcal{D}_{n+1}^	heta \mid Y_n] = 0$,

with $Y_n = \psi(X(n))$ and $\mathcal{D}_{n+1}^	heta = -h^	heta(X(n)) + c(X(n)) + \gamma h^	heta(X(n+1))$.

+   (ii) $\lambda = 1$: $	heta^*$ solves (9.33), with norm, (9.34).

Subject to (9.27), we have

$\mathcal{D}_{n+1} = c(X(n)) + [\gamma \psi(X(n+1)) - \psi(X(n))]^	op 	heta_n$,

and (9.37) can be placed in the form of the linear SA recursion (8.53b), with

$A_{n+1} = \zeta_n, [\gamma \psi(X(n+1)) - \psi(X(n))]^	op$,$\nb_{n+1} = \zeta_n c(X(n)).$ (9.38)

Let $A = \mathbb{E}[A_n]$ and $b = \mathbb{E}[b_n]$, where the expectations are in steady state. If $A$ is invertible, then $	heta^* = A^{-1}b$ is the unique solution to (9.35).

Proposition 9.8 (i) tells us that the matrix $A$ is invertible and the TD($\lambda$) algorithm is consistent under linear independence. Part (ii) is of interest when we consider the average-cost setting.

The definition of linear independence remains when $\psi$ is a function of $x$ only, and we continue to define it as (9.24):

$R^\psi = \mathbb{E}_\pi[\psi(X(n))\psi(X(n))^	op$. (9.39)

Let $\Sigma^\psi$ denote the steady-state covariance of the basis:

$\Sigma^\psi = R^\psi - ar{\psi}ar{\psi}^	op$. (9.40)

where $\psi = \mathbb{E}_\pi[\psi(X(n))]$.

**Proposition 9.8** The steady-state mean of the matrix $A_n$ in (9.38) satisfies the

+   (i) If the linear independence condition ($\gamma$, 24) holds, then $A$ is Hurwitz, and $	heta^* = A^{-1}b$ for any $\gamma \in [0,1]$ and $\lambda \in [0,1]$.

+   (ii) If $\Sigma^\psi > 0$ and $\Phi$ is aperiodic, then $A$ is Hurwitz for $\gamma = 1$ and $\lambda < 1$.

The following representation of $A$ is required in the proofs of Theorem 9.7 and Proposition 9.8. See (9.23) to recall the definition of the autocorrelation sequence $\{R(i)\}$.