
where $L(x,t)=\int_0^r K(x+p,t)\,dp$, $G(x)=\int_0^r g(x+p)\,dp$ and $\alpha=\int_0^r\int_0^p K(x+p,x+t)\,dt\,dp$.

$$\sum_{n=1}^{2^{k-1}}\sum_{m=0}^{M-1}c_{n,m}\left(H_{n,m}(x)+\psi_{n,m}(x)\alpha\right)=G(x), \tag{24.16}$$

where $H_{n,m}(x)=\int_0^x L(x,t)\psi_{n,m}(t)\,dt$. Collocation points are defined as

$$x_i=\frac{2i-1}{2p},\quad i=1,2,\ldots,p,$$

where $p=2^{k-1}M$. Satisfying Equation (24.15) at collocation points $x_i$, yields a linear system of equations. In matrix notation, we write

$$C(H+\Psi\alpha)=G,$$

where $G=[G(x_0),G(x_1),G(x_2),\ldots,G(x_p)]^T$,

$$\Psi=\begin{bmatrix}
\psi_{1,0}(x_1)&\psi_{1,0}(x_2)&\cdots&\psi_{1,0}(x_p)\\
\psi_{1,1}(x_1)&\psi_{1,1}(x_2)&\cdots&\psi_{1,1}(x_p)\\
\vdots&\vdots&\ddots&\vdots\\
\psi_{1,M-1}(x_1)&\psi_{1,M-1}(x_2)&\cdots&\psi_{1,M-1}(x_p)\\
\psi_{2,0}(x_1)&\psi_{2,0}(x_2)&\cdots&\psi_{2,0}(x_p)\\
\vdots&\vdots&\ddots&\vdots\\
\psi_{2^{k-1},M-1}(x_1)&\psi_{2^{k-1},M-1}(x_2)&\cdots&\psi_{2^{k-1},M-1}(x_p)
\end{bmatrix}$$

and

$$H=\begin{bmatrix}
H_{1,0}(x_1)&H_{1,0}(x_2)&\cdots&H_{1,0}(x_p)\\
H_{1,1}(x_1)&H_{1,1}(x_2)&\cdots&H_{1,1}(x_p)\\
\vdots&\vdots&\ddots&\vdots\\
H_{1,M-1}(x_1)&H_{1,M-1}(x_2)&\cdots&H_{1,M-1}(x_p)\\
H_{2,0}(x_1)&H_{2,0}(x_2)&\cdots&H_{2,0}(x_p)\\
\vdots&\vdots&\ddots&\vdots\\
H_{2^{k-1},M-1}(x_1)&H_{2^{k-1},M-1}(x_2)&\cdots&H_{2^{k-1},M-1}(x_p)
\end{bmatrix}$$

$$C=G(H+\Psi\alpha)^{-1}. \tag{24.17}$$

The wavelet coefficients $C=\{c_{n,m}\}$ are calculated by using Equation (24.17). Then using the values of $c_{n,m}$, the function $f(x)$ can be obtained by using Equation (24.13).

Nonlinear Volterra integral equations can also be handled using the proposed method. First, we will convert a nonlinear equation into a linear Volterra integral equation by substituting

Y(f(x)) = v(x).

Then after finding solution to this linear equation using the method explained above, the value of f(x) can be obtained by

f(x) = Y^{-1}(v(x)).

To check the accuracy of the proposed method, we use root mean square error (RMS) and maximum absolute error (MAE) given by

RMS = ( 1/N sum_{i=1}^{N} | f(x_i) - f_{ex}(x_i) |^2 )^{1/2}, MAE = max_{1 <= i <= N} | f(x_i) - f_{ex}(x_i) |,

where f(x_i) and f_{ex}(x_i) are numerical and exact solution and N is the number of points.

Now the question is what value of r should be chosen to find accurate results. We start with r=0.1 and decrease the value of α until the numerical solution converges to the exact solution of integral equation. We have chosen that value of r for which the root mean square (RMS) attained is minimum. For practical problems, we do not know the exact solution and so finding the optimal value of α is difficult. In that case, the value of the regularization parameter is chosen depending upon the a priori information about the solution.

## 24.4 Error Analysis

We present the following convergence theorem for Legendre wavelet basis.

