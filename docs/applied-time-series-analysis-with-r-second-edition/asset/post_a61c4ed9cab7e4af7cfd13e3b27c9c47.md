
In this section, we consider the case in which $s_t$ is a function of the form $s_t = C\cos(2\pi ft + \mathcal{V})$. In Chapters 1 and 4, we have discussed models with harmonic components and have studied them as a type of stationary process. The stationarity requires that the phase, $\mathcal{V}$, is a random variable. However, in physical situations in which one realization is available, the phase is constant throughout the only realization observed. For this reason, it is often the case that in signal-plus-noise models with harmonic components, the harmonic term, such as $s_t = C\cos(2\pi ft + \mathcal{V})$ is considered to be a deterministic signal as in the case of the trend-plus-noise examples.

Consider the case of the signal-plus-noise model with one harmonic component

$$X_t = C\cos(2\pi ft + \mathcal{V}) + Z_t,$$  \tag{5.4}

which is usually written as

$$X_t = A\cos(2\pi ft) + B\sin(2\pi ft) + Z_t,$$  \tag{5.5}

where $A = C\cos\mathcal{V}$ and $B = -C\sin\mathcal{V}$ using trigonometric identities. In practice, if $X_t$ satisfies Equation 5.5, the data set is analyzed as if it is a nonstationary process, in which case the parameters $A$, $B$, and $f$ are often estimated as a first step, and then the process

$$\widehat{Z}_t = X_t - \widehat{A}\cos(2\pi \widehat{f}t) - \widehat{B}\sin(2\pi \widehat{f}t),$$  \tag{5.6}

is modeled as a stationary process (see Bhansali 1979). While the noise term in Chapter 4 is often taken to be white noise, this is not a requirement in Equation 5.4, and $\widehat{Z}_t$ is typically modeled as an AR($p$) or ARMA($p,q$) process to allow for autocorrelation.

### EXAMPLE 5.2: LYNX DATA

We return to the lynx data (data set lynx in tswge) shown in Figure 3.15 that represent the annual number of lynx trappings in Canada from 1821 to 1934 (see Campbell and Walker, 1977). We previously considered this data set in Example 3.7 where we noted that because of the asymmetry in the actual lynx data shown in Figure 3.15a, the data have historically been analyzed after first taking the log (base 10) of the number of lynx trapped, and this data set (llynx in tswge) is

shown in Figure 3.15b where it can be seen that the asymmetry is largely removed. Figure 3.15c and d shows the sample autocorrelations and the Parzen spectral density estimate of the log-lynx data where the cyclic behavior of about 10 years is apparent in both plots. A feature to note about the sample autocorrelations is their slowly damping behavior.

We used a simple AR(2) model for the log-lynx data in Example 3.7, but the AR model typically used to model the log-lynx data is the AR(11) model

$(1 - 1.138 B + 0.51 B^2 - 0.238 B^3 + 0.29 B^4 - 0.148 B^5 + 0.14 B^6 + 0.148 B^7 - 0.08 B^8 + 0.04 B^9 - 0.13 B^{10} - 0.19 B^{10} + 0.31 B^{11}) X_t$

proposed by Tong (1977). Also, Campbell and Walker (1977) obtained the harmonic component model

$X_t = 2.9036 + 0.3649 \cos\left(\frac{2\pi t}{9.5}\right) - 0.4866 \sin\left(\frac{2\pi t}{9.5}\right) + u_t,$

where $u_t = 1.0302 u_{t-1} - 0.3228 u_{t-2} + a_t$, and $a_t$ has zero mean and variance 0.044. Bhansali (1979) compared the models and concluded, using Priestley's (1962) $P(\lambda)$ test designed to detect harmonic behavior, that the data contained a harmonic component. However, Woodward and Gray (1983) pointed out that the factored form of the Tong model has a factor of $1 - 1.562 B + 0.967 B^2$ which has roots very close to the unit circle (the absolute reciprocal is $|r^{-1}| = 0.98$) associated with frequency $f_0 = 0.104$ (=1/9.6). Additionally they generated realizations from the AR(11) model, which does not have harmonic components, and found that the Priestley $P(\lambda)$ test usually detected “harmonic components.” The lynx data will be re-examined in Chapter 11 when we discuss cyclic long-memory behavior.

## 5.2 ARIMA(p,d,q) and ARUMA(p,d,q) Processes

The ARIMA(p,d,q) and ARUMA(p,d,q) models defined in Definition 5.1 are useful nonstationary extensions of the ARMA(p,q) model.

### Definition 5.1

1. The *autoregressive integrated moving average process* of orders p, d, and q (ARIMA(p,d,q)) is a process, X_t, whose differences (1 − B)^d X_t satisfy an ARMA(p,q) model (that is, a stationary model) where d is a non-negative integer. We use the notation

φ(B)(1 − B)^d X_t = θ(B)a_t  (5.7)

where all the roots of φ(z) = 0 and θ(z) = 0 are outside the unit circle, and φ(z) and θ(z) have no common factors.

2. The *autoregressive unit root moving average process* of orders p, d, and q (ARUMA(p,d,q)) is an extension of the ARIMA(p,d,q) model to include processes, X_t, for which the process λ(B)X_t satisfies an ARMA(p,q) model where λ(B) = 1 − λ_1 B − ⋯ − λ_d B^d is an operator whose characteristic equation has all its roots (real and/or complex) on the unit circle. We use the notation

φ(B)λ(B)(X_t − μ) = θ(B)a_t  (5.8)

to denote such a process.

