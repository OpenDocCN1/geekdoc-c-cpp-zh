again apply the Parzen window spectral density estimator, and the resulting spectral density estimate is shown in Figure 12.2b, where we can see how the spectrum has been spread in an attempt to adjust for the changing frequencies. In Figure 12.2b the “peak” in the spectrum extends from about f = 0 to a little below f = 0.2 reflecting the fact that the frequency behavior varies within this range across time. The concept of a “spread spectrum” was introduced in Example 1.16.

![](bbox=[0.15, 0.3, 0.8, 0.55])

# FIGURE 12.2

(a) Linear chirp. (b) Spectral estimate for realization in (a).

In summary, we note that since the spectrum “assumes” that the time series is stationary, that is, that its frequency behavior does not change over time, it does not provide insight regarding any time–frequency behavior in the data. Note, for example, that if the realization in Figure 12.2a was simply reversed in direction so that the frequencies decreased in time, the Parzen spectral density estimate would not reflect the change in direction. In essence using classical spectral estimation methods, the frequency content at a given frequency is found by averaging over time. If characteristics of the signal depend on time, then these classical methods are not appropriate and can lead to misleading results.

# 12.2 Window-Based Methods that Localize the “Spectrum” in Time

A method for obtaining frequency information that is localized in time is needed in order to address the concerns raised in Section 12.1. In this section we discuss