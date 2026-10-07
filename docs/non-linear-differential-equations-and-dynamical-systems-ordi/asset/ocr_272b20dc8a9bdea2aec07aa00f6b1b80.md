# Non-Linear Differential Equations and Dynamical Systems

(4.421c), where the upper (lower) sign corresponds to $\Omega>0(\Omega<0)$. The solution of the unforced equation is (4.422a):

```
$\Theta(\theta) = C_{\pm}(	heta)\exp(\pm2\lambda\theta); \quad \frac{dC_{\pm}}{d\theta} = -2\omega_0\exp(\pm2\lambda\theta)\sin\theta, \quad (4.422a, b)$
```

using the method of variation of parameters (notes 1.2–1.4) the constant $C_{\pm}$ is replaced by a function $C_{\pm}(	heta)$, and substitution of (4.422a) in (4.421c) leads to (4.422b) as follows:

```
$-2\omega_0\sin\theta = \pm2\lambdaC_{\pm}(	heta)\exp(\pmpm2\lambda\theta) + \frac{d}{d\theta}[C_{\pm}(	heta)\exp(\pmpm2\lambda\theta)]=\exp(\pmpm2\lambda\theta)\frac{dC_{\pm}}{d\theta}\n(4.422c)
```

The integration of (4.422c) is elementary:

```
$C_{\pm}(\theta) = i\omega_0\frac{1}{2}[\exp(\pmpm2\lambda\theta+i)-\exp(\pmpm2\lambda\theta-i)]d\theta\n=i\omega_0\exp(\pmpm2\lambda\theta)\frac{e^{-i}}{\pm2\lambda+i}-\frac{e^{i}}{\pm2\lambda-i}]+D_{\pm},\n=\frac{2\omega_0^2}{1+4\lambda^2}\exp(\pm2\lambda\theta)(\cos\theta\pm2\lambda\sin\theta)+D_{\pm},\n(4.422d)
```

using (II.5.3, b) to within an added constant $D_{\pm}$.

# 4.7.18 Number of Revolutions and Damped Oscillation to Rest

Substituting (4.422d) with distinct added constant $D_{\pm}$ for $\Omega\geq0(\Omega\leq0)$ and upper (lower) sign in (4.422a; 4.421a) leads to:

```
$$\omega_1^2 = \frac{\omega_0^2}{1+4\lambda^2}; \quad [\Omega^2] = \begin{cases} D_{\pm}e^{-2\lambda^2t}+2\omega_0^2(\cos\theta-\pm2\lambda\sin\theta) & \text{if} \\Omega\geq0, \ D_{\pm}e^{2\lambda^2t}+2\omega_0^2(\cos\theta+\pm2\lambda\sin\theta) & \text{if} \\Omega\leq0. \end{cases}\n(4.423a-c)
```

Thus the nonlinear pendulum (Figure 4.19a) with quadratic friction (4.418a, b) has particular (134) paths (4.423b, c) in the phase plane where (4.423a) is the oscillation frequency for small amplitude and (4.419b) is the damping coefficient. The large amplitude motion (Figure 4.21) curls around (stable (unstable) equilibrium (4.424b) (4.424a) in the phase plane that are positions of suspended (inverted) (4.424c) where the pendulum is suspended (inverted) in the Figure 4.19b(c):

```
$\theta=0, \quad \theta_a=n\pi=\begin{cases}2\pi n & \text{stable equilibrium},\2\pi n-\pi & \text{unstable equilibrium}. \end{cases}\n(4.424a–c)
```