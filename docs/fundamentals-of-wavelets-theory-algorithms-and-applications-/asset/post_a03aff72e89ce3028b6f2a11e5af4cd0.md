
upper limit of $S\delta$ increases with the decreasing values of $s_0$. Therefore, it is better to choose $s_0 = \lceil \log_2(2m - 1) \rceil$, where $\lceil x \rceil$ represents the smallest integer that is greater than or equal to $x$.

## 10.6 NUMERICAL EXAMPLES

In this section we present some numerical examples for the scattering problems described in Section 10.1. Numerical results for strip and wire problems can be found in [14]. For more applications of wavelets to electromagnetic problems, readers may refer to [22].

The matrix equation (10.23) is solved for a circular cylindrical surface [23]. Figures 10.6 and 10.7 show the surface current distribution using linear and cubic splines, respectively, for different sizes of the cylinder. The wavelet MoM results are compared with the conventional MoM results. To obtain the conventional MoM results, we have used triangular functions for both expanding the unknown current distribution and testing the resultant equation. The conventional MoM results have been verified with the series solution [37]. Figure 10.8 gives the radar cross section for linear and cubic spline cases. The results of the conventional MoM and the wavelet MoM agree very well.

FIGURE 10.6: Magnitude and phase of the surface current distribution on a metallic cylinder using linear spline wavelet MoM and conventional MoM.

Reprinted with permission from [23]; copyright © 1995 by IEEE.

![](img/f73ae67732328dc36596b27ffe8d0152_575_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_575_1.png)

FIGURE 10.7: Magnitude and phase of the surface current distribution on a metallic cylinder using cubic spline wavelet MoM and conventional MoM.

![](img/f73ae67732328dc36596b27ffe8d0152_577_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_577_1.png)

FIGURE 10.8: Radar cross-section of a metallic cylinder computed using linear ($m=2$) and cubic ($m=4$) spline wavelet MoM and conventional MoM.

![](img/f73ae67732328dc36596b27ffe8d0152_579_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_579_1.png)

The effects of $\delta$ on the error in the solution and the sparsity of the matrix are shown in Figure 10.9. The magnitude of error increases rapidly for the linear spline case. Figure 10.10 shows a typical matrix obtained by applying the conventional MoM. A darker color on an element indicates a larger magnitude. The matrix elements with $\delta = 0.0002$ for the linear spline case are shown in Figure 10.11. In Figure 10.12, we present the thresholded matrix ($\delta = 0.0025$) for the cubic spline case. The $[A_{\psi\psi}]$ part of the matrix is almost diagonalized. Figure 10.13 gives an idea of the point-wise error in the solution for linear and cubic spline cases.

FIGURE 10.9: Error in the solution of the surface current distribution as a function of the threshold parameter $\delta$.

Reprinted with permission from [23]; copyright © 1995 by IEEE.

![](img/f73ae67732328dc36596b27ffe8d0152_581_0.png)

FIGURE 10.10: A typical gray-scale plot of the matrix elements obtained using conventional MoM. The darker color represents larger magnitude.

![](img/f73ae67732328dc36596b27ffe8d0152_582_0.png)

FIGURE 10.11: A typical gray-scale plot of the matrix elements obtained using linear wavelet MoM. The darker color represents larger magnitude.

Reprinted with permission from [23]; copyright © 1995 by IEEE.

![](img/f73ae67732328dc36596b27ffe8d0152_583_0.png)

FIGURE 10.12: A typical gray-scale plot of the matrix elements obtained using cubic wavelet MoM. The darker color represents larger magnitude.

Reprinted with permission from [23]; copyright © 1995 by IEEE.

![](img/f73ae67732328dc36596b27ffe8d0152_584_0.png)

FIGURE 10.13: The magnitude of the surface current distribution computed using linear ($m = 2$) and cubic ($m = 4$) spline wavelet MoM for different values of the threshold parameter $\delta$.

Reprinted with permission from [23]; copyright © 1995 by IEEE.

δ = 0.0000
δ = 0.0001
δ = 0.0002
δ = 0.0005
m = 2
a = 0.1λ₀
|V_sc| / E₀²
φ

δ = 0.0000
δ = 0.0004
δ = 0.0010
δ = 0.0025
m = 4
a = 0.1λ₀
|V_sc| / E₀²
φ

It is worth pointing out here that regardless of the size of the matrix, only 5 × 5 in the case of the linear spline and 11 × 11 in the case of the cubic splines (see the top-left corners of Figures 10.11 and 10.12) will remain unaffected by thresholding; a significant number of the remaining elements can be set to zero without causing much error in the solution.

