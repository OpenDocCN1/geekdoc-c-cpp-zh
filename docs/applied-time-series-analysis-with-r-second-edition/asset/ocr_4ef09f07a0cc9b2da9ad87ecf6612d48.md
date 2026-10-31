Echolocation signal. (b) Sample autocorrelations. (c) Parzen window spectral estimator.

These and other time series will be investigated in more detail in future chapters. The following chapters discuss the use of tools such as the autocorrelation and spectral density, and models such as the AR model for properly analyzing stationary and nonstationary time series data. For now, we have simply introduced these ideas briefly to help the reader begin to understand the concepts.

# Appendix 1A: Fourier Series

In Definition 1.15, we define the periodogram of a discrete time series $X_t$ to be

I. $I(f_j)=\hat{\sigma}_X^2+2\sum_{k=1}^{n-1}\hat{\gamma}_k\cos2\pi f_j k,$  (1A.1)

where $f_j$ are the harmonics of the fundamental frequency $1/n$. Specifically,

$f_j=j/n,\quad j=1,\dots,n/2\ (\text{if }n\text{ is even})$ 
$=j/n,\quad j=1,\dots,m\ (\text{if }n\text{ is odd and }n=2m+1).$

It is interesting to note that the periodogram has two useful alternate representations. The periodogram in Equation 1A.1 can be obtained as $1/n$ times the modulus squared of the Fourier transform of the data as given by Equation 1A.2.

II. $I(f_j)=\frac{1}{n}\left|\sum_{t=1}^{n}x_t e^{(-2\pi i j t / n)}\right|^2.$  (1A.2)

The proof of the equality of forms Equations 1A.1 and 1A.2 is left as Problem 1.20.

The third form of the periodogram involves the Fourier series. In this appendix, we discuss the topic of fitting a Fourier series to a discrete time series