Theorem 24.1 [11] Let f(x) be a function defined on [0,1) with bounded second derivative, say | f''(x) | ≤ M, and sum_{n=1}^{∞} sum_{m=0}^{∞} c_{n,m} ψ_{n,m}(x) be its infinite Legendre wavelets expansion, then |c_{n,m}| ≤ sqrt(12M) / [ (2n)^{5/2} (2M - 3)^2 ].

This means the Legendre wavelets series converges uniformly to f(x) and f(x) = sum_{n=1}^{∞} sum_{m=0}^{∞} c_{n,m} ψ_{n,m}(x).

Theorem 24.2 [11] Suppose f(x) be a continuous function defined on [0,1), with a second derivative f''(x) bounded by M, then we have the following accuracy estimation

‖ f(x) − f_{n,m}(x) ‖ = ‖ e_n ‖_2 ≤ ( 3M²/2 ∑_{n=1}^{∞} ∑_{m=M}^{∞} 1/(n⁵(2m−3)⁴) + 3M²/2 ∑_{n=2^{k−1}+1}^{∞} ∑_{m=0}^{M−1} 1/(n⁵(2m−3)⁴) )^{1/2} (24.18)

We have applied Legendre wavelets to Equation (24.12) which is a second-kind Volterra integral equation. Writing Equation (24.12) in simplified form we get

∫₀ˣ K(x,t) f(t) dt + α f(x) = g(x) (24.19)

Let f_{n,m}(x) be the approximate value of function f(x) obtained by truncating the Legendre wavelet for some suitable value of M and k. If we use the approximate value of f(t) in Equation (24.19), the function g(x) will also differ from its actual value (let us denote it by g_{n,m}(x)), we have

∫₀ˣ K(x,t) f_{n,m}(t) dt + f_{n,m}(x) α = g_{n,m}(x) (24.20)

Subtracting Equation (24.20) from Equation (24.19), we get

g_{n,m}(x) − g(x) = ∫₀ˣ K(x,t)(f_{n,m}(t) − f(t)) dt + (f_{n,m}(x) − f(x)) α

which is again a second-kind integral equation. Taking L² norm, we have

‖ g(x) − g_{n,m}(x) ‖ = ‖ ∫₀ˣ K(x,t)(f_{n,m}(t) − f(t)) dt + (f_{n,m}(x) − f(x)) α ‖ ≤ ‖ ∫₀ˣ K(x,t)(f_{n,m}(t) − f(t)) dt ‖ + ‖ (f_{n,m}(x) − f(x)) α ‖ ≤ ∫₀ˣ ‖ K(x,t)(f_{n,m}(t) − f(t)) ‖ dt + ‖ (f_{n,m}(x) − f(x)) α ‖ ≤ ∫₀ˣ ‖ K(x,t) ‖ ‖ (f_{n,m}(t) − f(t)) ‖ dt + ‖ (f_{n,m}(x) − f(x)) ‖ |α| = ‖ (f_{n,m}(x) − f(x)) ‖ ( ∫₀ˣ ‖ K(x,t) ‖ dt + |α| )

Assuming K(x, t) to be bounded by U on [0,1], and using Equation (24.18), we have

‖ g(x) − g_{n,m}(x) ‖ ≤ (|α| + U) ( 3M²/2 ∑_{n=1}^{∞} ∑_{m=M}^{∞} 1/(n⁵(2m−3)⁴) + 3M²/2 ∑_{n=2^{k−1}+1}^{∞} ∑_{m=0}^{M−1} 1/(n⁵(2m−3)⁴) )^{1/2} (24.21)

Equation (24.21) gives the upper bound for the error. We can see that as the value of m and n become large, the function $g_{n,m}(x)$ converges to function $g(x)$.

## 24.5 Numerical Examples

We will present the numerical solution to some problems of Volterra integral equations of the first kind. The numerical results presented in this chapter are obtained using $k=3$, $M=3$, i.e., 12 collocation points. All the computations are performed with help of Matlab.

### Example 5.1 Solve the following integral equation

$$\int_{0}^{x} \cos(x-t) f(t) dt = x \sin x, \ 0 \le x < 1.$$

The exact solution is $f(x)=2\sin x$.

The numerical solution converges to the exact solution for $r=10^{-3}$. The RMS and MAE obtained are 9.90872e-05 and 1.57312e-04 respectively. Table 24.1 shows the numerical results for Example 1. The error obtained is less than the method discussed in [2] using 64 and 128 collocation points. Maleknejad [10] used Haar wavelets with 128 elements and MAE obtained is 0.01, which is very large as compared to our method where we have used 12 collocation points. The results obtained by the proposed method are better as compared to the methods presented in [2] and [10].