It is worth noting that φ(B)λ(B)μ = φ(1)λ(1)μ, and therefore, we can write Equation 5.8 in the form

φ(B)λ(B)X_t = φ(1)λ(1)μ + θ(B)a_t  (5.9)

The term φ(1)λ(1)μ is called the *moving average constant*, and if λ(B) = (1 − B)^d, then λ(1) = 0 and so φ(1)λ(1)μ = 0. This is not true in general for an ARUMA(p,d,q) model, that is, if 1 − B is not a factor of λ(B), then φ(1)λ(1) ≠ 0.

### EXAMPLE 5.3: ARIMA(0, 1, 0) MODELS AND THE DOW JONES 2014 DATA

A realization from an ARIMA(0, 1, 0) process will be similar to those from a stationary AR(1) process with φ_1 close to +1. Consider for example the realization in Figure 3.5a from the AR(1) model (1 − 0.95B)X_t = a_t which shows the characteristic wandering behavior associated with the AR(1) model with a positive real root close to +1.

The spectral density shown in Figure 3.6a has a peak at zero. Figure 3.7a is a realization from $X_t - X_{t-1} = a_t$, that is, $(1 - B)X_t = a_t$ which is an ARIMA(0, 1, 0) model, and the realization in Figure 3.7a shows an accentuated wandering behavior. Although it is not apparent in Figures 3.5a and 3.7a, there is another distinct difference between the wandering behavior for these two models. If we had taken a sufficiently long realization from the stationary AR(1) model $(1 - 0.95B)X_t = a_t$, we would see that the wandering would tend to show some attraction to the mean (in this case $\mu = 0$), that is, the wandering would eventually go back and forth across the mean so that for a long realization the sample average would be close to zero (due to ergodicity). However, the wandering behavior seen in Figure 3.7a from the nonstationary ARIMA(0, 1, 0) model has no attraction to a mean.

Figure 3.8a shows the daily DOW Jones closing averages for 2014. An ARIMA(0, 1, 0) may be a reasonable model for these data because the wandering behavior is obvious and, through the years, the DOW Jones averages have shown no attraction to an overall mean (and have tended to rise in time).

### EXAMPLE 5.4: AN ARUMA(2, 2, 2) PROCESS

Consider the process

$X_t + 0.3X_{t-1} + 0.6X_{t-2} + 0.3X_{t-3} - 0.4X_{t-4} = 9 + a_t + 0.5a_{t-1} + 0.9a_{t-2}$,

which in factored form is given by

$(1 - 0.5B)(1 + 0.8B)(1 + B^2)(X_t - 5) = (1 + 0.5B + 0.9B^2)a_t. \quad (5.10)$

From the factored form in Equation 5.10, it can be seen that $X_t$ satisfies an ARUMA (2, 2, 2) with $\mu = 9 / (\phi(1)\lambda(1)) = 5$ since $Y_t = (1 + B^2)(X_t - 5)$ satisfies the equation

$(1 - 0.5B)(1 + 0.8B)Y_t = a_t + 0.5a_{t-1} + 0.9a_{t-2}$

and $Y_t$ is stationary with $E[Y_t] = 0$.

### 5.2.1 Extended Autocorrelations of an ARUMA(p,d,q) Process

Although it is not possible to directly define the autocovariances of an ARUMA$(p,d,q)$ process with $d > 0$, it is possible to define an “extended” autocorrelation of such a process in a meaningful way. To this end, we provide the following definition.

### Definition 5.2

Let $r_1, r_2, \ldots, r_{p+d}$ be the roots of $\phi(r)=0$, and let $\rho_k=\rho(k,r_1,r_2,\ldots,r_{p+d},\theta)$ denote the autocorrelations of a stationary ARMA $(p+d,q)$ process. Now suppose that the first $d$ of the $r_j$ approach the unit circle uniformly, that is, $|r_j|=|r_m|$ for $j,m\le d$. We denote these $d$ roots by $r_1,r_2,\ldots,r_d$. We define the extended autocorrelation of an ARUMA$(p,d,q)$ process as $\rho_k^*$, where $\rho_k^*$ is the limit of $\rho_k$ as the roots $r_j$, $j=1,\ldots,d$, approach the unit circle uniformly. That is

$$\rho_k^* = \lim_{\substack{|r_1|=|r_2|=\cdots=|r_d|\to 1}} \rho(k,r_1,r_2,\ldots,r_{p+d},\theta). \tag{5.11}$$

### EXAMPLE 5.5: AR(3) MODELS WITH ROOTS CLOSE TO +1

In Example 3.14, we illustrated the fact that the behavior of a (stationary) ARMA$(p,q)$ process tends to be dominated by the roots of $\phi(r)=0$ that are near the unit circle. Figure 5.2 shows the autocorrelations from the AR(3) models

$$(1-\alpha_1B)(1-1.2B+0.8B^2)X_t=a_t. \tag{5.12}$$

where $\alpha_1=0.8,\ 0.95,$ and $0.995$, respectively. The factor table is shown in Table 5.2 where it can be seen that there is a positive real root $(\alpha_1^{-1})$ and a pair of complex conjugate roots associated with the system frequency $f=0.13$. Figure 5.2 shows true autocorrelations for these models while Figure 5.3 shows realizations of length $n=200$ from the three models. Again, as in Example 3.14, it should be noticed that as $\alpha_1\to1$ (i.e. as the positive real root of the characteristic equation approaches the unit circle) the behavior associated with the positive real root becomes more dominant in the autocorrelations and in the
