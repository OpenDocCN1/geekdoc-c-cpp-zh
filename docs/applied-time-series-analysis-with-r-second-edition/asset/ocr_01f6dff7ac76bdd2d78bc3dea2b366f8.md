![](bbox=[0.38, 0.12, 0.62, 0.26])

![](bbox=[0.15, 0.32, 0.45, 0.54])

![](bbox=[0.55, 0.32, 0.85, 0.54])

# FIGURE 1.18

Plots associated with the model (1.40) of Example 1.9. (a) Realization. (b) Autocorrelation plot. (c) Spectral density plot.

The true autocorrelations, ρ_k, for models (1.40) and (1.41) are displayed in Figures 1.18b and 1.19b, respectively. In Figure 1.18b, it can be seen that the true autocorrelations damp exponentially to zero, but that there is relatively high positive correlation between X_t and X_{t+k} for small k, which is consistent with our observation from the data themselves. The autocorrelations shown in Figure 1.19b appear to be a damped oscillating exponential. In Figure 1.18c, the peak at f = 0 indicates that associated realizations such as the one in Figure 1.18a show little or no periodic behavior, that is, the data are primarily low frequency with no real periodic tendency. On the other hand, the spectral plot shown in Figure 1.19c is close to zero near f = 0 and has its maximum at f = 0.5 indicating that the data have a highly oscillatory nature, that is, they are predominantly high frequency with a period of about 2.

**Using R:** R commands for creating plots such as those in Figures 1.18 through 1.22 showing a realization, theoretical autocorrelations, and spectral density