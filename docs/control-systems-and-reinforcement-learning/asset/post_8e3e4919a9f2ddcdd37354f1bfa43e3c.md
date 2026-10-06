
## 9.5.3 Relative TD($\lambda$)

We can expect numerical challenges with TD($\lambda$) algorithms when $\gamma$ is close to unity. The reason comes from the fact that either of the value functions defined in (9.6) is typically unbounded as $\gamma \uparrow 1$. We exploit the fact that the value functions are large only because of an additive constant.

This structure is illustrated via an example in Exercise 6.6 (b). For the general case, consider the fixed-policy Q-function:

```
$Q_{\gamma}(z) \triangleq \sum_{k=0}^{\infty}\gamma^k E[c(\Phi(k)) \mid \Phi(0) = z].$
```

Let $\eta = E_{\omega}[c_n]$, $\tilde{c}(z) = c(z) - \eta$, $\tilde{c}_k = \tilde{c}(\Phi(k))$, and write

```
$Q_{\gamma}(z) = \sum_{k=0}^{\infty}\gamma^k E[\eta + \tilde{c}_k \mid \Phi(0) = z] = \frac{1}{1-\gamma}\eta + \sum_{k=0}^{\infty}\gamma^k E[\tilde{c}_k \mid z].$
```

For $\gamma \sim 1$, the right-hand side is a very large constant, plus a term that approximates the solution to Poisson's equation in Theorem 6.3 (i) (for the Markov chain $\Phi$ rather than $X$). Consequently,

```
$$\lim_{\gamma \uparrow 1}(Q_{\gamma}(z) - \frac{1}{1-\gamma}\eta) = \tilde{Q}(z), \quad z \in X \times U,$$
```

where $\tilde{Q}$ solves Poisson's equation:

```
$E[\tilde{c}_k + \tilde{Q}(\Phi(k+1)) \mid \Phi(k) = z] = \tilde{Q}(z).$ (9.56)
```

The function $\tilde{Q}_{\gamma} = Q_{\gamma} - \eta/(1-\gamma)$ solves the DP equation

```
$c + \gamma P\tilde{Q}_{\gamma} = \tilde{Q}_{\gamma} + \eta.$ (9.57)
```

We might use this to define a temporal difference sequence. In application to policy improvement, the new policy can be represented in terms of $Q_{\gamma}$ instead of $Q_{\pi}$:

```
$\Phi^{\gamma}(x) \in \arg min Q_{\gamma}(x,u) = \arg min Q_{\gamma}(x,u).$
```

To avoid estimation of $\eta$, we have an alternative, called the (fixed-policy) relative dynamic programming equation:

```
$c + \gamma PH = H + \delta(\mu,H),$ (9.58)
```

where $\delta > 0$ is a positive scalar, $\mu : X \times U \to [0,1]$ is a pmf (both design choices), and $\langle\mu, H\rangle = \sum_{x,u} \mu(x,u)H(x,u).$

In the Notation Section 6.3, the DP (9.58) can be expressed

```
$[I - (\gamma P - \delta 1 \mu)]H = c.$
```

Lemma 9.13 tells us that $H$ can be expressed as a power series under mild assumptions on $P$ and $\delta$. More important is that $H = Q + constant$, so it is just as valuable as $Q$ for application policy improvement.

**Lemma 9.13** Suppose that $\Phi$ is uni-chain. Then, for each $\gamma \in [0,1]$,

(i) The eigenvalues of the matrix $\gamma P-\delta 1 \otimes \mu$ coincide with those of $\gamma P$, except for $\lambda_1 = \gamma$ which is moved to $\gamma-\delta$.

(ii) Provided $|\gamma-\delta| < 1$, we have

```
$H = [I-(\gamma P-\delta 1 \otimes \mu)] = \sum_{n=0}^{\infty} (\gamma P-\delta 1 \otimes \mu)^n c.$
```

The sum is convergent because $(\gamma P-\delta 1 \otimes \mu)^n \to 0$ geometrically as $n \to \infty$.

(iii) $H=Q-k$, with

```
$k = \frac{\delta}{1-\delta}(\mu, Q) = \frac{\delta}{1-\gamma}(\mu, H).$
```

The big step in establishing (iii) is an application of Matrix Inverse Lemma (A.1) to obtain the representation

```
$[I-(\gamma P-\delta 1 \otimes \mu)]^{-1} = (I-\gamma P)^{-1}-\frac{\delta}{1-\delta}[1 \otimes \mu](I-\gamma P)^{-1}.$
```

The relative DP has probabilistic interpretation

```
$E[-H(\Phi(n))-\delta(\mu,H)+c_n+\gamma H(X(n+1))]=0, \quad n \geq 0,$
```

where $H(x)=\sum_{u} H(x,u)\mu(x,u)$. Suppose $\{\theta \in \mathbb{R}^d\}$ is a parameterized family of functions on $X \times U$. The goal in relative TD $(\lambda)$ is to have $\theta^*$ satisfying $f(\theta^*)=0$,

```
$f(\theta)=E_{\zeta_n}[-H(\Phi(n))-\delta(\mu,H)+c_n+\gamma H(X(n+1))]=0.$
```

where $\{\zeta_n\}$ are eligibility vectors defined via (9.53) if the parameterization is linear. SA algorithm to estimate $\theta^*$ is described in this special case:

## Relative TD($\lambda$) (Off-Policy)

For initialization $\theta_0, \zeta_0 \in \mathbb{R}^d$, the sequence of estimates are defined recursively: this is a linear SA based on the equation $f(\theta)=A\theta-b$, with

```
$A=E_{\zeta_n}[-\Phi(n)+\gamma X(n+1)], \quad b=-E_{\zeta_n}[c_n\zeta_n].$
```