### Example 5.2 Solve the following first kind Volterra integral equation:

$$\int_{0}^{x} e^{x+t} f(t) dt = x e^{x}, \ 0 \le x < 1.$$

The exact solution is $f(x)=e^{-x}$.

#### TABLE 24.1
Numerical Results for Example 1

| x | Exact Solution $f_{ex}(x)$ | Approximate Solution $f(x)$ | Error $|f_{ex}(x)-f(x)|$ |
|---|---|---|---|
| 0 | 0 | -0.00007965 | 7.96550793e-05 |
| 0.1 | 0.19966683 | 0.19963722 | 2.96138005e-05 |
| 0.2 | 0.39733866 | 0.3974936 | 1.54965758e-04 |
| 0.3 | 0.59104041 | 0.5908831 | 1.57311985e-04 |
| 0.4 | 0.77883668 | 0.77886882 | 3.21418644e-05 |
| 0.5 | 0.95885107 | 0.95880658 | 4.44903973e-05 |
| 0.6 | 1.12928494 | 1.12925794 | 2.70043350e-05 |
| 0.7 | 1.28843537 | 1.28856879 | 1.33420386e-04 |
| 0.8 | 1.43471218 | 1.43457363 | 1.38551225e-04 |
| 0.9 | 1.56665381 | 1.56669203 | 3.82122340e-05 |

The exact and approximate solutions are compared in Table 24.2. For r=10⁻⁷, the RMS value obtained is 4.25832179e-05. In [2], 32 and 64 collocation points are used to solve the equation and the error obtained is of the order 10⁻⁴, which is larger than the error obtained by our method which uses only 12 collocation points. Also, the MAE obtained is 6.66114205e-04 whereas the MAE in [10] using 128 elements is 0.005. So, we can say that the present method works better than the methods in [2] and [10].

### Example 5.3 Consider the following integral equation:

∫₀ˣ cos(x−t) f''(t) dt = 2 sin x, 0 ≤ x < 1,

with initial conditions y(0)=0, y'(0)=0.
The exact solution to this equation is given by f(x)=x².
The RMS and MAE for r=10⁻³ are given as
RMS = 1.09713545e−18 and MAE = 3.46944695e−18.

Table 24.3 shows the numerical results using the proposed method which are in good agreement with the exact solution. In [13] this problem is solved using different collocation points and MAE obtained are of the order 10⁻¹⁶ whereas our method gives a maximum absolute error of the order 10⁻¹⁸. We can see that our method gives more accuracy than the Haar wavelet method given in [13].

### Example 5.4 Consider the following integral equation:

∫₀ˣ cos(x−t) f''(t) dt = 6(1−cos x), 0 ≤ x < 1,

with initial conditions y(0)=0, y'(0)=0 and exact solution is given by f(x)=x³.
For r=10⁻⁵, the RMS value is 4.15754221e-04. The results obtained are shown in Table 24.4 which shows that the method gives good results. Singh et al. [13] have solved this example using Haar wavelet with 16 collocation points and the MAE obtained is 2.1e-03 whereas the MAE in our method using 16 collocation points is 7.81250052e-04.

#### TABLE 24.2
Numerical Results for Example 2

| x | Exact Solution f_ex(x) | Approximate Solution f(x) | Error |f_ex(x)−f(x)| |
|---|---|---|---|---|
| 0 | 1 | 0.99994741 | 5.25849051e-05 |
| 0.1 | 0.90483742 | 0.90482634 | 1.10749066e-05 |
| 0.2 | 0.81873075 | 0.81879610 | 6.53475231e-05 |
| 0.3 | 0.74081822 | 0.74075160 | 6.66114204e-05 |
| 0.4 | 0.67032004 | 0.67033623 | 1.61860716e-05 |
| 0.5 | 0.60653065 | 0.60654908 | 1.84196434e-05 |
| 0.6 | 0.54881163 | 0.54879850 | 1.3130883e-05 |
| 0.7 | 0.49658530 | 0.49663733 | 5.20355253e-05 |
| 0.8 | 0.44932896 | 0.44927604 | 5.29170127e-05 |
| 0.9 | 0.40656965 | 0.40658567 | 1.60138249e-05 |
