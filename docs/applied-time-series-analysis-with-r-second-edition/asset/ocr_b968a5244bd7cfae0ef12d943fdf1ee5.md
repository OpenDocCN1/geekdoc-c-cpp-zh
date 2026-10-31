Then **X**_t is called a VAR(p) process, that is, a vector AR process of order p.

Note that Equation 10.15 can be written in multivariate operator notation **Φ**(B)(**X**_t − **μ**) = **a**_t, where

**Φ**(B) = **I** − **Φ**₁B − ⋯ − **Φ**_p B^p,   (10.16)

and B^k **X**_t = **X**_{t−k}. Theorem 10.1 below gives stationarity conditions for VAR(p) models that are analogous to those in Theorem 3.2 for univariate AR(p) models.

# Theorem 10.1

A multivariate process **X**_t satisfying the difference equation in Equation 10.15 is a stationary and causal VAR(p) process if and only if the roots of the determinantal equation,

| **Φ**(z) | = | **I** − **Φ**₁z − ⋯ − **Φ**_p z^p | = 0,

lie outside the unit circle.

Proof: See Brockwell and Davis (1991) and Reinsel (1997).

Note that a VAR(p) model **Φ**(B)(**X**_t − **μ**) = **a**_t satisfying Theorem 10.1 can be written in the multivariate general linear process form

**X**_t − **μ** = **Ψ**(B)**a**_t   (10.17)
= Σ_{j=0}^{∞} **Ψ**_j **a**_{t−j},

where **Ψ**(B) = **Φ**^{-1}(B).

The multivariate Yule–Walker equations are given by

**Γ**(k) = **Γ**(k−1)**Φ**₁' + ⋯ + **Γ**(k−p)**Φ**_p',   k = 1, …, p,   (10.18)

where

**Γ**(0) = **Φ**₁**Γ**(−1) + ⋯ + **Φ**_p**Γ**(−p) + **Γ**_a,   (10.19)