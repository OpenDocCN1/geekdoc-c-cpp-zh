# Temporal Difference Methods

![](bbox=[0.238, 0.066, 0.429, 0.189])

```
$\eta = v^T Av$\n$\eta = -v^T R^	heta v + (\lambda^{-1} - 1)\sum_{i=1}^{\infty} (\gamma\lambda)^i v^T R(i)v.$
```

**Figure 9.7** Left: Eigenvalues of $A$ satisfy real($\eta$) $\le -(1-\varrho_v)\pm\infty$. Right: Eigenvalue expressed in terms of eigenvector and autocorrelation sequence.

The identity (9.104) then follows from the smoothing property of conditional expectation:

```
$E_\pi[h(X(n))\psi(X(n))] = E_\pi[\sum_{i=0}^{\infty} \gamma^i c(X(n+i))\psi(X(n))]$\n$\sum_{i=0}^{\infty} \gamma^i E_\pi[c(X(n+i))\psi(X(n))] = E_\pi[\zeta_c(X(n))]$.
```

**Proof of Proposition 9.8** We confront a notational clash in analysis of TD($\lambda$), since a focus is bounding eigenvalues of a matrix $A$. In the remainder of this section, an eigenvalue-eigenvector pair is denoted $(\eta, v)$ for which is not zero, and $Av = \eta v$.

Let $(\eta, v)$ denote any eigenvalue-eigenvector pair for $A$, satisfying $||v||=1$. The eigenvector equation $Av = \eta v$ together with Lemma 9.9 gives the formula for $\eta$ shown on the right-hand side of Figure 9.7.

Let $z^0 = v^T R^	heta v > 0$ and $\omega = \eta + z^0 \in \mathbb{C}$, so that $\eta = -z^0 + w$. It remains to show that $|w| \le \varrho_v z^0$, that $\eta$ lies within the closed disc in Figure 9.7. This follows from Lemma 9.28:

```
$|w| \le (\lambda^{-1}-1)\sum_{i=1}^{\infty}(\gamma\lambda)^i v^T R(i)v \le q v^T R^	heta v)(\lambda^{-1}-1 \le q\varrho_v^2$.
```

**Proof of Proposition 9.12** Each part of the proof is based on properties of the function $p(\gamma) = \det(A_\gamma)$, which requires another representation of $A_\gamma$.

Following the proof of Lemma 9.9, we write $\zeta_n = \sum_{i=0}^{\infty}(\gamma\lambda)^i\psi(X_{(n-i)})$ and hence

```
$A_\gamma = \sum_{i=0}^{\infty}(\gamma\lambda)^i E_\pi[\psi_{(n-i)} + \gamma\psi_{(n+1)})^T$.
```

We always have $A_0 = -R^	heta$, so that $p(0)=\det(R^	heta)\neq 0$ for any value of $\lambda$.

```
$A_\gamma = -R^	heta + \gamma B, \quad \text{with } \ B = E_\pi[\psi(X(n))\psi(X(n+1))^T].$.
```

Part (i) is established by recognizing that $p(\gamma)$ is a polynomial function of degree $d$ that is not identically zero, and is therefore for at most $d$ values of $\gamma$.