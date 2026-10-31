high-order AR model to data with the understanding that this may create spurious peaks.

![](bbox=[0.17, 0.2, 0.82, 0.63])

# FIGURE 7.1

(a) True spectral density for the AR(4) model in Example 7.9b, (b) AR(4) spectral density estimator, (c) AR(2) spectral density estimator, and (d) AR(12) spectral density estimator.

+   2. An ARMA(2,1) model: Figure 7.2a shows the true spectral density for the ARMA(2,1) model discussed in Example 7.10. Table 7.10 shows estimation results based on the realization from this model that was shown in Figure 3.24a. In Figure 7.2b, we show the ARMA(2,1) spectral density estimator based on ML estimates. It is seen that the estimated spectral density is very similar to the true spectral density in Figure 7.2a in that it has a single peak at about f = 0.1 along with a dip at f = 0 associated with the MA component. Figure 7.2c shows the periodogram and Figure 7.2d shows the Parzen spectral density estimator based on a truncation point M = 28(= 2√200), the default value for