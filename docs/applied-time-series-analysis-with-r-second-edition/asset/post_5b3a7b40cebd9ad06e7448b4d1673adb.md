
## FIGURE 8.12

(a) Realization in Figure 8.11a differenced. (b) Sample autocorrelations for the differenced data in (a). (c) AR(4) spectral density estimate for (a). (d) Parzen spectral density estimate for (a).

(1 − B)(1 − 1.74B + 1.64B² − 1.49B³ + 0.71B⁴)X_t = a_t.  (8.32)

The factor table associated with the fitted model in Equation 8.32 is given in Table 8.8.

As suggested in Section 7.8, the associated ARUMA(4,1,0) spectral density estimate is plotted using the ARMA(5,0) spectral density estimate associated with a nearly nonstationary model such as

(1 − 0.995B)(1 + 0.9B²)(1 − 1.79B + 0.85B²)X_t = a_t.  (8.33)

The resulting ARUMA spectral density estimate is shown in Figure 8.11c, and in Figure 8.11d we show the corresponding Parzen spectral density estimator. Notice that in the ARUMA spectral density estimate there is only a somewhat weak indication of the system frequency at f = 0.04 while in the Parzen spectral density estimate there is no indication at all. This illustrates the important fact that frequency information is often more visible in the factor table than it is in the spectral density.

## Table 8.8

Factor Table for the ARUMA(4,1,0) Model in Equation 8.32

| AR Factors | Roots (r_j) | |r_j^{-1}| | f0j |
|---|---|---|---|
| 1 − B | 1 | 1 | 0.0 |
| 1 + 0.02B + 0.85B² | −0.01 ± 1.08i | 0.92 | 0.25 |
| 1 − 1.77B + 0.83B² | 1.06 ± 0.27i | 0.91 | 0.04 |

The problem is that the peak in the spectral density at the frequency associated with the nonstationary factor (in this case f = 0) dominates the contribution in the spectral density associated with frequencies nearby (in this case f = 0.04). One technique to more clearly see the more subtle features of the spectral density is to transform the data to

$$\begin{aligned}\rho_k &= 0 && \text{for } k>q,\\ \rho_k &\ne 0 && \text{for } k=q.\end{aligned} \tag{8A.1}$$

The behavior described in (8A.1) uniquely determines the order $q$ of an MA($q$) process if the true autocorrelations are known. Thus, sample autocorrelations that are near zero for $k>q$ while $\hat{\rho}_q=0$ suggest an MA($q$) as a possible model. From Bartlett’s (1946) approximation in Equation 1.22 it follows that if $X_t$ is an MA($q$) process, then

$$\operatorname{Var}(\hat{\rho}_k)\approx \frac{1}{n}\left(1+2\sum_{v=1}^{q}\rho_v^2\right).$$

for $k>q$. Further, since $E[\hat{\rho}_k]\approx 0$ for $k>q$, then a rough guide is that if

$$\left|\hat{\rho}_k\right|>2\sqrt{\frac{1+2\sum_{v=1}^{q}\hat{\rho}_v^2}{n}}, \tag{8A.2}$$

for some $k>q$, then this is evidence against an MA($q$) at the $\alpha=0.05$ level of significance. Thus, if an MA($q$) is to be considered as the model, then $\hat{\rho}_k$ should essentially remain within the limits specified by Equation 8A.2 for $k>q$. However, as with the test for white noise, the quoted significance level applies separately for each $k$ so that it will not be unusual to observe a small percentage of $\hat{\rho}_k$’s, $k\ge q$, outside the specified limits when the model is an MA($q$). It should be noted that when $X_t$ is white noise, that is, $X_t$ is MA($q$) with $q=0$, then the summation in Equation 8A.2 is taken to be zero, and Equation 8A.2 reduces to Equation 8.1.

## EXAMPLE 8A.1: MODEL IDENTIFICATION BASED ON SAMPLE AUTOCORRELATIONS

Figure 8A.1a shows a realization of length $n=100$ from the MA(3) process

$$X_t=a_t-0.7a_{t-1}-0.54a_{t-2}+0.81a_{t-3}. \tag{8A.3}$$

Figure 8A.1b is a plot of the true autocorrelations, and Figure 8A.1c shows the sample autocorrelations with limits obtained based on

Equation 8A.2. There it can be seen that $\hat{\rho}_k$, $k = 1, 2, 3$ are similar to the theoretical quantities, and $\hat{\rho}_k$, $k > 3$ are near zero. The limits associated with lag $k$ are plotted at

$\pm 2 \sqrt{\frac{1 + 2 \sum_{v=1}^k \hat{\rho}_v^2}{n}}$  (8A.4)

