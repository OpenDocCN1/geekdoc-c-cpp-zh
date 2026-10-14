
+   19. Strauss, T., Fan, X., Sun, S., & Khan, T. (2015). Statistical inversion of absolute permeability in single-phase darcy flow. *Procedia Computer Science*, 51, 1188–1197.
+   20. Jin, B., & Maass, P. (2012). An analysis of electrical impedance tomography with applications to Tikhonov regularization. *ESAIM: Control, Optimisation and Calculus of Variations*, 18(04), 1027–1048.
+   21. Jin, B., Khan, T., & Maass, P. (2012). A reconstruction algorithm for electrical impedance tomography based on sparsity regularization. *International Journal for Numerical Methods in Engineering*, 89(3), 337–353.
+   22. Khan, T., & Smirnova, A. (2005). 1D inverse problem in diffusion based optical tomography using iteratively regularized Gauss-Newton algorithm. *Applied Mathematics and Computation*, 161(1), 149–170.
+   23. Kirsh, A., & Grinberg, N. (2008). *The Factorization Method for Inverse Problems*. Oxford University Press.
+   24. Isaacson, D., Mueller, J. L., Newell, J. C., & Siltanen, S. (2004). Reconstructions of chest phantoms by the D-bar method for electrical impedance tomography. *IEEE Transactions on Medical Imaging*, 23(7), 821–828.
+   25. Kaipio, J.P., Kolehmainen, V., Somersalo, E., & Vauhkonen, M. (2000). Statistical inversion and Monte Carlo sampling methods in electrical impedance tomography. *Inverse Problems*, 16(5), 1487.
+   26. Kaipio, J.P., Seppänen, A., Somersalo, E., & Haario, H. (2004). Posterior covariance related optimal current patterns in electrical impedance tomography. *Inverse Problems*, 20(3), 919.
+   27. Nissinen, A., Heikkinen, L.M., & Kaipio, J.P. (2008). The Bayesian approximation error approach for electrical impedance tomography experimental results. *Measurement Science and Technology*, 19(1), 015501.
+   28. Nissinen, A., Heikkinen, L.M., Kolehmainen, V., & Kaipio, J.P. (2009). Compensation of errors due to discretization, domain truncation and unknown contact impedances in electrical impedance tomography. *Measurement Science and Technology*, 20(10), 105504.
+   29. Jin, B., & Maass, P. (2012). Sparsity regularization for parameter identification problems. *Inverse Problems*, 28(12), 123001.
+   30. Smirnova, Alexandra, Renaud, Rosemary A., & Khan, Taufiquar. (2007). Convergence and application of a modified iteratively regularized Gauss-Newton algorithm. *Inverse Problems*, 23, 1547–1563.
+   31. Bakushinsky, A.B., & Smirnova, A. (2005). On application of generalized discrepancy principle to iterative methods for nonlinear ill-posed problems, *Numer. Func. Anal. Optim.*, 26, 35–48.
+   32. Nocedal, J., & Wright, S.J. (1999). *Numerical Optimization*, Springer, NY.
+   33. Chib, S., & Greenberg, E. (1995). Understanding the metropolis-hastings algorithm. *The American Statistician*, 49(4), 327–335.
+   34. Bardsley, J.M. (2012). MCMC-based image reconstruction with uncertainty quantification. *SIAM Journal on Scientific Computing*, 34(3), A1316–A1332.

## 6

## On an Efficient Family of Steffensen-Like Methods for Finding Nonlinear Equations

Vali Torkashvand and Manochehr Kazemi

## CONTENTS

-   6.1 Introduction................................................................................................................ 91
-   6.2 A Class of Without-Memory Methods................................................................................................ 92
-   6.3 The New Methods with Memory ....................................................................................................... 94
-   6.4 Numerical Examples ........................................................................................................................... 96
-   6.5 Conclusion .......................................................................................................................................... 98
-   References............................................................................................................................................... 101

### 6.1 Introduction

