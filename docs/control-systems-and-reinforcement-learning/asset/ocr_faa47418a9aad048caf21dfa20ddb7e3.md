# 9.5 Return to the Q-Function

(i) The eigenvalues of the matrix $\gamma P-\delta 1 \otimes \mu$ coincide with those of $\gamma P$, except for $\lambda_1 = \gamma$ which is moved to $\gamma-\delta$.

(ii) Provided $|\gamma-\delta| < 1$, we have

```
$H = [I-(\gamma P-\delta 1 \otimes \mu)] = \sum_{n=0}^{\infty} (\gamma P-\delta 1 \otimes \mu)^n c.$
```

The sum is convergent because $(\gamma P-\delta 1 \otimes \mu)^n 	o 0$ geometrically quickly as $n 	o \infty$.

(iii) $H=Q-k$, with

```
$k = \frac{\delta}{1-\delta}(\mu, Q) = \frac{\delta}{1-\gamma}(\mu, H).$
```

The big step in establishing part (iii) is an application of the Matrix Inverse Lemma (A.1) to obtain the representation

```
$[I-(\gamma P-\delta 1 \otimes \mu)]^{-1} = (I-\gamma P)^{-1}-\frac{\delta}{1-\delta}[1 \otimes \mu](I-\gamma P)^{-1}$.
```

The relative DP has the probabilistic interpretation

```
$E[-H(\Phi(n))-\delta(\mu,H)+c_n+\gamma H(X(n+1)) \mid F_n]=0, \quad n \geq 0$,
```

where $H(x)=\sum_{u} H(x,u)\Phi(u \mid x)$ as in (9.54). Suppose that $\{	heta^0: \theta \in \mathbb{R}^d\}$ is a parameterized family of functions on $X 	imes U$. The goal in relative TD $(\lambda)$ learning is to have $	heta^*$ satisfying $f(\theta^*)=0$,

```
$f(\theta)E_{\zeta_n}[-H(\Phi(n))-\delta(\mu,H)+c_n+\gamma H(X(n+1))]_{\zeta_n}=0$.
```

where $\{\zeta_n\}$ are the eligibility vectors - defined via (9.53) if the parameterization is linear.
A SA algorithm to estimate $	heta^*$ is described in this special case:

# Relative TD($\lambda$) (Off-Policy)

For initialization $	heta_0, \zeta_0 \in \mathbb{R}^d$, the sequence of estimates are defined recursively:

This is a linear SA recursion based on the equation $\frac{d\theta}{dt}=f(\theta)=A\theta-b$, in $\zeta_n$,

```
$A=E_{\zeta_n}[\zeta_n(-\Phi(n))-\delta\psi^n+\gamma\psi(X(n+1))], \quad b=-E_{\zeta_n}[c_n\zeta_n].
```

where $\psi^n$ is a $d$-dimensional column vector, where $i$-th component is the $\langle\mu,\psi_i\rangle$. Conditions to ensure that $A$ is Hurwitz can be obtained in the off-policy setting.

A challenge for $\lambda=1$ in case $b=-E_{\zeta_n}[c_n\zeta_n]$ may be very large when $\gamma\sim1$, and this suggests high variance in the algorithm. The regeneration technique introduced in Section 10.3 is one approach to obtain algorithms that are reliable when both $\gamma$ and $\lambda$ are close to unity.