that is, these are the limits based on Equation 8A.2 where $q = k$. Thus, at each lag $k$, the limits shown are those for checking $\rho_j = 0$ for a given $j > k$. To test for an MA($k$) model, one would essentially compare $\hat{\rho}_j$, $j > k$, to the limits in Equation 8A.4 associated with an MA($k$). We see that the sample autocorrelations, $\hat{\rho}_j$, stay within these limits for $j > 3$, and $\hat{\rho}_3$ is outside the limits. Thus, an MA(3) seems to be an appropriate model.

![](img/a0e0259119deb8c7b41dfd4f664e541d_433_0.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_433_1.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_433_2.png)

## FIGURE 8A.1

(a) Realization from the MA(3) model in Equation 8A.3. (b) True autocorrelations from the model in Equation 8A.3. (c) Sample autocorrelations with MA(q) limits.

## EXAMPLE 8A.2: THE NEED FOR CAUTION WHEN USING AUTOCORRELATIONS FOR MODEL IDENTIFICATION

Care needs to be exercised before an MA(q) model is selected in the manner suggested above. In Figure 8A.2c we plot sample autocorrelations, and it should be noted that they fall within the limit lines for j > 2 suggesting an MA(2). However, the autocorrelations are actually based on the realization of length n = 150 shown in Figure 8A.2a from the AR(1) model

$$X_t - 0.65 X_{t-1} = a_t$$ (8A.5)

Examination of Figure 8A.2c reveals that the sample autocorrelations tend to damp exponentially toward zero as would be expected for an AR(1) with positive φ₁. The corresponding true autocorrelations are shown in Figure 8A.2b. Because of this damping, the sample autocorrelations eventually tend to remain within the limits associated with some MA(k), which in this case is k = 3. This illustrates the fact that one must make a judgment concerning whether:

![](img/a0e0259119deb8c7b41dfd4f664e541d_435_0.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_435_1.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_435_2.png)

## FIGURE 8A.2

(a) Realization and (b) sample autocorrelations from the near-nonstationary AR(3) model in Equation 8.13.

- 1. The autocorrelations have “died out” like mixtures of damped exponentials and/or sinusoids as would be consistent with many AR(p) and ARMA(p,q) models with p > 0, or
- 2. The decay to zero is abrupt as in Figure 8A.1 which is typical of MA(q) processes.

The use of partial autocorrelations helps with the above decision.

## 8A.2 Patterns in Partial Autocorrelations

It was shown in Section 3.2 that the autocorrelations of an AR(p) process behave

## EXAMPLE 8A.3: MODEL IDENTIFICATION BASED ON SAMPLE PARTIAL AUTOCORRELATIONS

In Figure 8A.3a, we show the true autocorrelations, and in Figure 8A.3c we show the true partial autocorrelations for the AR(3) model

In Figure 8A.3b and d, we show the sample autocorrelations and sample partial autocorrelations respectively from a realization (not shown) of length n = 200 from the model in Equation 8A.9. Examination of the true and sample autocorrelations in Figure 8A.3a and b gives us very little information concerning the fact that the model is an AR(3). In fact the damped sinusoidal nature is similar to that seen in several examples of AR(2) models in Chapter 3. However, in Figure 8A.3c it is clear that the associated model is an AR(3) since the true partial autocorrelation at k = 3 is nonzero while those for k > 3 are zero. The sample partial autocorrelations in Figure 8A.3d clearly show the AR(3) behavior, and the model identification of the process is as an AR(3).

$X_t - 0.7 X_{t-1} - 0.54 X_{t-2} + 0.81 X_{t-3} = a_t.$
(8A.9)

homogeneous difference equation with constant coefficients for k > q. The Box–Jenkins procedure is based on the fact that the functional form of the solution is satisfied by ρ_k for k > q − p. Unfortunately these types of patterns do not provide perfect identification even when true quantities are known, and model identification is even more difficult when only the sample autocorrelations and sample partial autocorrelations are available.

## EXAMPLE 8A.4: BOX–JENKINS MODEL IDENTIFICATION FOR ARMA(1,2) AND ARMA(4,3) MODELS

- 1. In Figure 8A.4a–d, we show true autocorrelations, sample autocorrelations, true partial autocorrelations, and sample partial autocorrelations for the ARMA(1,2) model

## TABLE 8A.1

## Patterns Used for Box–Jenkins Model Identification

AR(p)
φ_kk = 0,  k > p (φ_pp = φ_p ≠ 0)
ρ_k is a damped { exponential (p = 1) 
 sinusoid and / or exponential (p > 1) }
MA(q)
ρ_k = 0,  k > q (ρ_q ≠ 0)
φ_kk is a dominated by damped { exponential (q = 1) 
 sinusoid and / or exponential (q > 1) }
ARMA(q,p)
ρ_k is a damped exponential or sinusoid after first q−p
φ_kk is dominated by damped exponential or sinusoid after first p−q
