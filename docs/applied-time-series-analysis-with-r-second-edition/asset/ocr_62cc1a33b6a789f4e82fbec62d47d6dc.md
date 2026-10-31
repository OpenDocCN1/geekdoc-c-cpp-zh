In this section, we consider the case in which $s_t$ is a function of the form $s_t = C\cos(2\pi ft + \mathcal{V})$. In Chapters 1 and 4, we have discussed models with harmonic components and have studied them as a type of stationary process. The stationarity requires that the phase, $\mathcal{V}$, is a random variable. However, in physical situations in which one realization is available, the phase is constant throughout the only realization observed. For this reason, it is often the case that in signal-plus-noise models with harmonic components, the harmonic term, such as $s_t = C\cos(2\pi ft + \mathcal{V})$ is considered to be a deterministic signal as in the case of the trend-plus-noise examples.

Consider the case of the signal-plus-noise model with one harmonic component

$$X_t = C\cos(2\pi ft + \mathcal{V}) + Z_t,$$  \tag{5.4}

which is usually written as

$$X_t = A\cos(2\pi ft) + B\sin(2\pi ft) + Z_t,$$  \tag{5.5}

where $A = C\cos\mathcal{V}$ and $B = -C\sin\mathcal{V}$ using trigonometric identities. In practice, if $X_t$ satisfies Equation 5.5, the data set is analyzed as if it is a nonstationary process, in which case the parameters $A$, $B$, and $f$ are often estimated as a first step, and then the process

$$\widehat{Z}_t = X_t - \widehat{A}\cos(2\pi \widehat{f}t) - \widehat{B}\sin(2\pi \widehat{f}t),$$  \tag{5.6}

is modeled as a stationary process (see Bhansali 1979). While the noise term in Chapter 4 is often taken to be white noise, this is not a requirement in Equation 5.4, and $\widehat{Z}_t$ is typically modeled as an AR($p$) or ARMA($p,q$) process to allow for autocorrelation.

# EXAMPLE 5.2: LYNX DATA

We return to the lynx data (data set lynx in tswge) shown in Figure 3.15 that represent the annual number of lynx trappings in Canada from 1821 to 1934 (see Campbell and Walker, 1977). We previously considered this data set in Example 3.7 where we noted that because of the asymmetry in the actual lynx data shown in Figure 3.15a, the data have historically been analyzed after first taking the log (base 10) of the number of lynx trapped, and this data set (llynx in tswge) is