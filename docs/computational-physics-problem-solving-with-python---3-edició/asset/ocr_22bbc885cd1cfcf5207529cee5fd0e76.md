# 13

# Wavelet and Principal Components Analyses: Nonstationary Signals and Data Compression

There are a number of techniques that extend Fourier analysis to signals whose forms change in time. This chapter introduces *wavelet analysis*, a field that has seen extensive development and application in areas as diverse as brain waves, stock-market trends, gravitational waves, and compression of photographic images. The first part of the chapter deals with wavelet basics, and covers the essential materials. The second part of the chapter explores the discrete wavelet transform, and is marked as optional as a result of its technical nature. However, it is a beautiful bit of analysis and the basis of much of the digital revolution. The chapter ends with a discussion of principal component analysis, another powerful technique for analyzing signals with space and time correlations.

# 13.1

**Problem: Spectral Analysis of Nonstationary Signals**

**Problem**  You have sampled the signal in Figure 13.1 that seems to contain an increasing number of frequencies as time increases. Your *problem* is to undertake a spectral analysis of this signal that tells you, in the most compact way possible, the amount of each frequency present at each instant of time. *Hint:* Although we want the method to be general enough to work with numerical data, for pedagogical purposes it is useful to know that the signal is

$$
y(t)=
\begin{cases}
\sin 2\pi t, & \text{for } 0\le t\le 2,\\
5\sin 2\pi t+10\sin 4\pi t, & \text{for } 2\le t\le 8,\\
2.5\sin 2\pi t+6\sin 4\pi t+10\sin 6\pi t, & \text{for } 8\le t\le 12.
\end{cases}
\tag{13.1}
$$

# 13.2

## Wavelet Basics

The Fourier analysis we used in Chapter 12 reveals the amount of the harmonic functions $\sin(\omega t)$ and $\cos(\omega t)$, and their overtones, that are present in a signal. An