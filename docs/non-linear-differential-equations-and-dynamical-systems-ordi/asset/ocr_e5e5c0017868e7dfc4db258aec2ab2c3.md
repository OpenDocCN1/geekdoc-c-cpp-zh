# Unsteady, Non-Linear, and Chaotic Systems

substituting (4.38a) in (4.35b, c) leads to (4.38b). A non-trivial solution (4.39a) requires that the determinant of the matrix of coefficients be zero (4.39b):

```
${A,B} \neq {0,0\}: \quad 0 = \begin{pmatrix} \vartheta-a & -b \ -c & \vartheta-d \end{pmatrix} \n = (\vartheta-a)(\vartheta-d) + ad-bc = P_2(\vartheta),; \n = \vartheta^2-(a+d)\vartheta+ad-bc$ \quad (4.39a-c)$
```

leading to the characteristic polynomial (4.39c) = (4.37a, b) = (4.40a, b):

```
$D = \frac{d}{dt}: P_2(D) = D^2-(a+d)D+(ab-bc) = D^2+\omega_{\xi}^2 = (D-\xi_{\xi})(D+\xi_{\xi});; \quad (4.40a,b)$
```

The characteristic polynomial (4.40a, b) of the first-order system of linear equations with constant coefficients (4.35a-c) can be obtained: (i) directly (4.39c) from vanishing of the determinant (4.39b) matrix of coefficients (4.38b) for the exponential solutions (4.38a); or (ii) indirectly, eliminating (4.36) for a linear second-order differential equation with constant coefficients satisfied by each of the variables (4.37a, b). The characteristic polynomial of the second degree (4.40a, b) leads to an analysis with the equivalent second-order linear system with constant coefficients (chapter 2) corresponding to a damped harmonic oscillator (subsection 4.2.2).

# 4.2.2 Equivalent Damped Harmonic Oscillator

The characteristic polynomial corresponds to that (2.81b) = (4.40b) for a "damped oscillator":

```
$\lambda = \frac{a+d}{2}=-b\gamma, \quad \omega_0^2 = ad-bc \neq 0; \quad (4.41a,b)$
```

where: (i) (4.13a) was used in (4.41a); (ii) the condition $\omega_0 \neq 0$ in (4.41b) implies (4.5a) that the differential equation (4.5b) is non-trivial dy/dx const. The characteristic polynomial (4.40a, b) corresponds to a generalized oscillator, since (problem 79) the two pairs of terms are interpreted as: (i) the (4.42a) first two terms (4.42c) specify (4.41b) a velocity (4.42b) that is amplified (decays) with time for $\lambda<0(\lambda>0)$ in (4.42d) and is constant for $\lambda=0;$

```
$ad=bc; \quad v=\dot{x}; \quad 0=\dot{x}+2\lambda\dot{x}=\dot{v}+2\lambda v; \quad v(t)=v(0)e^{-2\lambda t};; \quad (4.42a-d)$
```