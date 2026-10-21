Solving these two equations, it follows that $s_1 = -s_2$. This implies we can reduce the above two conditions to the single condition

$\lambda_m^s = \lambda_n^{-s}$

Following the work of McLean [McL82a, McL82b] and Francius & Kharif [FK06], there are two main conditions that we need to investigate for collisions of eigenvalues with opposite signatures:

+   - **Class I:** $n = -m$ (the case of complex conjugates colliding at the origin),
+   - **Class II:** $n = -m - 1$ (collisions on the imaginary axis, away from the origin).

There are additional collisions of interest (such as when $n = -m - 2$, etc). However, recalling that the perturbations are periodic in $\mu$ with period 1, we can omit these additional collisions from consideration. These conditions give rise to the well-known resonant curves that are found throughout the literature (see for example (Ref. [McL82a, McL82b, FK06])). They are shown in Figure 3 for $h = .5$. These curves connect the values of $\mu$ and $\rho$ for which eigenvalues with opposite signatures collide.

# 4.2. General Results.

As mentioned in the introduction, much is known about the transverse stability of one-dimensional solutions of Euler’s equations. Our intent is to demonstrate that the use of the AFM method reproduces these known results for the same parameter values as those used most recently by Francius & Kharif [FK06], with less computational effort, or equivalently, with greater accuracy for comparable computational effort. The comparison is not straightforward. In [FK06], the authors used solutions that were allowed to have non-zero average value for a fixed depth whereas with our method, we strictly inforce zero-average values solutions.

![](bbox=[0.21, 0.62, 0.77, 0.85])

FIGURE 4. The spectrum {$\lambda$} (real vs. imaginary part) for $h = .5$ and amplitude $a = .1$. Computed with $N = 16$ Fourier modes, 1000 $\mu$ values, and 300 $\rho$ values.