Nonlinear equations are ubiquitous in many areas of applied mathematics and play vital roles in a number of applications such as science and engineering. Nonlinear equations are usually difficult to solve analytically, therefore a numerical method is needed. Construction of iterative methods to approximate a solution for solving nonlinear equation f(x)=0 is one of the most important tasks in applied mathematics. The best-known iterative method for determining the solution of this problem is Newton’s method (NM) given by x_{k+1}=x_k - f(x_k)/f'(x_k), which produces a sequence {x_n} quadratically convergent to the simple root α, if the initial approximation x_0 is sufficiently close to α and f' exists near α. The key idea by Traub [16] that provides the order acceleration lies in a special form of the error relation and a convenient choice of a free parameter. We define a self-accelerating parameter, which is calculated during the iterative process using Newton’s interpolating polynomial. Accelerating technique relies on information from the current and the previous iterative step, defining in this way two-point methods with memory. The rest of this chapter is organized as follows: Section 6.2 is devoted to modifications of the two steps of Guo and Qian methods [11]. Section 6.3 is concerned with developing new with-memory methods. Section 6.4 includes some numerical performances and conclusions are made in Section 6.5.

### 6.2 A Class of Without-Memory Methods

In 2015 Guo and Qian followed the two-point methods without memory (GQM) [11]:

\begin{cases} w_k = x_k + f(x_k), y_k = x_k - \dfrac{f(x_k)}{f[x_k, w_k]}, \quad k = 0,1,2,\dots, \\ x_{k+1} = y_k - \dfrac{(x_k - y_k)(x_k - w_k)(y_k - w_k)f(y_k)}{(y_k - w_k)^2 f(x_k) + (x_k - w_k)(x_k - 2y_k + w_k)f(y_k) - (x_k - y_k)^2 f(w_k)}. \end{cases} (6.1)

The next theorem states the error equations in the methods in Equation (6.1).

# Theorem 6.1 Let I ⊆ ℝ be an open interval, f : I → ℝ be a scalar function which has a simple root α in the open interval I, and also the initial approximation x₀ is sufficiently close the simple zero, then the iteration method defined by (1) is of fourth-order convergence and it satisfies the error equation below:

e_{k+1} = (1 + f'(α))^2 c_2 (c_2^2 - c_3) e_k^4 + O(e_k^5). (6.2)

# Proof 6.1 The proof is given in Guo and Qian [11].

By imposing two parameters in the method described in Equation (6.1), the family of two-parameters without-memory method of the following fourth-order result (TKM4):

\begin{cases} w_k = x_k + γ f(x_k), y_k = x_k - \dfrac{f(x_k)}{f[x_k, w_k] + λ f(w_k)}, \quad k = 0,1,2,\dots, \\ x_{k+1} = y_k - \dfrac{(x_k - y_k)(x_k - w_k)(y_k - w_k)f(y_k)}{(y_k - w_k)^2 f(x_k) + (x_k - w_k)(x_k - 2y_k + w_k)f(y_k) - (x_k - y_k)^2 f(w_k)}. \end{cases} (6.3)

Where γ ∈ ℝ. The next theorem states the error equations in the methods of Equation (6.3).

# Theorem 6.2 Let I ⊆ ℝ be an open interval, f : I → ℝ be a scalar function which has a simple root α in the open interval I, and also the initial approximation x₀ is sufficiently close the simple zero, then, the iteration method (3) has fourth-order convergence and satisfies the following error equation:

e_{k+1} = (1 + f'(α)γ)^2 (λ + c_2)(c_2(λ + c_2) - c_3) e_k^4 + O(e_k^5). (6.4)

wherein c_k = f^k(α)/k!, ∀k ∈ {2,3,4,⋯}, e_k = x_k - α and λ, γ are two real valued free parameters.

# Proof 6.2 Using Taylor's series and symbolic computation; we can determine the asymptotic error constant of the two-step without memory family of methods (3). Now we expand f(x_k) about the simple zero α. Hence, we have

f(x_k) = f'(α)[e_k + c_2 e_k^2 + c_3 e_k^3 + c_4 e_k^4 + O(e_k^5)], (6.5)

and

$$w_k-\alpha=x_k-\alpha-e_kf'(\alpha)\gamma\left(1+e_k\left(c_2+c_3e_k^3+c_4e_k^4\right)\right), \tag{6.6}$$

Using the first-order divided difference of the function $f[x,w]=\dfrac{f(x)-f(w)}{x-w}$, we have:

$$f[x_k,w_k]=\frac{1}{e_k\gamma\left(1+e_k\left(c_2e_k(c_3+c_4e_k)\right)\right)}\Big(e_k^2c_2+e_k^3c_3+e_k^4c_4+e_kf'(\alpha)\gamma(1$$
$$\quad+e_k(c_2e_k(c_3+c_4e_k)))-c_2(e_k-e_kf'(\alpha)\gamma(1+e_k(c_2+e_k(c_3+e_kc_4))))^4$$
$$\quad-c_3(e_k-e_kf'(\alpha)\gamma(1+e_k(c_2+e_k(c_3+e_kc_4))))^4-c_4(e_k-e_k\gamma f'(\alpha)$$
$$\quad\cdot(1+e_k(c_2+e_k(c_3+e_kc_4))))^4\Big)$$

Furthermore, it is easy to find:

$$\frac{f(x_k)}{f[x_k,w_k]+\lambda f(w_k)}=(e_kf'(\alpha)(1+e_k(c_2+e_kc_3)))\Big/\Big([[c_2e_k^2+e_k^3c_3+e_k\gamma f'(\alpha)$$
$$\quad\cdot(1+e_k(c_2+e_kc_3))-c_2(e_k-e_kf'(\alpha)(1+e_k(c_2+e_kc_3)))^2$$
$$\quad-c_3(e_k-e_k\gamma f'(\alpha)(e_kf'(\alpha)(1+e_k(c_2+e_kc_3))^3)]/e_k\gamma(1+e_k(c_2$$
$$\quad+e_kc_3))|f'(\alpha)\lambda(e_k-e_k\gamma f'(\alpha)(1+e_k(c_2+e_kc_3)))+c_2(e_k$$
$$\quad-e_k\gamma f'(\alpha)(1+e_k(c_2+c_3e_k))^2+c_3(e_k-e_k\gamma f'(\alpha)(1+e_k(c_2$$
$$\quad+e_kc_3))+c_2(e_k-e_k\gamma f'(\alpha)e_kc_3)))^3\Big)$$

Using Equation (6.7) and some simplifications, we get:

$$y_k-\alpha=x_k-\alpha-\frac{f(x_k)}{f[x_k,w_k]+\lambda f(w_k)}=-( -1+f'(\alpha)\gamma)(\lambda+c_2)e_k^2+(\lambda^2(-1+f'(\alpha)\gamma)^2$$
$$\quad-2f'(\alpha)\gamma)(-2+\gamma f'(\alpha))c_2+(\lambda+c_2)+2c_3+f'(\alpha)\gamma)(-3+f'(\alpha)\gamma)c_3]e_k^3$$
$$\quad+(-\lambda^3(-1+f'(\alpha)\gamma)^3+\lambda(5-f'(\alpha)\gamma(7+f'(\alpha)\gamma(-4-f'(\alpha)\gamma)))c_2^2$$
$$\quad+(4-\gamma f'(\alpha)(5+f'(\alpha)\gamma(-3+f'(\alpha)\gamma)))c_2^3+\lambda(-4+f'(\alpha)\gamma(7+f'(\alpha)\gamma(-5$$
$$\quad+f'(\alpha)\gamma)))c_3+c_2(-\lambda^2(-1+f'(\alpha)\gamma(3+f'(\alpha)\gamma(-2+f'(\alpha)\gamma))+( -7+f'(\alpha)$$
$$\quad\cdot\gamma(10+f'(\alpha)\gamma(-7+2f'(\alpha)\gamma)))c_3)(3+f'(\alpha)\gamma(-3+f'(\alpha)\gamma)c_4)e_k^4+O(e_k^5)$$