## 10.7 SEMIORTHOGONAL VERSUS ORTHOGONAL WAVELETS

Both semiorthogonal and orthogonal wavelets have been used for solving integral equations. A comparative study of their advantages and disadvantages has been reported in [14]. The orthonormal wavelet transformation, because of its unitary similar property, preserves the condition number (κ) of the original impedance matrix A; semiorthogonal wavelets do not. Consequently, the transformed matrix equation may require more iterations to converge to the desired solution. Some results comparing the condition number of matrices for different cases are given in Table 10.2 [17].

TABLE 10.2: Effect of Wavelet Transform Using Semiorthogonal and Orthonormal Wavelets on the Condition Number of the Impedance Matrixᵃ

| Basis and Transform | Number of Unknowns | Octave Level | \(\delta\) | \(S_\xi\) | \(\epsilon_\xi\) | Condition Number \(\kappa\) Before Threshold | Condition Number \(\kappa\) After Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Pulse and none | 64 | N/A | N/A | 0.0 | \(2.6 \times 10^{-5}\) | 14.7 | --- |
| Pulse and Pulse | 64 | 1 | \(7.2 \times 10^{-2}\) | 46.8 | 0.70 | 16.7 | 16.4 |
| Pulse and o.n. | 64 | 1 | \(7.5 \times 10^{-3}\) | 59.7 | 0.87 | 14.7 | 14.5 |

\(^a\)Original impedance matrix is generated using pulse basis functions.

In applying wavelets directly to solve integral equations, one of the most attractive features of semiorthogonal wavelets is that closed-form expressions are available for such wavelets. Most of the continuous o.n. wavelets cannot be written in closed form. One thing to be kept in mind is that, unlike signal processing applications where one usually deals with a discretized signal and decomposition and reconstruction sequences, here in the boundary value problem we often have to compute the wavelet and scaling function values at any given point. For a strip and thin wire case, a comparison of the computation time and sparsity is summarized in Tables 10.3 and 10.4 [14].

TABLE 10.3: Comparison of CPU Time per Matrix Element for Spline, Semiorthogonal, and Orthonormal Basis Function

| | Wire | Plate |
| :--- | :--- | :--- |
| spline | 0.12 s | \(0.25 \times 10^{-3}\) s |
| s.o. wavelet | 0.49 s | 0.19 s |
| o.n. wavelet | 4.79 s | 4.19 s |

Source: Reprinted with permission from [14]; copyright © 1997 by IEEE.

TABLE 10.4: Comparison of Percentage Sparsity ($S_\delta$) and Percentage Relative Error ($\epsilon_\delta$) for Semiorthogonal and Orthonormal Wavelet Impedance Matrices as a Function of Threshold Parameter ($\delta$)

| Scatterer Octave Levels | Number of Unknowns s.o. | o.n. | Threshold \(\delta\) | Sparsity \(S_\delta\) s.o. | o.n. | Relative Error \(\epsilon_\delta\) s.o. | o.n. |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Wire/j = 4 | 29 | 33 | \(1 \times 10^{-6}\) | 34.5 | 24.4 | \(3.4 \times 10^{-3}\) | \(4.3 \times 10^{-3}\) |
| | | | \(5 \times 10^{-6}\) | 48.1 | 34.3 | \(3.9 \times 10^{-3}\) | \(1.3 \times 10^{-3}\) |
| | | | \(1 \times 10^{-5}\) | 51.1 | 36.5 | 16.5 | \(5.5 \times 10^{-2}\) |
| Plate/ j = 2, 3, 4 | 33 | 33 | \(1 \times 10^{-4}\) | 51.6 | 28.1 | \(1 \times 10^{-4}\) | 0.7 |
| | | | \(5 \times 10^{-4}\) | 69.7 | 45.9 | 4.7 | 5.2 |
| | | | \(1 \times 10^{-3}\) | 82.4 | 50.9 | 5.8 | 10.0 |

Source: Reprinted with permission from [14]; copyright © 1997 by IEEE.

As discussed in the previous chapters, semiorthogonal wavelets are symmetric and hence have a generalized linear phase, an important factor in function reconstruction. It is well known [31] that symmetric or antisymmetric, real-valued, continuous, and compactly supported o.n. scaling functions and wavelets do not exist. Finally, in using wavelets to solve spectral domain problems, as discussed before, we need to look at the time-frequency window product of the basis. Semiorthogonal wavelets approach the optimal value of the time-frequency product, which is 0.5, very fast. For instance, this value for the cubic spline wavelet is 0.505. It
