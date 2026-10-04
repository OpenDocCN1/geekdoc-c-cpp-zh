in vector form. In the notation of Section 3.4, this multiplication produces the additive component $x_t^{(j)}$.

# 10.6.7.3 $\Psi$ Complex

Complex roots of the characteristic equation, $\phi(z) = 0$, occur in complex conjugate pairs, and if $r_j$ and $r_k$ are complex conjugates, that is $r_k = ar{r}_j$, then it follows that $\psi_{ik} = \overline{\psi}_{ij}$ for every $t$. We assume that complex conjugate pairs occur in adjacent rows of $\Psi_t$. The following assumes that $\psi_{ij}$ and $\psi_{ij+1}$ are complex conjugate pairs, and $\Psi_t$ is used to denote $\psi_{j+1}$. Thus, the real sequence

```
$x_t^{(j)} = \psi_{it} + \psi_{ijt}, \quad (10.65)$
```

is the additive component that corresponds to the quadratic factor, $1 - \alpha_1 z - \alpha_2 z^2$, of the characteristic polynomial (with the pair of complex conjugate roots, $r_j$ and $r_{j+1} = ar{r}_j$). Using the fact that $\Psi_t = U^{-1}X_t$, the component, $x_t^{(j)}$, can be obtained by adding the $j$th and $(j+1)$st rows of $U^{-1}$ and multiplying the resulting $p$ real coefficients by $x_t$, Appendix 10A shows that $x_t^{(j)}$ in Equation 10.65 is a realization from ARMA(2,1) model.

# EXAMPLE 10.14: FINDING THE ADDITIVE COMPONENTS OF THE AR(3) DISCUSSED IN SECTION 3.17

Figure 3.26 shows the additive components of the AR(3) model $X_t - 2.55X_{t-1} + 2.42X_{t-2} - 0.855X_{t-3} = a_t$ for which the factored form is $(1-0.95B)(1-1.6B + 0.9B^2)X_t = a_t$. For this AR(3) model, it follows that

$\Phi = \begin{pmatrix} 0 & 1 & 0 \ 0 & 0 & 1 \ 0.855 & -2.42 & 2.55 \end{pmatrix}$

and from the factor table in Table 3.1, it is seen that

$U = \begin{pmatrix} 1 & 0 & 0 \ 1 & (0.89+0.57i)^2 & (0.89-0.57i)^2 & 0.95 \ 1 & 0.89+0.57i & 1 & 1 \end{pmatrix} \quad (10.66)$

and it follows that

$U^{-1} = \begin{pmatrix} -1.76-0.53i & 2.81+1.82i & -1.08-1.25i \ -1.76+0.53i & 2.81-1.82i & -1.08+1.25i \ 3.52 & -5.61 & 3.15 \end{pmatrix} \quad (10.67)$