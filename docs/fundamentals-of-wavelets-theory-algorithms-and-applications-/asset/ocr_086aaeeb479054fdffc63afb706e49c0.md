properly since the spline wavelets are not symmetrical with respect to the origin. The CIWT circumvents this problem by shifting the location of the IWT in the time axis by \(at^*\) toward the right.

The integral wavelet transform of a function gives local time-scale information. To get the time-frequency information, we need to map the scale parameter to frequency. There is no general way of doing so. However, as a first approximation, we may consider the following mapping,

```
(8.36) \(a \mapsto f := \frac{c}{a},\)
```

where \(c > 0\) is a calibration constant. In this book, the constant \(c\) has been determined based on the one-sided center (\(\omega_+^*\)) and one-sided radius (\(\Delta\hat{\Psi}_+\)) of the wavelet \(\hat{\psi}(\omega)\), which are defined in Chapter 4.

For the cubic spline wavelet we get \(\omega_+^* = 5.164\) and \(\Delta\hat{\Psi}_+ = 0.931\). The corresponding figures for the linear spline wavelet are 5.332 and 2.360, respectively. Based on these parameters, we choose values of \(c\) as 1.1 for cubic spline and 1.5 for linear spline cases. It is important to point out that these values of \(c\) may not be suitable for all cases. Further research in this direction is required. We have chosen \(c\) by taking the lower cut-off frequency of \(\hat{\psi}(\omega)\).