where $\psi^n$ is a $d$-dimensional column vector where $i$-th component is $\langle\mu,\psi_i\rangle$. Conditions to ensure that $A$ is Hurwitz can be obtained in the off-policy setting. A challenge for $\lambda=1$: case $b=-E_{\zeta_n}[c_n\zeta_n]$ may be very large when $\gamma\sim1$, and this suggests high variance in the algorithm. The regeneration technique introduced in Section 10.3 is one approach to obtain algorithms that are reliable when both $\gamma$ and $\lambda$ are close to unity.

## Temporal Difference Methods

An alternative is to abandon approximation of $Q$ and turn to the advantage function.

### 9.5.4 TD($\lambda$) for Advantage

The advantage function introduced in Section 9.1.3 admits the following equivalent forms:

**Proposition 9.14** The following representations hold for the advantage function:

```
$V(x,u) = Q(x,u) - h(x) \quad (9.65a)$
$-h(x) + c(x,u) + \gamma E[h(X(k+1)) \mid \Phi(k) = (x,u)] \quad (9.65b)$
= c(x,u) - c_{\phi}^*(x) + \gamma E[h(X(k+1)) \mid \Phi(k) = (x,u)] - E[h(X(k+1)) \mid X(k) = x] \quad (9.65c)$
```

for each $x \in \mathbb{X}, u \in \mathbb{U}$, and with $c_{\phi}^*(x) = \sum_{u} c(x,u)\phi(u|x)$.

The motivation for the advantage function is in part the desire to reduce variance in the estimate of the function used in policy improvement. This brings a question: can we estimate $V$ directly with reduced variance (as compared to estimating $Q$ and $h$ and then subtracting)? It might not be surprising that the answer is yes, but full justification comes until Section 10.2. We provide here a heuristic and an algorithm.

For the heuristic, we have $E[V(\Phi(k))] = 0$ for each $k$, so it is reasonable to choose a policy class that holds for any approximation within this class. This is not difficult to arrange.

The following notation is introduced in Chapter 10:

```
$$\psi(x) = \sum_{u} \psi(x,u)\phi(u|x) \quad \quad \widetilde{\psi}(x,u) = \widetilde{\psi}(x,u) - \psi(x), \quad x \in \mathbb{X}, u \in \mathbb{U} (9.66)$$
```

We search for an approximation within the following class:

```
$$\widetilde{\mathcal{H}} = \{H^{\theta} \in \mathcal{H} : \theta \in \mathbb{R}^d\}. \quad \quad (9.67)$$
```

We have by definition $E|H(\Phi(k)) \mid X(k)| = 0$ for any $H \in \widetilde{\mathcal{H}}$. With a bit more work, we learn that $H=Q+constant$ is just as valuable as $Q$ for application policy improvement.

## 9.5 Return to the Q-Function

### 9.5.1 Optimal Control Essentials

(i) The eigenvalues of the matrix $\gamma P-\delta 1 \otimes \mu$ coincide with those of $\gamma P$, except for $\lambda_1 = \gamma$ which is moved to $\gamma-\delta$.

(ii) Provided $|\gamma-\delta| < 1$, we have

```
$H = [I-(\gamma P-\delta 1 \otimes \mu)] = \sum_{n=0}^{\infty} (\gamma P-\delta 1 \otimes \mu)^n c.$
```

The sum is convergent because $(\gamma P-\delta 1 \otimes \mu)^n \to 0$ geometrically as $n \to \infty$.

(iii) $H=Q-k$, with

```
$k = \frac{\delta}{1-\delta}(\mu, Q) = \frac{\delta}{1-\gamma}(\mu, H).$
```

The big step in establishing (iii) is an application of Matrix Inverse Lemma (A.1) to obtain the representation

```
$[I-(\gamma P-\delta 1 \otimes \mu)]^{-1} = (I-\gamma P)^{-1}-\frac{\delta}{1-\delta}[1 \otimes \mu](I-\gamma P)^{-1}.$
```

The relative DP has probabilistic interpretation

```
$E[-H(\Phi(n))-\delta(\mu,H)+c_n+\gamma H(X(n+1))]=0, \quad n \geq 0,$
```

where $H(x)=\sum_{u} H(x,u)\mu(x,u)$. Suppose $\{\theta \in \mathbb{R}^d\}$ is a parameterized family of functions on $X \times U$. The goal in relative TD $(\lambda)$ is to have $\theta^*$ satisfying $f(\theta^*)=0$,

```
$f(\theta)=E_{\zeta_n}[-H(\Phi(n))-\delta(\mu,H)+c_n+\gamma H(X(n+1))]=0.$
```

where $\{\zeta_n\}$ are eligibility vectors defined via (9.53) if the parameterization is linear. SA algorithm to estimate $\theta^*$ is described in this special case:

### 9.6 Watkins's Q-Learning

### TD($\lambda$) (On-Policy)

For initialization $\theta_0, \zeta_0 \in \mathbb{R}^d$, the sequence of estimates are defined recursively: this is a linear SA based on the equation $f(\theta)=A\theta-b$, with

```
$A=E_{\zeta_n}[-\Phi(n)+\gamma X(n+1)], \quad b=-E_{\zeta_n}[c_n\zeta_n].$
```

where $\psi^n$ is a $d$-dimensional column vector where $i$-th component is $\langle\mu,\psi_i\rangle$. Conditions to ensure that $A$ is Hurwitz can be obtained in the off-policy setting. A challenge for $\lambda=1$: case $b=-E_{\zeta_n}[c_n\zeta_n]$ may be very large when $\gamma\sim1$, and this suggests high variance in the algorithm. The regeneration technique introduced in Section 10.3 is one approach to obtain algorithms that are reliable when both $\gamma$ and $\lambda$ are close to unity.
