# Applied Time Series Analysis with R

![](bbox=[0.145, 0.121, 0.835, 0.295])

FIGURE 5.7
Two examples of TVF data: (a) MNTA seismic data and (b) Doppler data.

and seismic signals. Figure 5.7a shows seismic wave data from a explosion (collected at seismic station MNTA in Wyoming) that consist of 700 measurements with a sampling rate of 0.1 s. Examination of the data shows that the periodic behavior is compacting in time, that is, the dominant frequency in the data is increasing with time. Figure 5.7b shows a Doppler signal that dramatically demonstrates frequency behavior that is decreasing with time. These signals are not well modeled using ARMA models which are designed to model stationary behavior. Historically, TVF data have been analyzed using windowing techniques that break the data into windows sufficiently that "stationarity" within the window is a reasonable approximation. However, if the frequencies are changing sufficiently fast (as in the Doppler signal), then such a procedure is problematic at best.

In Chapter 12, we discuss the short-term Fourier transform and wavelets for dealing with TVF data. If the frequencies in the data are changing in time in a smoother manner as is the case in the three TVF realizations in Figures 1.26a and 5.7, the data can be modeled using G-stationary models. These are models for which the data are nonstationary, but an appropriate transformation of the time axis produces stationary data that can be modeled using stationary-based techniques. G-stationary models are the topic of Chapter 13, and further discussion will be deferred until then.

# Appendix 5A: R Commands

# 5A.1 Basic Computation and Plot Routines

+   * gen.arima.wge(n,phi,theta,d,lambda,vara,sn) is a function that generates a realization of n from a given AR, MA, or ARIMA model.