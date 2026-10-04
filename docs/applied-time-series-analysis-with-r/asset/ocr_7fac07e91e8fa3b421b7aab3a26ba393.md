# ARMA Time Series Models

$$\rho_2 = \frac{-	heta_2}{1+\theta_1^2+\theta_2^2}, \ \rho_k=0, k \ge 3.$

Using Equation 3.6, the spectral density of the MA(2) process is given by

$S_X(f)=\frac{\sigma_2^2}{[1+\theta_1^2+\theta_2^2-2\theta_1(1-\theta_2)\cos 2\pi-2\theta_2\cos 4\pi]}.$

**Using R:** The twsg function arma.wge can be used to generate and plot a realization from an MA model, *true.arma.aut* *true.arma.spec.wge* calculate and plot the true autocorrelations and spectral densities for an MA model, respectively. Additionally, the twsg function plots.true.wge can be used to generate a realization, calculate the true autocorrelations and spectral density, and create a plot Figure 3.11 in this text. Be careful with the coefficients. That is, for the MA(2) model $X_t = a_t-1.1a_{t-1}+0.6a_{t-2}$ the coefficients $\theta_1$ and $\theta_2$ are 1.1, and $-0.6$, respectively. These twsg functions can also be used for AR and ARMA models which will be discussed in the future. See Appendix 3B for more details.

# 3.2 AR Processes

Let $a_t$, be a white noise process and if $X_t$, $t=0, \pm1,\dots$, $\phi_p$ be real constants with $\phi_p \neq 0$. Then, loosely speaking, is specified by

$X_t-\mu-\phi_1(X_{t-1}-\mu)-\phi_2(X_{t-2}-\mu)-\dots-\phi_p(X_{t-p}-\mu)=a_t, \quad (3.13)$

then $X$, is called an AR process of order $p$, which is usually shortened to AR(p). We will write Equation 3.13 in the operator form

$$\phi(B)(X_t-\\mu)=a_t, \quad (3.14)$

where

the AR(p) model in Equation 3.14 can be rewritten in the form $\phi(B)X_t=\phi(B)\mu+a_t$, by noting that

$$\phi(B)\mu=(1-\phi_1B-\dots-\\phi_pB^p)\mu \n ==(1-\phi_1-\dots-\phiphi_p)\mu \n ==\phi(1)\mu,$